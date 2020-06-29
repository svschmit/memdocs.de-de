---
title: Verwalten von Antivireneinstellungen mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien und Verwenden von Berichten für Geräte, die Sie mithilfe von Richtlinien für die Datenträgerverschlüsselung für Endpunktsicherheit in Microsoft Endpoint Manager verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: bfefdee7e949faf9e484ea20e7fc203ee72a9784
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879655"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Antivirenrichtlinie für Endpunktsicherheit in Intune

Die Antivirenrichtlinie für Endpunktsicherheit in Intune unterstützen Sicherheitsadministratoren dabei, sich auf die Verwaltung der einzelnen Gruppen von Antivireneinstellungen für verwaltete Geräte zu konzentrieren. Integrieren Sie Intune mit Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung, um die Antivirenrichtlinie zu verwenden.

Die Antivirenrichtlinie umfasst mehrere Profile. Jedes Profil enthält nur die Einstellungen, die für den Microsoft Defender ATP-Antivirus für macOS, Windows 10 oder für die Benutzeroberfläche der Windows-Sicherheits-App auf Windows 10-Geräten relevant sind.

Diese Antivirenrichtlinien finden Sie unter **Verwalten** im Knoten „Endpunktsicherheit“ im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

Antivirenrichtlinien enthalten dieselben Einstellungen wie die Profile *Endpunktschutz* oder *Geräteeinschränkung* für die Richtlinie [Gerätekonfiguration](../configuration/device-profile-create.md) und ähneln den Einstellungen der Richtlinie [Gerätekonformität](../protect/device-compliance-get-started.md). Diese Richtlinientypen enthalten jedoch zusätzliche Einstellungskategorien, die nicht mit Antivirus in Zusammenhang stehen. Die zusätzlichen Einstellungen können die Konfiguration von Antivirus erschweren. Außerdem sind die Einstellungen der Antivirenrichtlinie für macOS nicht über die anderen Richtlinientypen verfügbar. Aufgrund des Antivirenprofils von macOS müssen die Einstellungen nicht mehr mithilfe von `.plist`-Dateien konfiguriert werden.

## <a name="prerequisites-for-antivirus-policy"></a>Voraussetzungen für eine Antivirenrichtlinie

- **macOS**
  - Eine unterstützte Version von macOS
  - Damit Intune Antivireneinstellungen auf einem Gerät verwalten kann, muss Microsoft Defender ATP auf diesem Gerät installiert sein. Siehe: [Microsoft Defender ATP für macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (in der Dokumentation zu Microsoft Defender ATP)

- **Windows 10 und höher**
  - Damit Intune Antivireneinstellungen auf einem Gerät verwalten kann, muss Microsoft Defender ATP auf diesem Gerät installiert sein. Weitere Informationen finden Sie in [Microsoft Defender ATP für Windows](../protect/advanced-threat-protection.md) in der Intune-Dokumentation.
  - Die Windows-Sicherheits-App ist auf allen Geräten installiert, auf denen Windows 10 ausgeführt wird, und es sind keine weiteren Voraussetzungen erforderlich.

## <a name="antivirus-profiles"></a>Antivirenprofile

**macOS-Profile**:

- **Antivirus**: Verwalten Sie [Einstellungen für Antivirenrichtlinien](../protect/antivirus-microsoft-defender-settings-macos.md) für macOS.

  Wenn Sie [Microsoft Defender ATP für Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) verwenden, können Sie die Antivireneinstellungen für Ihre verwalteten macOS-Geräte über Intune konfigurieren und bereitstellen, anstatt diese Einstellungen mithilfe von `.plist`-Dateien zu konfigurieren.

**Windows 10-Profile:**

- **Microsoft Defender Antivirus** – Verwalten Sie [Einstellungen für Antivirenrichtlinien](../protect/antivirus-microsoft-defender-settings-windows.md) für Windows 10.

  Defender Antivirus ist die Komponente der nächsten Generation von of Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). Der Schutz der nächsten Generation vereint maschinelles Lernen, Big Data-Analyse, eingehende Forschung zur Bedrohungsabwehr und Cloudinfrastruktur zum Schutz von Geräten in Ihrer Unternehmensorganisation.

  Das Profil *Microsoft Defender Antivirus* ist eine separate Instanz der Antivireneinstellungen im Profil *Geräteeinschränkungen* für die Gerätekonfigurationsrichtlinie.
  
  Im Unterschied zu den Antivireneinstellungen in einem Profil *Geräteeinschränkungen* , können Sie diese Einstellungen für Geräte verwenden, die gemeinsam verwaltet werden. Um diese Einstellungen verwenden zu können, muss der Schieberegler [Workload für Co-Verwaltung](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) für Endpoint Protection auf Intune eingestellt sein.

- **Windows-Sicherheitseinstellungen**: Verwalten Sie die [Einstellungen für die Windows-Sicherheits-App](../protect/antivirus-security-experience-windows-settings.md), die Endbenutzer im Microsoft Defender Security Center anzeigen können. Verwalten Sie auch die Benachrichtigungen, die an Benutzer gesendet werden. Die Windows-Sicherheits-App wird von einer Reihe von Windows-Sicherheitsfeatures zum Bereitstellen von Benachrichtigungen zur Integrität und Sicherheit des Computers verwendet. Benachrichtigungen der Sicherheits-App umfassen sind Firewalls, Antivirensoftware, Windows Defender SmartScreen und andere.

## <a name="antivirus-policy-reports"></a>Berichte zu Antivirenrichtlinien

Berichte zu Antivirenrichtlinien enthalten Statusdetails zu den Antivirenrichtlinien der Endpunktsicherheit und den Gerätestatus. Diese Berichte sind im Knoten „Endpunktsicherheit“ im Microsoft Endpoint Manager Admin Center verfügbar:

Um die Berichte anzuzeigen, wechseln Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431)zu „Endpunktsicherheit“, und wählen Sie **Antivirus** aus. Wenn Sie „Antivirus“ auswählen, wird die Seite „Zusammenfassung“ geöffnet. Zusätzliche Berichts-und Statusansichten sind als zusätzliche Seiten verfügbar.

### <a name="summary"></a>Zusammenfassung

Auf der Seite **Zusammenfassung** können Sie [neue Richtlinien erstellen](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) und eine Liste der zuvor erstellten Richtlinien anzeigen. Die Liste enthält allgemeine Details zum Profil, das in der Richtlinie enthalten ist (Richtlinientyp), und Informationen dazu, ob die Richtlinie zugewiesen ist.

![Übersichtsseite der Antivirenrichtlinie](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Wenn Sie eine Richtlinie aus der Liste auswählen, wird die *Übersichtsseite* für diese Richtlinieninstanz geöffnet, und es werden weitere Informationen angezeigt. Wenn Sie eine Kachel aus dieser Ansicht auswählen, zeigt Intune zusätzliche Details für dieses Profil an, sofern diese verfügbar sind.

![Übersichtsseite der Antivirenrichtlinie](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Fehlerhafte Windows 10-Endpunkte

Auf der Seite **Fehlerhafte Windows 10-Endpunkte** können Sie Informationen zum Antivirenstatus ihrer mit MDM verwalteten Windows 10-Geräte anzeigen. Diese Informationen werden von Windows Defender Antivirus, das auf dem Gerät ausgeführt wird, als *Status des Bedrohungs-Agent* zurückgegeben.

In dieser Ansicht werden nur Geräte mit erkannten Problemen angezeigt. Es werden keine Details für Geräte angezeigt, die als bereinigt identifiziert werden.

![Übersichtsseite der Antivirenrichtlinie](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
