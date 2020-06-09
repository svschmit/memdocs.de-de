---
title: 'Windows 10: Virenschutzrichtlinien-Einstellungen für Microsoft-Sicherheitsfunktionalität für Intune | Microsoft-Dokumentation'
description: Virenschutzrichtlinien-Einstellungen für Endpunktsicherheit für die Windows-Sicherheits-App in Microsoft Intune
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
ms.openlocfilehash: 78cc6182cf8682935ecaa6c319e30ee8261fc2fb
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455258"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Einstellungen für das Windows-Sicherheitsfunktionalitätsprofil in Microsoft Intune

Zeigen Sie die Virenschutzrichtlinien-Einstellungen an, die Sie für das **Windows-Sicherheitsfunktionalitätsprofil** für Windows 10 in Microsoft Intune als Teil einer [Endpunktsicherheitsrichtlinie](../protect/endpoint-security-policy.md) konfigurieren können.

**Windows-Sicherheit**

- **Manipulationsschutz aktivieren, um eine Deaktivierung von Microsoft Defender zu verhindern**  
  [Verhindern von Änderungen an Sicherheitseinstellungen mit Manipulationsschutz](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Nicht konfiguriert** (*Standard*): Wenn auf einem Client der Status *Aktivieren* oder *Deaktivieren* vorhanden ist, hat die Bereitstellung von *Nicht konfiguriert* keinerlei Auswirkung auf die Einstellung. 
  - **Aktivieren**: Aktiviert die Einschränkung „Manipulationsschutz“. Wenn Sie den Status in „Aktiviert“ oder „Deaktiviert“ ändern möchten, stellen Sie die umgekehrte Einstellung bereit, dass diese wirksam wird.
  - **Deaktivieren**: Deaktiviert die Einschränkungen „Manipulationsschutz“. Wenn Sie den Status in „Aktiviert“ oder „Deaktiviert“ ändern möchten, stellen Sie die umgekehrte Einstellung bereit, dass diese wirksam wird.

- **Bereich für Viren- und Bedrohungsschutz in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für Viren- und Bedrohungsschutz in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf Viren- und Bedrohungsschutz beziehen, werden unterdrückt.

  - **Option zur Ransomware-Datenwiederherstellung in der Windows-Sicherheits-App ausblenden**  
    CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für Ransomware-Datenwiederherstellung in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf Ransomware beziehen, werden unterdrückt.

- **Kontoschutzbereich in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für Kontoschutz in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf Kontoschutz beziehen, werden unterdrückt.

- **Bereich für Firewall- und Netzwerkschutz in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für Firewall- Netzwerkschutz in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf Firewall- und Netzwerkschutz beziehen, werden unterdrückt.

- **Bereich zur App- und Browsersteuerung in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich zur App- und Browsersteuerung in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf App- und Browsersteuerung beziehen, werden unterdrückt.

- **Gerätesicherheitsbereich in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für Hardwareschutz in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf Hardwareschutz beziehen, werden unterdrückt.
  
- **Bereich für Geräteleistung und -integrität in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für Geräteleistung und -integrität in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Benachrichtigungen, die sich auf Leistung und Integrität beziehen, werden unterdrückt.

- **Bereich „Familienoptionen“ in der Windows-Sicherheits-App ausblenden**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzerzugriff und Benachrichtigungen sind zulässig.
  - **Ja**: Bereich für „Familienoptionen“ in der Windows-Sicherheits-App ist für Endbenutzer nicht sichtbar. Außerdem werden Benachrichtigungen, die sich auf „Familienoptionen“ beziehen, unterdrückt.

- **Benachrichtigungen der Windows-Sicherheits-App**  
  CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)

  Verwenden Sie diese Einstellung, um Windows-Sicherheitsbenachrichtigungen für alle vorherigen Featureeinstellungen für Ihre Benutzer zu blockieren. Alternativ können Sie die Benachrichtigungen der Windows-Sicherheits-App pro Feature mithilfe der vorherigen Einstellungen verwalten.

  - **Nicht konfiguriert** (*Standard*): Alle Benachrichtigungen der Windows-Sicherheits-App, die nicht von einer anderen Einstellung gesteuert werden, sind zulässig.
  - **Nicht kritische Benachrichtigungen blockieren**: Benachrichtigungen wie Scanabschlüsse werden blockiert.
  - **Alle Benachrichtigungen blockieren**: Kritische und nicht kritische Benachrichtigungen werden für alle Windows-Sicherheitsfeatures blockiert.

- **Windows-Sicherheitssymbol aus dem Infobereich ausblenden**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  Damit diese Einstellung wirksam wird, muss sich der Benutzer entweder abmelden und anmelden oder den Computer neu starten.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. das Symbol wird angezeigt.
  - **Ja**: Windows-Sicherheitssymbol auf der Taskleiste von Benutzern ausblenden.
  
- **Option „TPM löschen“ in der Windows-Sicherheits-App deaktivieren**  
  CSP: [DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. der Zugriff auf die Schaltfläche ist zulässig.
  - **Ja**: Deaktiviert den Zugriff auf die Schaltfläche „TPM löschen“ in der Windows-Sicherheits-App.

- **Benutzer bei Feststellung einer Sicherheitslücke zum Aktualisieren der TPM-Firmware auffordern**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzer erhalten keine Eingabeaufforderung.
  - **Ja**: Windows gestatten, eine Eingabeaufforderung für Endbenutzer anzuzeigen, wenn eine potenzielle Sicherheitslücke in der TPM-Firmware festgestellt wird. Anschließend werden die Benutzer aufgefordert, Firmwareupdates auszuführen, um das Sicherheitsrisiko zu beheben.

- **Kontaktinformationen für den Support der Organisation**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Geben Sie an, wo die IT-Organisationsinformationen in der Windows-Sicherheits-App und in den Benachrichtigungen angezeigt werden sollen.
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **In App und Benachrichtigungen anzeigen**
  - **Nur in App anzeigen**
  - **Nur in Benachrichtigungen anzeigen**
