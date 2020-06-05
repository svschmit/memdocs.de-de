---
title: Intune-Einstellungen für Sicherheitsbaselines in Microsoft Defender Advanced Threat Protection
titleSuffix: Microsoft Intune
description: Von Intune unterstützte Einstellungen für Sicherheitsbaselines zur Verwaltung von Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: 330a4387ef1a079b2a0f691bfb0b887117dd9e4b
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429355"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Microsoft Defender Advanced Threat Protection-Baselineeinstellungen für Intune

Zeigen Sie die Baselineeinstellungen für Microsoft Defender Advanced Threat Protection an, die von Microsoft Intune unterstützt werden. Die Standardeinstellungen der ATP-Baseline (Advanced Threat Protection) entsprechen der für ATP empfohlenen Konfiguration und stimmen möglicherweise nicht mit den Standardeinstellungen anderer Sicherheitsbaselines überein.

::: zone pivot="atp-april-2020"

Die Angaben in diesem Artikel gelten für Version 4 der Microsoft Defender ATP-Baseline, die am 21. April 2020 veröffentlicht wurde. Verwenden Sie die im Bereich *Versionen* für diese Baseline verfügbare Aktion [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Baselines vergleichen), um zu sehen, was sich in dieser Version der Baseline im Vergleich zu früheren Versionen geändert hat.

::: zone-end
::: zone pivot="atp-march-2020"

Die Angaben in diesem Artikel gelten für Version 3 der Microsoft Defender ATP-Baseline, die am 1. März 2020 veröffentlicht wurde. Verwenden Sie die im Bereich *Versionen* für diese Baseline verfügbare Aktion [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Baselines vergleichen), um zu sehen, was sich in dieser Version der Baseline im Vergleich zu früheren Versionen geändert hat.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


Die Microsoft Defender Advanced Threat Protection-Baseline ist verfügbar, wenn Ihre Umgebung den Anforderungen zur Verwendung von [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites) entspricht.

Diese Baseline wurde für physische Geräte optimiert und wird zurzeit nicht für die Verwendung auf virtuellen Computern (VMs) oder VDI-Endpunkten empfohlen. Bestimmte Baselineeinstellungen können sich auf interaktive Remotesitzungen in virtualisierten Umgebungen auswirken. Weitere Informationen finden Sie unter [Increase compliance to the Microsoft Defender ATP security baseline (Erhöhung der Compliance für die Microsoft Defender ATP-Sicherheitsbaseline)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline).


## <a name="application-guard"></a>Application Guard

Weitere Informationen finden Sie in der Windows-Dokumentation unter [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp).  

Während der Verwendung von Microsoft Edge schützt Microsoft Defender Application Guard Ihre Umgebung vor Websites, die von Ihrer Organisation nicht als vertrauenswürdig definiert wurden. Wenn Benutzer Websites besuchen, die nicht in Ihrer isolierten Netzwerkgrenze aufgelistet sind, werden die Websites in einer virtuellen Hyper-V-Browsersitzung geöffnet. Vertrauenswürdige Websites werden durch eine Netzwerkgrenze definiert.  

- **Application Guard für Microsoft Edge aktivieren (Optionen)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Aktiviert für Microsoft Edge** (*Standardeinstellung*): Application Guard öffnet nicht genehmigte Websites in einem virtualisierten Hyper-V-Browsercontainer.
  - **Nicht konfiguriert**: Jede beliebige Website (vertrauenswürdig oder nicht vertrauenswürdig) wird auf dem Gerät geöffnet und nicht in einem virtualisierten Container.  
  
  Wenn *Aktiviert für Microsoft Edge* festgelegt ist, können Sie *Externen Inhalt von genehmigten Nicht-Unternehmensstandorten blockieren* und das *Verhalten der Zwischenablage* konfigurieren.

  - **Externen Inhalt von genehmigten Nicht-Unternehmensstandorten blockieren**  
    CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Ja** (*Standardeinstellung*): Es wird verhindert, dass Inhalte von nicht genehmigten Websites geladen werden.
    - **Nicht konfiguriert**: Websites, bei denen es sich nicht um Unternehmenswebsites handelt, können auf dem Gerät geöffnet werden.

  - **Verhalten der Zwischenablage**  
    CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Legen Sie zulässige Aktionen für das Kopieren und Einfügen zwischen dem lokalen Computer und dem virtuellen Browser von Application Guard fest. Zu den Optionen gehören:
    - **Nicht konfiguriert**  
    - **Kopieren und Einfügen zwischen PC und Browser blockieren** (*Standardeinstellung*): Beides wird blockiert. Daten können zwischen dem Computer und dem virtuellen Browser nicht übertragen werden.
    - **Kopieren und Einfügen nur von Browser zu PC zulassen**: Daten können nicht vom PC in den virtuellen Browser übertragen werden.
    - **Kopieren und Einfügen nur von PC zu Browser zulassen**: Daten können nicht vom virtuellen Browser auf den Host-PC übertragen werden.
    - **Kopieren und Einfügen zwischen PC und Browser zulassen**: Es werden keine Inhalte blockiert.

