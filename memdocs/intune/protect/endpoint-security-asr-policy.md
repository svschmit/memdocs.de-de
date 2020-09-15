---
title: Verwalten von Einstellungen für die Verringerung der Angriffsfläche mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien für Geräte, die Sie mithilfe von Einstellungen für die Verringerung der Angriffsfläche mit Endpunktsicherheitsrichtlinien in Microsoft Intune verwalten
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/3/2020
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
ms.openlocfilehash: 303acae2eba275907b70fcc52660217568913c62
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432522"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Richtlinie zur Verringerung der Angriffsfläche für Endpunktsicherheit in Intune

Wenn Defender Antivirus auf Ihren Windows 10-Geräten verwendet wird, können Sie Endpunktsicherheitsrichtlinien von Intune für die Verringerung der Angriffsfläche verwenden, um diese Einstellungen für Ihre Geräte zu verwalten.

Mithilfe von Richtlinien zur Verringerung der Angriffsfläche können Sie die Angriffsflächen verringern, indem Sie die Stellen minimieren, an denen Ihre Organisation anfällig für Cyberbedrohungen und Angriffe ist. Weitere Informationen finden Sie unter [Übersicht über die Verringerung der Angriffsfläche]( /windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in der Dokumentation zu Windows Threat Protection.

Die Endpunktsicherheitsrichtlinien für die Verringerung der Angriffsfläche finden Sie unter *Verwalten* im Knoten **Endpunktsicherheit** des [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431). Jedes *Profil* für die Verringerung der Angriffsfläche verwaltet Einstellungen für einen bestimmten Bereich eines Windows 10-Geräts.

Zeigen Sie [Profileinstellungen für die Verringerung der Angriffsfläche](../protect/endpoint-security-asr-profile-settings.md) an.

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Profileinstellungen für die Verringerung der Angriffsfläche

- Windows 10 oder höher
- Defender Antivirus muss die primäre Antivirussoftware auf dem Gerät sein.

## <a name="attack-surface-reduction-profiles"></a>Profile zur Verringerung der Angriffsfläche

**Windows 10-Profile**:

- **App- und Browserisolation**: Verwalten von Einstellungen für Windows Defender Application Guard (Application Guard) als Teil von Defender ATP. Mithilfe von Application Guard können Sie alte und neu aufkommende Angriffe verhindern und vom Unternehmen definierte Websites als nicht vertrauenswürdig isolieren, während Sie definieren, welche Websites, Cloudressourcen und interne Netzwerke vertrauenswürdig sind.

  Weitere Informationen finden Sie unter [Application Guard](/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) in der Dokumentation zu Microsoft Defender ATP.

- **Webschutz**: Einstellungen, die Sie für den Webschutz in Microsoft Defender ATP verwalten können, konfigurieren Netzwerkschutz, um Ihre Computer vor Bedrohungen aus dem Web zu schützen. Durch Integration in Microsoft Edge und beliebte Browser von Drittanbietern wie Chrome und Firefox geht der Webschutz gegen Bedrohungen aus dem Web ohne einen Webproxy vor und kann Computer schützen, wenn Sie remote oder lokal verwendet werden. Der Webschutz beendet den Zugriff auf:
  - Phishingwebsites
  - Malwarevektoren
  - Exploitwebsites
  - Nicht vertrauenswürdige Websites oder Websites, die nur wenig vertrauenswürdig sind
  - Websites, die Sie in Ihrer benutzerdefinierten Indikatorliste blockiert haben.

  Weitere Informationen finden Sie unter [Webschutz](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) in der Dokumentation zu Microsoft Defender ATP.

- **Anwendungssteuerung**: Anwendungssteuerungseinstellungen können dabei helfen, Sicherheitsbedrohungen zu mindern, indem sie die Anwendungen einschränken, die Benutzer ausführen können, sowie den Code, der im Systemkern (Kernel) ausgeführt wird. Verwalten Sie Einstellungen, mit denen nicht signierte Skripts und MSIs blockiert werden können, und schränken Sie die Ausführung von Windows PowerShell auf den Modus mit eingeschränkter Sprache ein.

  Weitere Informationen finden Sie unter [Anwendungssteuerung](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) in der Dokumentation zu Microsoft Defender ATP.
  
    > [!NOTE]
    > Wenn Sie diese Einstellung verwenden, ruft das aktuelle AppLocker-CSP-Verhalten den Endbenutzer dazu auf, seinen Computer neu zu starten, wenn eine Richtlinie bereitgestellt wird.

- **Regeln zur Verringerung der Angriffsfläche**: Konfigurieren Sie Einstellungen für Regeln zur Verringerung der Angriffsfläche, die auf Verhalten abzielen, das Schadsoftware und böswillige Apps üblicherweise zum Infizieren von Computern verwenden, beispielsweise:
  - Ausführbare Dateien und Skripts, die in Office-Apps oder Web-E-Mail zum Herunterladen oder Ausführen von Dateien verwendet werden.
  - Verborgene oder anderweitig verdächtige Skripts.
  - Verhalten, das Apps in der Regel nicht bei der täglichen Arbeit zeigen. Das Verringern der Angriffsfläche bedeutet, dass Angreifern weniger Möglichkeiten zum Durchführen von Angriffen geboten werden.

  Weitere Informationen finden Sie unter [Regeln zum Verringern der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) in der Dokumentation zu Microsoft Defender ATP.

- **Gerätesteuerung**: Mit Einstellungen für die Gerätesteuerung können Sie Geräte für einen mehrstufigen Ansatz zum Sichern von Wechselmedien konfigurieren. Microsoft Defender ATP bietet mehrere Überwachungs- und Steuerungsfeatures, mit denen Sie eine Gefährdung Ihrer Geräte durch Bedrohungen in nicht autorisierten Peripheriegeräten verhindern können.

  Weitere Informationen finden Sie unter [Steuern von USB-Geräten und anderen Wechselmedien mithilfe von Microsoft Defender ATP](/windows/security/threat-protection/device-control/control-usb-devices-using-intune) in der Dokumentation zu Microsoft Defender ATP.

- **Schutz vor Exploits**: Exploit-Schutzeinstellungen können Schutz vor Schadsoftware bieten, die Exploits verwendet, um Geräte zu infizieren und Schadsoftware zu verteilen. Der Exploit-Schutz besteht aus einer Reihe von Entschärfungen, die entweder auf das Betriebssystem oder auf einzelne Apps angewendet werden können.

  Weitere Informationen finden Sie unter [Aktivieren von Schutz vor Exploits](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) in der Dokumentation zu Microsoft Defender ATP.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
