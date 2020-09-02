---
title: Verwalten von Antivireneinstellungen mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien und Verwenden von Berichten für Geräte, die Sie mithilfe von Richtlinien für die Datenträgerverschlüsselung für Endpunktsicherheit in Microsoft Endpoint Manager verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 2460a132711fb19d12f33bbada23756fc2344cca
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194245"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Antivirenrichtlinie für Endpunktsicherheit in Intune

Antivirenrichtlinien für Endpunktsicherheit in Intune unterstützen Sicherheitsadministratoren dabei, sich auf die Verwaltung der einzelnen Gruppen von Antivireneinstellungen für verwaltete Geräte zu konzentrieren. Integrieren Sie Intune mit Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung, um die Antivirenrichtlinie zu verwenden.

Die Antivirenrichtlinie umfasst mehrere Profile. Jedes Profil enthält nur die Einstellungen, die für den Microsoft Defender ATP-Antivirus für macOS, Windows 10 oder für die Benutzeroberfläche der Windows-Sicherheits-App auf Windows 10-Geräten relevant sind.

Diese Antivirenrichtlinien finden Sie unter **Verwalten** im Knoten „Endpunktsicherheit“ im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

Antivirenrichtlinien enthalten dieselben Einstellungen wie die Profile *Endpunktschutz* oder *Geräteeinschränkung* für die Richtlinie [Gerätekonfiguration](../configuration/device-profile-create.md) und ähneln den Einstellungen der Richtlinie [Gerätekonformität](../protect/device-compliance-get-started.md). Diese Richtlinientypen enthalten jedoch zusätzliche Einstellungskategorien, die nicht mit Antivirus in Zusammenhang stehen. Die zusätzlichen Einstellungen können die Konfiguration von Antivirus erschweren. Außerdem sind die Einstellungen der Antivirenrichtlinie für macOS nicht über die anderen Richtlinientypen verfügbar. Aufgrund des Antivirenprofils von macOS müssen die Einstellungen nicht mehr mithilfe von `.plist`-Dateien konfiguriert werden.

## <a name="prerequisites-for-antivirus-policy"></a>Voraussetzungen für eine Antivirenrichtlinie

**Allgemein:**