- **Richtlinie für Windows-Netzwerkisolation**  
  CSP: [Richtlinien-CSP: NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Geben Sie eine Liste von *Netzwerkdomänen* an, bei denen es sich um Unternehmensressourcen handelt, die in der Cloud gehostet werden und die Application Guard als Unternehmenswebsites behandelt.
  - **Konfigurieren** (*Standardeinstellung*)
  - **Nicht konfiguriert**

  Wenn *Konfigurieren* festgelegt ist, können Sie *Netzwerkdomänen* definieren.

  - **Netzwerkdomänen**  
    Klicken Sie auf **Hinzufügen**, und geben Sie Domänen, IP-Adressbereiche und Netzwerkgrenzen an. Die Standardkonfiguration ist *securitycenter.windows.com*.

## <a name="bitlocker"></a>BitLocker

Weitere Informationen finden Sie in der Windows-Dokumentation unter [Einstellungen für BitLocker-Gruppenrichtlinien](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings).

- **Speicherkarten müssen verschlüsselt sein (nur mobil)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Diese Einstellung gilt nur für Geräte mit den SKUs „Windows Mobile“ und „Mobile Enterprise“.
  - **Ja** (*Standardeinstellung*): Die Verschlüsselung von Speicherkarten ist für mobile Geräte erforderlich.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Betriebssystems zurückgesetzt, d. h. die Verschlüsselung von Speicherkarten ist nicht erforderlich.

- **Vollständige Datenträgerverschlüsselung für Betriebssystem- und Festplattenlaufwerke aktivieren**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Wenn das Laufwerk vor Anwendung dieser Richtlinie verschlüsselt wurde, werden keine weiteren Maßnahmen ergriffen. Wenn die Verschlüsselungsmethode und die Optionen mit der Methode und den Optionen dieser Richtlinie übereinstimmen, sollte die Konfiguration erfolgreich sein. Wenn eine direkte BitLocker-Konfigurationsoption nicht dieser Richtlinie entspricht, gibt die Konfiguration wahrscheinlich einen Fehler zurück.
  
  Zur Anwendung dieser Richtlinie auf ein bereits verschlüsseltes Laufwerk entschlüsseln Sie dieses, und wenden Sie die MDM-Richtlinie noch mal an. In der Windows-Standardeinstellung ist keine BitLocker-Laufwerkverschlüsselung erforderlich, für die Azure AD Join- und MSA-Registrierung/-Anmeldung (Microsoft-Konto) kann die automatische Verschlüsselung mit Aktivierung von BitLocker mit der Verschlüsselung „XTS-AES, 128 Bit“ jedoch angewendet werden.

  - **Ja** (*Standardeinstellung*): Die Verwendung von BitLocker wird erzwungen.
  - **Nicht konfiguriert**: BitLocker wird nicht erzwungen.

- **BitLocker: Richtlinie für Systemlaufwerk**  
  [BitLocker-Gruppenrichtlinieneinstellungen](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Konfigurieren** (*Standardeinstellung*)
  - **Nicht konfiguriert**

  Wenn *Konfigurieren* festgelegt ist, haben Sie die Möglichkeit, die Option *Verschlüsselungsmethode für Betriebssystemlaufwerke konfigurieren* zu konfigurieren.

  - **Verschlüsselungsmethode für Betriebssystemlaufwerke konfigurieren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Diese Einstellung ist verfügbar, wenn *BitLocker: Richtlinie für Systemlaufwerk* auf *Konfigurieren* festgelegt ist.  

    Konfigurieren Sie die Verschlüsselungsmethode und Verschlüsselungsstärke für Systemlaufwerke.  *XTS-AES, 128 Bit* ist die Standardverschlüsselungsmethode von Windows und der empfohlene Wert.

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **AES-CBC, 128 Bit**
    - **AES-CBC, 256 Bit**
    - **AES-XTS, 128 Bit**
    - **AES-XTS, 256 Bit**

- **BitLocker: Richtlinie für Festplattenlaufwerk**  
  [BitLocker-Gruppenrichtlinieneinstellungen](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Konfigurieren** (*Standardeinstellung*)
  - **Nicht konfiguriert**

  Wenn *Konfigurieren* festgelegt ist, haben Sie die Möglichkeit, die Optionen *Schreibzugriff auf Festplattenlaufwerke ohne BitLocker-Schutz blockieren* und *Verschlüsselungsmethode für Festplattenlaufwerke konfigurieren* zu konfigurieren.

  - **Schreibzugriff auf Festplattenlaufwerke ohne BitLocker-Schutz blockieren**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Diese Einstellung ist verfügbar, wenn *BitLocker: Richtlinie für Festplattenlaufwerk* auf *Konfigurieren* festgelegt ist.

    - **Nicht konfiguriert** (*Standardeinstellung*): Daten können auf nicht verschlüsselte Festplattenlaufwerke geschrieben werden.
    - **Ja**: Windows lässt nicht zu, dass Daten auf Festplattenlaufwerke geschrieben werden, die nicht durch BitLocker geschützt sind. Wenn ein Festplattenlaufwerk nicht verschlüsselt ist, muss der Benutzer den BitLocker-Setup-Assistenten für das Laufwerk ausführen, bevor er Schreibzugriff erhält.

  - **Verschlüsselungsmethode für Festplattenlaufwerke konfigurieren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Diese Einstellung ist verfügbar, wenn *BitLocker: Richtlinie für Festplattenlaufwerk* auf *Konfigurieren* festgelegt ist.

    Konfigurieren Sie die Verschlüsselungsmethode und Verschlüsselungsstärke für Festplattenlaufwerke. *XTS-AES, 128 Bit* ist die Standardverschlüsselungsmethode von Windows und der empfohlene Wert.

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **AES-CBC, 128 Bit**
    - **AES-CBC, 256 Bit**
    - **AES-XTS, 128 Bit**
    - **AES-XTS, 256 Bit**

- **BitLocker-Richtlinie für Wechseldatenträger**  
  [BitLocker-Gruppenrichtlinieneinstellungen](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Konfigurieren** (*Standardeinstellung*)
  - **Nicht konfiguriert**

  Wenn *Konfigurieren* festgelegt ist, können Sie die Optionen *Configure encryption method for removable data-drives* (Verschlüsselungsmethode für Wechseldatenträger konfigurieren) und *Schreibzugriff auf Wechseldatenträger ohne BitLocker-Schutz blockieren* konfigurieren.

  - **Configure encryption method for removable data-drives** (Verschlüsselungsmethode für Wechseldatenträger konfigurieren)  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Diese Einstellung ist verfügbar, wenn *BitLocker: Richtlinie für Wechseldatenträger* auf *Konfigurieren* festgelegt ist.

    Konfigurieren Sie die Verschlüsselungsmethode und Verschlüsselungsstärke für Laufwerke von Wechseldatenträgern. *XTS-AES, 128 Bit* ist die Standardverschlüsselungsmethode von Windows und der empfohlene Wert.

    - **Nicht konfiguriert**
    - **AES-CBC, 128 Bit**
    - **AES-CBC, 256 Bit** (*Standardeinstellung*)
    - **AES-XTS, 128 Bit**
    - **AES-XTS, 256 Bit**

  - **Schreibzugriff auf Wechseldatenträger ohne BitLocker-Schutz blockieren**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Diese Einstellung ist verfügbar, wenn *BitLocker: Richtlinie für Wechseldatenträger* auf *Konfigurieren* festgelegt ist.

    - **Nicht konfiguriert** (*Standardeinstellung*): Daten können auf nicht verschlüsselte Laufwerke von Wechseldatenträgern geschrieben werden.  
    - **Ja**: Windows lässt nicht zu, dass Daten auf Laufwerke von Wechseldatenträgern geschrieben werden, die nicht durch BitLocker geschützt sind. Wenn ein Laufwerk eines Wechseldatenträgers nicht verschlüsselt ist, muss der Benutzer den BitLocker-Setup-Assistenten für das Laufwerk ausführen, bevor er Schreibzugriff erhält.

## <a name="browser"></a>Browser

- **SmartScreen für Microsoft Edge anfordern**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ja** (*Standardeinstellung*): SmartScreen wird verwendet, um Benutzer vor potenziellen betrügerischen Phishing-Angriffen und Schadsoftware zu schützen.
  - **Nicht konfiguriert**

- **Zugriff auf schädliche Websites blockieren**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ja** (*Standardeinstellung*): Benutzer werden daran gehindert, Warnungen des Microsoft Defender SmartScreen-Filters zu ignorieren und zu der Website zu wechseln.
  - **Nicht konfiguriert**

- **Block unverified file download** (Herunterladen nicht überprüfter Dateien blockieren)  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ja** (*Standardeinstellung*): Benutzer werden daran gehindert, Warnungen des Microsoft Defender SmartScreen-Filters zu ignorieren und nicht überprüfte Dateien herunterzuladen.
  - **Nicht konfiguriert**

## <a name="data-protection"></a>Schutz von Daten

- **Block direct memory access** (Direkten Speicherzugriff blockieren)  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Die Richtlinieneinstellung wird nur erzwungen, wenn BitLocker oder die Geräteverschlüsselung aktiviert ist.

  - **Ja** (*Standardeinstellung*): Der direkte Speicherzugriff (DMA) für alle Hot-Plug-fähigen PCI-Downstreamports wird blockiert, bis sich ein Benutzer bei Windows anmeldet. Nachdem sich ein Benutzer angemeldet hat, werden die an die Hot-Plug-PCI-Ports angeschlossenen PCI-Geräte von Windows aufgezählt. Jedes Mal, wenn der Benutzer den Computer sperrt, wird DMA an Hot-Plug-PCI-Anschlüssen ohne untergeordnete Geräte blockiert, bis sich der Benutzer erneut anmeldet. Geräte, die vor dem Entsperren des Computers bereits aufgezählt wurden, sind weiterhin funktionsfähig, bis sie entfernt werden oder das System neu gestartet bzw. in den Ruhezustand versetzt wird.
  - **Nicht konfiguriert**

## <a name="device-guard"></a>Device Guard  

- **Credential Guard aktivieren**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard verwendet den Windows-Hypervisor, um Schutz bereitzustellen. Zur ordnungsgemäßen Funktion sind „Sicherer Start“ und DMA-Schutz erforderlich, die wiederrum erfordern, dass die Hardwareanforderungen erfüllt sind.

  - **Nicht konfiguriert**: Die Verwendung von Credential Guard wird deaktiviert. Hierbei handelt es sich um die Windows-Standardeinstellung.
  - **Mit UEFI-Sperre aktivieren** (*Standardeinstellung*): Credential Guard wird aktiviert und kann nicht remote deaktiviert werden, weil die UEFI-Konfiguration manuell gelöscht werden muss.
  - **Ohne UEFI-Sperre aktivieren**: Credential Guard wird aktiviert und kann ohne physischen Zugriff auf den Computer deaktiviert werden.

## <a name="device-installation"></a>Geräteinstallation

- **Hardware device installation by device identifiers** (Installation von Hardwaregeräten anhand der Geräte-ID)  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Mit dieser Richtlinieneinstellung können Sie eine Liste von Plug & Play-Hardware-IDs und kompatiblen IDs für Geräte angeben, deren Installation unter Windows verhindert wird. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht.  Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus.

  - **Nicht konfiguriert**
  - **Installation von Hardwaregeräten zulassen**: Geräte können installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.
  - **Installation von Hardwaregeräten blockieren** (*Standardeinstellung*): Windows wird an der Installation gehindert, wenn die zugehörige Hardware-ID oder kompatible ID in der von Ihnen erstellten Liste enthalten ist.

  Wenn *Installation von Hardwaregeräten blockieren* festgelegt ist, können Sie die Optionen *Übereinstimmende Hardwaregeräte entfernen* und *Hardwaregerätebezeichner, die blockiert werden* konfigurieren.

  - **Zugehörige Hardwaregeräte entfernen** (Übereinstimmende Hardwaregeräte entfernen)

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.
    - **Ja**
    - **Nicht konfiguriert**

  - **Hardware device identifiers that are blocked** (Blockierte Bezeichner von Hardwaregeräten)  
    
    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.

    Klicken Sie auf **Hinzufügen**, und geben Sie die ID des Hardwaregeräts an, das Sie blockieren möchten.

- **Hardware device installation by device identifiers** (Installation von Hardwaregeräten anhand der Setupklassen)  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Mit dieser Richtlinieneinstellung können Sie eine Liste von GUIDs für Gerätesetupklassen angeben, die Gerätetreiber beschreiben, die unter Windows nicht installierbar sind. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht. Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus.

  - **Nicht konfiguriert**
  - **Installation von Hardwaregeräten zulassen**: Geräte können von Windows installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.
  - **Installation von Hardwaregeräten blockieren** (*Standardeinstellung*): Windows wird an der Installation eines Geräts gehindert, dessen GUIDs für Setupklassen in der von Ihnen erstellten Liste enthalten sind.

  Wenn *Installation von Hardwaregeräten blockieren* festgelegt ist, können Sie die Optionen *Übereinstimmende Hardwaregeräte entfernen* und *Hardwaregerätebezeichner, die blockiert werden* konfigurieren.

  - **Zugehörige Hardwaregeräte entfernen** (Übereinstimmende Hardwaregeräte entfernen)

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.
    - **Ja**
    - **Nicht konfiguriert**

  - **Hardware device identifiers that are blocked** (Blockierte Bezeichner von Hardwaregeräten)

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.

    Klicken Sie auf **Hinzufügen**, und geben Sie die ID des Hardwaregeräts an, das Sie blockieren möchten.

## <a name="dma-guard"></a>DMA Guard

- **Aufzählung externer Geräte, die mit Kernel-DMA-Schutz nicht kompatibel sind**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Diese Richtlinie kann zusätzliche Sicherheit für externe DMA-fähige Geräte bieten. Sie ermöglicht eine bessere Kontrolle über die Aufzählung von externen DMA-fähigen Geräten, die mit DMA Remapping/Gerätespeicherisolation und Sandboxing nicht kompatibel sind.
  
  Diese Richtlinie gilt nur, wenn der Kernel-DMA-Schutz unterstützt wird und durch die Systemfirmware aktiviert wurde. Kernel-DMA-Schutz ist ein Plattformfeature, das zum Zeitpunkt der Herstellung vom System unterstützt werden muss. Sie können auf der Zusammenfassungsseite der Datei „MSINFO32.exe“ über das Feld „Kernel DMA Protection“ (Kernel-DMA-Schutz) überprüfen, ob das System den Kernel-DMA-Schutz unterstützt.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Alle blockieren**
  - **Alle zulassen**

## <a name="endpoint-detection-and-response"></a>Endpunkterkennung und Reaktion

Weitere Informationen zu den folgenden Einstellungen finden Sie in der Windows-Dokumentation unter [CSP „WindowsAdvancedThreatProtection“](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp).

- **Beispielfreigabe für alle Dateien**  
  CSP: [Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Hiermit wird der Konfigurationsparameter für die Microsoft Defender Advanced Threat Protection-Beispielfreigabe zurückgegeben oder festgelegt.  
  
  - **Ja** (*Standardeinstellung*)
  - **Nicht konfiguriert**

- **Häufigkeit von Telemetrieberichten erhöhen**  
  CSP: [Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Hiermit wird die Häufigkeit von Microsoft Defender Advanced Threat Protection-Telemetrieberichten erhöht.  

  - **Ja** (*Standardeinstellung*)
  - **Nicht konfiguriert**

## <a name="firewall"></a>Firewall

Weitere Informationen finden Sie in der Windows-Dokumentation unter [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp).

- **Zustandsbehaftetes FTP (File Transfer Protocol) deaktivieren**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Ja** (*Standardeinstellung*)
  - **Nicht konfiguriert**: Die Firewall verwendet FTP zum Untersuchen und Filtern sekundärer Netzwerkverbindungen, sodass Ihre Firewallregeln möglicherweise ignoriert werden.

- **Die Anzahl der Sekunden, die sich eine Sicherheitszuordnung im Leerlauf befinden kann, bevor Sie gelöscht wird**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Geben Sie an, wie lange die Sicherheitszuordnungen beibehalten werden, nachdem kein Netzwerkdatenverkehr mehr angezeigt wird. Wenn diese Einstellung nicht konfiguriert ist, löscht das System eine Sicherheitszuordnung im Leerlauf nach *300* Sekunden (Standardeinstellung).
  
  Die Anzahl muss zwischen **300** und **3600** Sekunden liegen.

- **Codierung vorinstallierter Schlüssel**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Wenn UTF-8 nicht erforderlich ist, werden vorinstallierte Schlüssel anfangs mit UTF-8 verschlüsselt. Anschließend können Gerätebenutzer eine andere Verschlüsselungsmethode auswählen.

  - **Nicht konfiguriert**
  - **Keine**
  - **UTF8** (*Standardeinstellung*)

- **Überprüfung der Zertifikatssperrliste (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Geben Sie an, wie die Überprüfung der Zertifikatssperrliste (CRL) durchgesetzt wird.  

  - **Nicht konfiguriert** (*Standardeinstellung*): Die CRL-Überprüfung wird deaktiviert.
  - **Keine**
  - **Versuch**
  - **Require**

- **Paketwarteschlangen**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Geben Sie an, wie die Skalierung für die Software auf der Empfangsseite für den verschlüsselten Empfang und die Weiterleitung im Klartext für das IPsec-Tunnelgatewayszenario aktiviert werden soll. Durch diese Einstellung wird die Paketreihenfolge beibehalten.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung für Paketwarteschlangen wird auf den Standardwert des Clients zurückgesetzt, d. h. diese werden deaktiviert.
  - **Deaktiviert**
  - **Warteschlange für eingehenden Datenverkehr**
  - **Warteschlange für ausgehenden Datenverkehr**
  - **Warteschlange für beide**

- **Firewallprofil: privat**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Konfigurieren** (*Standardeinstellung*)
  - **Nicht konfiguriert**

  Wenn die Einstellung auf *Konfigurieren* festgelegt ist, können Sie die folgenden zusätzlichen Einstellungen konfigurieren.

  - **Eingehende Verbindungen blockiert**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Unicastantworten auf Multicastbroadcasts erforderlich**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Geschützter Modus erforderlich**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Ausgehende Verbindungen erforderlich**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Eingehende Benachrichtigungen blockiert**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Globale Portregeln aus Gruppenrichtlinie zusammengeführt**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Geschützter Modus blockiert**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Firewall aktiviert**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Nicht konfiguriert**
    - **Gesperrt**
    - **Zulässig** (*Standardeinstellung*)

  - **Autorisierte Anwendungsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Eingehender Datenverkehr erforderlich**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

- **Firewallprofil: öffentlich**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Konfigurieren** (*Standardeinstellung*)
  - **Nicht konfiguriert**

  Wenn die Einstellung auf *Konfigurieren* festgelegt ist, können Sie die folgenden zusätzlichen Einstellungen konfigurieren.

  - **Eingehende Verbindungen blockiert**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Unicastantworten auf Multicastbroadcasts erforderlich**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Geschützter Modus erforderlich**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Ausgehende Verbindungen erforderlich**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Autorisierte Anwendungsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Eingehende Benachrichtigungen blockiert**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Globale Portregeln aus Gruppenrichtlinie zusammengeführt**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Geschützter Modus blockiert**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Firewall aktiviert**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Nicht konfiguriert**
    - **Gesperrt**
    - **Zulässig** (*Standardeinstellung*)

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Eingehender Datenverkehr erforderlich**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

- **Firewallprofil: Domäne**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Unicastantworten auf Multicastbroadcasts erforderlich**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Autorisierte Anwendungsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**  

  - **Eingehende Benachrichtigungen blockiert**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Globale Portregeln aus Gruppenrichtlinie zusammengeführt**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Geschützter Modus blockiert**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Firewall aktiviert**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Nicht konfiguriert**
    - **Gesperrt**
    - **Zulässig** (*Standardeinstellung*)

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*Standardeinstellung*)
    - **Nicht konfiguriert**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Tägliche Schnellüberprüfung ausführen um**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Konfigurieren Sie, wann die tägliche Schnellüberprüfung ausgeführt wird. Die Standardeinstellung für den Ausführungszeitpunkt der Schnellüberprüfung ist **2 Uhr**.

- **Scheduled scan start time** (Startzeit für die geplante Überprüfung)  
  
  In der Standardeinstellung ist diese Eigenschaft auf **2 Uhr** festgelegt.

- **Niedrige CPU-Priorität für geplante Überprüfungen konfigurieren**  
  CSP: [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Ja** (*Standardeinstellung*)
  - **Nicht konfiguriert**

- **Erstellung untergeordneter Prozesse durch Office-Kommunikations-Apps blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874499)  

  Diese ASR-Regel wird über die folgende GUID gesteuert: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. die Erstellung von untergeordneten Prozessen wird nicht blockiert.
  - **Benutzerdefiniert**
  - **Aktivieren** (*Standardeinstellung*): Office-Kommunikationsanwendungen werden am Erstellen von untergeordneten Prozessen gehindert.
  - **Überwachungsmodus**: Untergeordnete Prozesse werden nicht blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Adobe Reader am Erstellen von untergeordneten Prozessen hindern**  
  [Reduzieren von Angriffsflächen mit Regeln zur Reduzierung von Angriffsflächen](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. die Erstellung von untergeordneten Prozessen wird nicht blockiert.
  - **Benutzerdefiniert**
  - **Aktivieren** (*Standardeinstellung*): Adobe Reader wird am Erstellen von untergeordneten Prozessen gehindert.
  - **Überwachungsmodus**: Untergeordnete Prozesse werden nicht blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Eingehende E-Mail-Nachrichten überprüfen**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Das E-Mail-Postfach sowie E-Mail-Dateien wie PST-, DBX-, MNX-, MIME- und BINHEX-Dateien werden überprüft.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. E-Mail-Dateien werden nicht überprüft.

- **Echtzeitschutz aktivieren**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Die Echtzeitüberwachung wird erzwungen, und der Benutzer kann diese nicht deaktivieren.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. aktiviert. Der Benutzer kann diese jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um die Echtzeitüberwachung zu deaktivieren.

- **Anzahl von Tagen (0–90) zum Aufbewahren der unter Quarantäne gestellten Schadsoftware**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Konfigurieren Sie die Anzahl der Tage, für die Elemente im Quarantäneordner aufbewahrt werden sollen, bevor sie entfernt werden. Der Standardwert ist 0 (**null**) und gibt an, dass Elemente in der Quarantäne nie entfernt werden.

- **Defender system scan schedule** (Defender-Zeitplan für Systemüberprüfung)  
  CSP: [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Legen Sie fest, an welchem Tag Defender Geräte überprüfen soll. Die Standardeinstellung der Überprüfung ist **Benutzerdefiniert**, kann jedoch auf *Täglich*, also an jedem Tag der Woche, oder auf *Keine Überprüfung geplant* festgelegt werden.

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout** (Zusätzliche Zeit (0–50 Sekunden) zum Verlängern des Zeitlimits für Cloudschutz)  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender Antivirus blockiert verdächtige Dateien automatisch 10 Sekunden lang, um die Dateien in der Cloud zu überprüfen und sicherzustellen, dass sie sicher sind. Bei dieser Einstellung können Sie dieses Timeout um 50 Sekunden verlängern.  Der Standardwert für das Zeitlimit ist auf 0 (**null**) Sekunden festgelegt.

- **Bei einer vollständigen Überprüfung zugeordnete Netzlaufwerke überprüfen**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Bei einer vollständigen Überprüfung werden zugeordnete Netzwerklaufwerke eingeschlossen.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. die Überprüfung auf zugeordneten Netzlaufwerken wird deaktiviert.

- **Netzwerkschutz aktivieren**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Ja** (*Standardeinstellung*): Böswilliger Datenverkehr, der durch Signaturen im Netzwerkinspektionssystem (NIS) erkannt wurde, wird blockiert.
  - **Nicht konfiguriert**

- **Alle heruntergeladenen Dateien und Anlagen überprüfen**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Alle heruntergeladenen Dateien und Anlagen werden überprüft. Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. aktiviert. Der Benutzer kann diese jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um diese Einstellung zu deaktivieren.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. aktiviert. Der Benutzer kann diese jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um diese Einstellung zu deaktivieren.

::: zone-end
::: zone pivot="atp-april-2020"

- **Zugriffsbasierten Schutz blockieren**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ja**
  - **Nicht konfiguriert** (*Standardeinstellung*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Zugriffsbasierten Schutz blockieren**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ja** (*Standardeinstellung*)
  - **Nicht konfiguriert**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Browserskripts überprüfen**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Die Skriptüberprüfungsfunktionen von Microsoft Defender werden erzwungen, und der Benutzer kann diese nicht deaktivieren.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. die Skriptüberprüfung ist aktiviert. Der Benutzer kann diese jedoch deaktivieren.

- **Benutzerzugriff auf Microsoft Defender-App blockieren**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Auf die Benutzeroberfläche von Microsoft Defender kann nicht zugegriffen werden, und Benachrichtigungen werden unterdrückt.
  - **Nicht konfiguriert**: Wenn diese Einstellung auf „Ja“ festgelegt ist, kann auf die Windows Defender-Benutzeroberfläche nicht zugegriffen werden, und Benachrichtigungen werden unterdrückt. Wenn die Einstellung auf „Nicht konfiguriert“ festgelegt ist, wird sie auf den Standardwert des Clients zurückgesetzt, d. h. Benutzeroberfläche und Benachrichtigungen sind zulässig.

- **Maximal zulässige CPU-Auslastung (0–100 Prozent) pro Überprüfung**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Geben Sie die maximale CPU-Auslastung in Prozent an, die für eine Überprüfung verwendet werden soll. Der Standardwert ist **50**.

- **Überprüfungstyp**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Benutzerdefiniert**
  - **Deaktiviert**
  - **Schnellüberprüfung** (*Standardeinstellung*)
  - **Vollständige Überprüfung**

- **Eingeben, wie oft (0–24 Stunden) nach Security Intelligence-Updates gesucht wird**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Geben Sie in Stunden an, wie oft nach aktualisierten Signaturen gesucht werden soll. Beispielsweise wird bei einem Wert von 1 jede Stunde überprüft. Beim Wert 2 erfolgt alle zwei Stunden eine Suche usw.

  Wenn kein Wert definiert ist, verwenden die Geräte den Standardwert des Clients, d. h. **8** Stunden.

- **Zustimmung für die Übermittlung von Beispielen in Windows Defender**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Diese Einstellung sucht nach der Benutzerzustimmungsebene in Microsoft Defender, um Daten zu senden. Wenn die erforderliche Zustimmung bereits erteilt wurde, sendet Microsoft Defender die Daten. Wenn nicht (und wenn der Benutzer angegeben hat, nie zu fragen), wird die Benutzeroberfläche gestartet, um den Benutzer zur Einwilligung aufzufordern (sofern *Schutz über die Cloud* auf *Ja* festgelegt wurde), bevor Daten gesendet werden.

  - **Sichere Beispiele automatisch senden** (*Standardeinstellung*)
  - **Immer bestätigen**
  - **Nie senden**
  - **Alle Beispiele automatisch senden**

- **Von der Cloud bereitgestellte Schutzebene**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Konfigurieren Sie, wie aggressiv Defender Antivirus beim Blockieren und Überprüfen verdächtiger Dateien vorgehen soll.
  - **Nicht konfiguriert** (*Standardeinstellung*): Standardmäßige Blockierungsebene von Defender.
  - **Hoch**: Unbekannte Dateien werden aggressiv blockiert, gleichzeitig wird die Clientleistung optimiert. Dies beinhaltet eine höhere Wahrscheinlichkeit falsch positiver Ergebnisse.
  - **Hoher Zuwachs**: Unbekannte Dateien werden aggressiv blockiert, und es werden zusätzliche Schutzmaßnahmen angewendet, die möglicherweise die Clientleistung beeinträchtigen.
  - **Keine Toleranz**: Alle unbekannten ausführbaren Dateien werden blockiert.

- **Archivdateien überprüfen**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Das Scannen von Archivdateien wie ZIP- oder CAB-Dateien wird erzwungen.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. archivierte Dateien werden überprüft. Der Benutzer kann die Überprüfung jedoch deaktivieren.

- **Verhaltensüberwachung aktivieren**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Die Verhaltensüberwachung wird erzwungen, und der Benutzer kann diese nicht deaktivieren.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. aktiviert. Der Benutzer kann diese jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um die Echtzeitüberwachung zu deaktivieren.
  
- **Bei vollständiger Überprüfung Wechseldatenträger überprüfen**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Bei einer vollständigen Überprüfung werden Laufwerke von Wechseldatenträgern (z. B. USB-Speichersticks) überprüft.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Wechseldatenträger werden überprüft. Der Benutzer kann diese Überprüfung jedoch deaktivieren.
  
- **Netzwerkdateien überprüfen**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Ja** (*Standardeinstellung*): Microsoft Defender überprüft Netzwerkdateien.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. die Überprüfung von Netzwerkdateien ist deaktiviert.
  
- **Potenziell unerwünschte App-Aktion in Defender**  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Geben Sie den Erkennungsgrad für potenziell unerwünschte Anwendungen (Potentially Unwanted Applications, PUAs) an. Defender warnt Benutzer, wenn potenziell unerwünschte Software heruntergeladen oder versucht wird, solche Software auf einem Gerät zu installieren.
  - **Gerätestandard**
  - **Blockieren** (*Standardeinstellung*): Erkannte Elemente werden blockiert und im Verlauf zusammen mit anderen Bedrohungen angezeigt.
  - **Überwachung**: Defender erkennt potenziell unerwünschte Anwendungen, ergreift aber keine Maßnahmen. Sie finden Informationen zu den Anwendungen, bei denen Defender Aktionen ausgeführt hätte, indem Sie nach Ereignissen suchen, die von Defender in der Ereignisanzeige erstellt wurden.

- **Von der Cloud bereitgestellten Schutz aktivieren**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standardmäßig sendet Defender auf Windows 10-Desktop-Geräten Informationen zu allen gefundenen Problemen an Microsoft. Microsoft analysiert diese Informationen, um mehr über die Probleme zu erfahren, die Sie und andere Kunden betreffen, und dann verbesserte Lösungen anzubieten.

  - **Ja** (*Standardeinstellung*): Der von der Cloud bereitgestellte Schutz ist aktiviert.  Gerätebenutzer können diese Einstellung nicht ändern.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert des Systems zurückgesetzt.

- **Einschleusung von Code durch Office-Anwendungen in andere Prozesse blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872974)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Einschleusungen von Code durch Office-Anwendungen in andere Prozesse werden blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Erstellung ausführbarer Inhalte durch Office-Anwendungen blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872975)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Das Erstellen von ausführbarem Inhalt durch Office-Anwendungen wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.
  
- **Starten heruntergeladener ausführbarer Inhalte durch JavaScript oder VBScript blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872979)

   Diese ASR-Regel wird über die folgende GUID gesteuert: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Defender blockiert das Ausführen von JavaScript- oder VBScript-Dateien, die aus dem Internet heruntergeladen wurden.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.
  
- **Netzwerkschutz aktivieren**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Benutzerdefiniert**
  - **Aktivieren**: Der Netzwerkschutz ist für alle Benutzer im System aktiviert.
  - **Überwachungsmodus** (*Standardeinstellung*): Benutzer werden nicht für gefährliche Domänen blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Nicht vertrauenswürdige und nicht signierte Prozesse, die über USB ausgeführt werden, blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874502)

  Diese ASR-Regel wird über die folgende GUID gesteuert: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Nicht vertrauenswürdige und nicht signierte Prozesse, die über ein USB-Laufwerk ausgeführt werden, werden blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Diebstahl von Anmeldeinformationen aus dem Subsystem für die lokale Sicherheitsautorität (lsass.exe) von Windows blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874499)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Benutzerdefiniert**
  - **Aktivieren** (*Standardeinstellung*): Versuche, Anmeldeinformationen über „lsass.exe“ zu stehlen, werden blockiert.
  - **Überwachungsmodus**: Benutzer werden nicht für gefährliche Domänen blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Download ausführbarer Inhalte aus E-Mail- und Webmailclients blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Ausführbarer Inhalt, der von E-Mail- oder Webmailclients heruntergeladen wurde, wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Alle Office-Anwendungen am Erstellen von untergeordneten Prozessen hindern**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872976)

  Diese ASR-Regel wird über die folgende GUID gesteuert: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*)
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Ausführung möglicherweise verschleierter Skripts blockieren (js/vbs/ps)**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872978)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Defender blockiert die Ausführung verborgener Skripts.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Win32-API-Aufrufe über Office-Makros blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872977)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren** (*Standardeinstellung*): Die Verwendung von Win32-API-Aufrufen durch Office-Makros wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Security Center

- **Blockieren der Bearbeitung der Exploit Guard-Schutzumgebung durch Benutzer**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Ja** (*Standardeinstellung*): Benutzer werden daran gehindert, im Microsoft Defender Security Center Änderungen am Bereich der Exploit-Schutzeinstellungen vorzunehmen.
  - **Nicht konfiguriert**: Lokale Benutzer können Änderungen am Bereich der Exploit-Schutzeinstellungen vornehmen.

## <a name="smart-screen"></a>SmartScreen

- **Ignorieren von SmartScreen-Warnungen durch die Benutzer blockieren**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Diese Einstellung erfordert, dass die Einstellung „Enforce SmartScreen for apps and files“ (SmartScreen für Apps und Dateien erzwingen) aktiviert ist.
  - **Ja** (*Standardeinstellung*): SmartScreen bietet keine Option, mit der Benutzer die Warnung ignorieren und die App ausführen können. Die Warnung wird angezeigt, der Benutzer kann Sie jedoch umgehen.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. das Überschreiben durch den Benutzer ist zulässig.

- **Nur Apps aus Store zulassen**  

  - **Ja** (*Standardeinstellung*)
  - **Nicht konfiguriert**

- **Windows SmartScreen aktivieren**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Ja** (*Standardeinstellung*): Die Verwendung von SmartScreen wird für alle Benutzer erzwungen.
  - **Nicht konfiguriert**: Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. SmartScreen wird aktiviert. Benutzer können diese Einstellung jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um SmartScreen zu deaktivieren.