- **macOS**
  - Eine unterstützte Version von macOS
  - Damit Intune Antivireneinstellungen auf einem Gerät verwalten kann, muss Microsoft Defender ATP auf diesem Gerät installiert sein. Siehe: [Microsoft Defender ATP für macOS](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (in der Dokumentation zu Microsoft Defender ATP)

- **Windows 10 und höher**
  - Es gelten keine zusätzlichen Voraussetzungen.

**Unterstützung für Configuration Manager-Clients** (*Vorschau*)

*Dieses Szenario befindet sich in der Vorschau und erfordert die Verwendung von Configuration Manager, Current Branch-Version 2006 oder höher*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Einrichten der Mandantenanfügung für Configuration Manager-Geräte**: Konfigurieren Sie die *Mandantenanfügung*, um die Bereitstellung von Antivirenrichtlinien auf Geräten zu unterstützen, die von Configuration Manager verwaltet werden. Zum Einrichten der Mandantenanfügung gehört auch die Konfiguration von Configuration Manager-Gerätesammlungen zur Unterstützung der Endpunktsicherheitsrichtlinien von Intune.

  Informationen zur Mandantenanfügung finden Sie unter [Konfigurieren der Mandantenanfügung zur Unterstützung von Endpunktsicherheitsrichtlinien](../protect/tenant-attach-intune.md).

## <a name="antivirus-profiles"></a>Antivirenprofile

### <a name="devices-managed-by-intune"></a>Von Intune verwaltete Geräte

Die folgenden Profile werden für Geräte unterstützt, die Sie mit Intune verwalten:

**macOS**:

- Plattform: **macOS**

  - Profil: **Antivirus**: Verwalten Sie [Einstellungen für Antivirenrichtlinien](../protect/antivirus-microsoft-defender-settings-macos.md) für macOS.

    Wenn Sie [Microsoft Defender ATP für Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) verwenden, können Sie die Antivireneinstellungen für Ihre verwalteten macOS-Geräte über Intune konfigurieren und bereitstellen, anstatt diese Einstellungen mithilfe von `.plist`-Dateien zu konfigurieren.

**Windows 10**:

- Plattform: **Windows 10-Profile**

  - Profil: **Microsoft Defender Antivirus** – Verwalten Sie [Einstellungen für Antivirenrichtlinien](../protect/antivirus-microsoft-defender-settings-windows.md) für Windows 10.

    Defender Antivirus ist die Komponente der nächsten Generation von of Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). Diese Features der nächsten Generation vereinen Technologien wie maschinelles Lernen und Cloudinfrastruktur, um Geräte in Ihrer Unternehmensorganisation zu schützen.

    Das Profil *Microsoft Defender Antivirus* ist eine separate Instanz der Antivireneinstellungen im Profil *Geräteeinschränkungen* für die Gerätekonfigurationsrichtlinie.
  
    Im Unterschied zu den Antivireneinstellungen in einem Profil *Geräteeinschränkungen* , können Sie diese Einstellungen für Geräte verwenden, die gemeinsam verwaltet werden. Um diese Einstellungen verwenden zu können, muss der Schieberegler [Workload für Co-Verwaltung](/configmgr/comanage/how-to-switch-workloads) für Endpoint Protection auf Intune eingestellt sein.

  - Profil: **Microsoft Defender Antivirus-Ausschlüsse**: Verwalten Sie Richtlinieneinstellungen nur für [Antivirus-Ausschlüsse](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    Mit dieser Richtlinie können Sie Einstellungen für die folgenden Microsoft Defender Antivirus-Konfigurationsdienstanbieter verwalten, die Antivirus-Ausschlüsse definieren:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Diese Konfigurationsanbieter für Antivirus-Ausschlüsse werden ebenfalls mithilfe der Richtlinie für *Microsoft Defender Antivirus* verwaltet, die identische Einstellungen für Ausschlüsse umfasst. Einstellungen beider Richtlinientypen (*Antivirus* und *Antivirus-Ausschlüsse*) unterliegen einer [Richtlinienzusammenführung](#policy-merge-for-settings) und erstellen eine übergeordnete Gruppe von Ausschlüssen für entsprechende Geräte und Benutzer.

  - Profil: **Windows-Sicherheitseinstellungen**: Verwalten Sie die [Einstellungen für die Windows-Sicherheits-App](../protect/antivirus-security-experience-windows-settings.md), die Endbenutzer im Microsoft Defender Security Center anzeigen können. Verwalten Sie auch die Benachrichtigungen, die an Benutzer gesendet werden.

    Die Windows-Sicherheits-App wird von einer Reihe von Windows-Sicherheitsfeatures zum Bereitstellen von Benachrichtigungen zur Integrität und Sicherheit des Computers verwendet. Benachrichtigungen der Sicherheits-App umfassen sind Firewalls, Antivirensoftware, Windows Defender SmartScreen und andere.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Von Configuration Manager verwaltete Geräte *(in der Vorschau)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Richtlinienzusammenführungen für Einstellungen

Einige Antivirus-Richtlinieneinstellungen unterstützen das *Zusammenführen von Richtlinien*. Durch Zusammenführung von Richtlinien lassen sich Konflikte vermeiden, die entstehen können, wenn mehrere Richtlinien für dieselben Geräte gelten und dieselbe Einstellung konfigurieren. Intune wertet die von der Richtlinienzusammenführung (aus allen anwendbaren Richtlinien) unterstützten Einstellungen für jeden Benutzer oder jedes Gerät aus. Diese Einstellungen werden dann zu einer einzigen übergeordneten Richtliniengruppe zusammengeführt.

Ein Beispiel: Sie erstellen drei separate Antivirus-Richtlinien, die verschiedene Antivirus-Dateipfadausschlüsse definieren. Letztendlich werden alle drei Richtlinien demselben Benutzer zugewiesen. Da der Microsoft Defender-Konfigurationsanbieter für Dateipfadausschlüsse die Richtlinienzusammenführung unterstützt, bewertet und kombiniert Intune die Dateiausschlüsse von allen anwendbaren Richtlinien für den Benutzer. Die Ausschlüsse werden zu einer übergeordneten Gruppe hinzugefügt, und an das Gerät des Benutzers wird nur eine einzige Liste mit Ausschlüssen übermittelt.

Wenn die Richtlinienzusammenführung für eine Einstellung nicht unterstützt wird, kann es zu Konflikten kommen. Konflikte können dazu führen, dass ein Benutzer oder ein Gerät keine Richtlinie für eine Einstellung empfängt. Die Richtlinienzusammenführung unterstützt z. B. nicht den Konfigurationsdienstanbieter, der die Installation übereinstimmender Geräte-IDs verhindert (*PreventInstallationOfMatchingDeviceIDs*). Konfigurationen für diesen Konfigurationsdienstanbieter werden nicht zusammengeführt, sondern separat verarbeitet.

Bei der separaten Verarbeitung werden Richtlinienkonflikte wie folgt aufgelöst:

1. Die sicherste Richtlinie wird angewendet.
2. Wenn zwei Richtlinien gleichermaßen sicher sind, wird die zuletzt geänderte Richtlinie angewendet.
3. Wenn die zuletzt geänderte Richtlinie den Konflikt nicht auflösen kann, wird keine Richtlinie an den Dienst übermittelt.

### <a name="settings-and-csps-that-support-policy-merge"></a>Einstellungen und Konfigurationsdienstanbieter mit Unterstützung für die Richtlinienzusammenführung

Die folgenden Einstellungen unterstützen die Richtlinienzusammenführung:

[Microsoft Defender Antivirus-Richtlinien](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Defender: auszuschließende Prozesse** – Konfigurationsdienstanbieter: [Defender/ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Dateierweiterungen, die von Überprüfungen und Echtzeitschutz ausgeschlossen werden sollen** – Konfigurationsdienstanbieter: [Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Defender: auszuschließende Dateien und Ordner** – Konfigurationsdienstanbieter: [Defender/ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Berichte zu Antivirenrichtlinien

Berichte zu Antivirenrichtlinien enthalten Statusdetails zu den Antivirenrichtlinien der Endpunktsicherheit und den Gerätestatus. Diese Berichte sind im Knoten „Endpunktsicherheit“ im Microsoft Endpoint Manager Admin Center verfügbar:

Um die Berichte anzuzeigen, wechseln Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431)zu „Endpunktsicherheit“, und wählen Sie **Antivirus** aus. Wenn Sie „Antivirus“ auswählen, wird die Seite „Zusammenfassung“ geöffnet. Zusätzliche Berichts-und Statusansichten sind als zusätzliche Seiten verfügbar.

### <a name="summary"></a>Zusammenfassung

Auf der Seite **Zusammenfassung** können Sie [neue Richtlinien erstellen](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) und eine Liste der zuvor erstellten Richtlinien anzeigen. Die Liste enthält allgemeine Details zum Profil, das in der Richtlinie enthalten ist (Richtlinientyp), und Informationen dazu, ob die Richtlinie zugewiesen ist.

![Seite mit Zusammenfassung der Antivirus-Richtlinie](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Wenn Sie eine Richtlinie aus der Liste auswählen, wird die *Übersichtsseite* für diese Richtlinieninstanz geöffnet, und es werden weitere Informationen angezeigt. Wenn Sie eine Kachel aus dieser Ansicht auswählen, zeigt Intune zusätzliche Details für dieses Profil an, sofern diese verfügbar sind.

![Übersichtsseite der Antivirenrichtlinie](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Fehlerhafte Windows 10-Endpunkte

Auf der Seite **Fehlerhafte Windows 10-Endpunkte** können Sie Informationen zum Antivirenstatus ihrer mit MDM verwalteten Windows 10-Geräte anzeigen. Diese Informationen werden von Windows Defender Antivirus, das auf dem Gerät ausgeführt wird, als *Status des Bedrohungs-Agent* zurückgegeben.

In dieser Ansicht werden nur Geräte mit erkannten Problemen angezeigt. Es werden keine Details für Geräte angezeigt, die als bereinigt identifiziert werden.

![Antivirus-Richtlinie: Seite mit fehlerhaften Endpunkten](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)