## <a name="windows-hello-for-business"></a>Windows Hello for Business

Weitere Informationen finden Sie in der Windows-Dokumentation unter [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp).

- **Windows Hello for Business blockieren**  

   Windows Hello for Business ist eine alternative Methode zum Anmelden bei Windows durch Ersetzen von Kennwörtern, Smartcards und virtuellen Smartcards.

  - **Nicht konfiguriert**: Geräte stellen Windows Hello for Business bereit. Dies ist die Windows-Standardeinstellung.
  - **Deaktiviert** (*Standardeinstellung*): Geräte stellen Windows Hello for Business bereit.
  - **Aktiviert**: Geräte stellen Windows Hello for Business für keinen Benutzer bereit.

  Wenn *Deaktiviert* festgelegt ist, können Sie die folgenden Einstellungen konfigurieren:

  - **Kleinbuchstaben in PIN**  
    - **Nicht zulässig**
    - **Erforderlich**
    - **Zulässig** (*Standardeinstellung*)

  - **Sonderzeichen in PIN**
    - **Nicht zulässig**
    - **Erforderlich**
    - **Zulässig** (*Standardeinstellung*)

  - **Großbuchstaben in PIN**
    - **Nicht zulässig**
    - **Erforderlich**
    - **Zulässig** (*Standardeinstellung*)

::: zone-end

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Sicherheitsbaselines](security-baselines.md)
- [Vermeiden von Konflikten](security-baselines.md#avoid-conflicts)
- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)