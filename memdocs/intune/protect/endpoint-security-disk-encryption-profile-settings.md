---
title: Einstellungen der Datenträgerverschlüsselungsrichtlinie für Endpunktsicherheit in Intune | Microsoft-Dokumentation
description: Einstellungen der Datenträgerverschlüsselungsrichtlinie für Endpunktsicherheit für BitLocker und FileVault in Microsoft Intune
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
ms.openlocfilehash: db23ee1742934e8545c03c529d6a05c13cc59f1a
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633281"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Einstellungen der Datenträgerverschlüsselungsrichtlinie für Endpunktsicherheit in Intune

Erfahren Sie, welche Einstellungen Sie in Profilen für die Richtlinie zur *Datenträgerverschlüsselung* im Intune-Knoten „Endpunktsicherheit“ als Teil einer [Endpunktsicherheitsrichtlinie](../protect/endpoint-security-policy.md) konfigurieren können.

Unterstützte Plattformen und Profile:

- **macOS**:
  - Profil: **FileVault**
- **Windows 10 und höher**:
  - Profil: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Verschlüsselung

**FileVault aktivieren**  
- **Nicht konfiguriert** (*Standardeinstellung*)
- **Ja**: Aktivieren der vollständigen Datenträgerverschlüsselung mithilfe von XTS-AES 128 mit FileVault auf Geräten, auf denen macOS 10.13 und höher ausgeführt wird. FileVault wird aktiviert, wenn der Benutzer sich vom Gerät abmeldet.

  Wenn für diese Einstellung *Ja* festgelegt wird, können Sie weitere Einstellungen für FileVault konfigurieren.

  - **Art des Wiederherstellungsschlüssels**
    *Persönlicher Schlüssel*: Für Geräte wird diese Art von Wiederherstellungsschlüssel erstellt. Konfigurieren Sie die folgenden Einstellungen für den persönlichen Schlüssel:

    - **Rotation für persönlichen Wiederherstellungsschlüssel**  
      Geben Sie an, wie häufig der persönliche Wiederherstellungsschlüssel für ein Gerät rotiert werden soll. Sie können die Standardeinstellung **Nicht konfiguriert** oder einen Wert von **1** bis **12** Monaten festlegen.
    - **Beschreibung des Hinterlegungsstandorts für den persönlichen Wiederherstellungsschlüssel**  
      Legen Sie eine kurze Nachricht an den Benutzer fest, die erklärt, wie dieser den persönlichen Wiederherstellungsschlüssel abrufen kann. Diese Meldung wird auf dem Anmeldebildschirm des Benutzers angezeigt, wenn dieser sein Kennwort vergessen hat und zur Eingabe des persönlichen Wiederherstellungsschlüssels aufgefordert wird.

  - **Zulässige Anzahl von Umgehungen**  
    Hiermit wird festgelegt, wie häufig ein Benutzer Aufforderungen zum Aktivieren von FileVault ignorieren kann, bevor FileVault für die Benutzeranmeldung als erforderlich festgelegt wird.
    - **Nicht konfiguriert** (*Standardeinstellung*): Die Verschlüsselung auf dem Gerät ist erforderlich, bevor die nächste Anmeldung zugelassen wird.
    - **1** bis **10**: Benutzern das Ignorieren der Eingabeaufforderung ein- bis zehnmal gestatten, bevor die Verschlüsselung auf dem Gerät erforderlich ist.
    - **Kein Limit, immer auffordern**: Der Benutzer wird aufgefordert, FileVault zu aktivieren, eine Verschlüsselung ist jedoch zu keinem Zeitpunkt erforderlich.

  - **Verzögerung bis zum Abmelden zulassen**  
    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Die Aufforderung zum Aktivieren von FileVault wird verzögert, bis der Benutzer sich abmeldet.  

  - **Aufforderung bei Abmeldung deaktivieren**  
    Mit dieser Option wird verhindert, dass die Aufforderung dem Benutzer bei der Abmeldung angezeigt wird, der die Aktivierung von FileVault anfordert. Wenn diese Option deaktiviert ist, wird die Eingabeaufforderung bei der Abmeldung deaktiviert, und der Benutzer wird stattdessen aufgefordert, wenn er sich anmeldet.
    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Die Aufforderung zum Aktivieren von FileVault beim Abmelden wird deaktiviert.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker – Grundeinstellungen

- **Vollständige Datenträgerverschlüsselung für Betriebssystem- und Festplattenlaufwerke aktivieren**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Wenn das Laufwerk vor Anwendung dieser Richtlinie verschlüsselt wurde, werden keine weiteren Maßnahmen ergriffen. Wenn die Verschlüsselungsmethode und die Optionen mit der Methode und den Optionen dieser Richtlinie übereinstimmen, sollte die Konfiguration erfolgreich sein. Wenn eine direkte BitLocker-Konfigurationsoption nicht dieser Richtlinie entspricht, gibt die Konfiguration wahrscheinlich einen Fehler zurück.
  
  Zur Anwendung dieser Richtlinie auf ein bereits verschlüsseltes Laufwerk entschlüsseln Sie dieses, und wenden Sie die MDM-Richtlinie noch mal an. In der Windows-Standardeinstellung ist keine BitLocker-Laufwerkverschlüsselung erforderlich. Für die Azure AD Join- und MSA-Registrierung/-Anmeldung (Microsoft-Konto) kann jedoch die automatische Verschlüsselung angewendet werden, wobei BitLocker mit der Verschlüsselung „XTS-AES, 128 Bit“ aktiviert wird.

  - **Nicht konfiguriert** (*Standardeinstellung*): BitLocker wird nicht erzwungen.
  - **Ja**: Die Verwendung von BitLocker wird erzwungen.

- **Speicherkarten müssen verschlüsselt sein (nur mobil)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Diese Einstellung gilt nur für Geräte mit den SKUs „Windows Mobile“ und „Mobile Enterprise“.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Betriebssystems zurückgesetzt, d. h. die Verschlüsselung von Speicherkarten ist nicht erforderlich.
  - **Ja**: Die Verschlüsselung von Speicherkarten ist für mobile Geräte erforderlich.

- **Aufforderung zur Drittanbieterverschlüsselung ausblenden**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Wenn BitLocker auf einem System aktiviert ist, das bereits von einer Drittanbieterverschlüsselungslösung verschlüsselt wird, wird das Gerät möglicherweise als unbrauchbar angezeigt. Es kann zu Datenverlust kommen, und möglicherweise müssen Sie Windows neu installieren. Daher wird dringend davon abgeraten, BitLocker auf Geräten zu aktivieren, auf denen eine Drittanbieterverschlüsselungslösung installiert oder aktiviert ist.

  Im BitLocker-Setup-Assistenten werden Benutzer standardmäßig aufgefordert, zu bestätigen, dass keine Drittanbieterverschlüsselungslösung vorhanden ist.

  - **Nicht konfiguriert** (*Standardeinstellung*): Im BitLocker-Setup-Assistenten wird eine Warnung angezeigt, und Benutzer werden aufgefordert, zu bestätigen, dass keine Drittanbieterverschlüsselungslösung vorhanden ist.
  - **Ja**: Die Benutzeraufforderung im BitLocker-Setup-Assistenten wird ausgeblendet.

  Wenn BitLocker-Features zur unbeaufsichtigten Aktivierung benötigt werden, muss die Warnung zu Verschlüsselungsprodukten von Drittanbietern ausgeblendet werden, weil jede Eingabeaufforderung den Workflow einer unbeaufsichtigten Aktivierung unterbricht.

  Bei Festlegung auf *Ja* kann anschließend die folgende Einstellung konfiguriert werden:

  - **Standardbenutzern das Aktivieren der Verschlüsselung während der Autopilot-Ausführung gestatten**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Nicht konfiguriert** (*Standardeinstellung*): In Azure Active Directory Join-Szenarien (AADJ) mit unbeaufsichtigter Aktivierung müssen Benutzer keine lokalen Administratoren sein, um BitLocker zu aktivieren.
    - **Ja**: Die Standardeinstellung des Clients wird beibehalten, sodass lokaler Administratorzugriff erforderlich ist, um BitLocker zu aktivieren.

    In Szenarien mit beaufsichtigter Aktivierung/Autopilot-Szenarien muss der Benutzer ein lokaler Administrator sein, um den BitLocker-Setup-Assistenten abzuschließen.

- **Vom Client gesteuertes Wiederherstellungskennwort aktivieren für**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  AWA-Geräte (Add Work Account, früher Workplace Join) werden bei der Schlüsselrotation nicht unterstützt.
  - **Nicht konfiguriert** (*Standardeinstellung*): Der Client führt keine Rotation für BitLocker-Wiederherstellungsschlüssel durch.
  - **Deaktiviert**
  - **In Azure AD eingebundene Geräte**
  - **In Azure AD und hybrid eingebundene Geräte**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker – Einstellungen für Festplattenlaufwerk

- **BitLocker: Richtlinie für Festplattenlaufwerk**  
  [BitLocker-Gruppenrichtlinieneinstellungen](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Wiederherstellung von Festplattenlaufwerken**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Festlegung, wie mit BitLocker geschützte Festplattenlaufwerke wiederhergestellt werden, wenn die erforderlichen Informationen zum Startschlüssel nicht vorhanden sind.

    - **Nicht konfiguriert** (*Standardeinstellung*): Die standardmäßigen Wiederherstellungsoptionen werden unterstützt, einschließlich Datenwiederherstellungs-Agent. Der Endbenutzer kann Wiederherstellungsoptionen angeben, und die Wiederherstellungsinformationen werden nicht in Azure Active Directory gesichert.
    - **Konfigurieren**: Aktivieren des Zugriffs, um verschiedene Verfahren zur Laufwerkwiederherstellung zu konfigurieren.

    Wenn diese Einstellung auf *Konfigurieren* festgelegt wird, sind die folgenden Einstellungen verfügbar:

    - **Erstellung des Wiederherstellungsschlüssels durch den Benutzer**  
      - **Blockiert** (*Standardeinstellung*)
      - **Erforderlich**
      - **Zulässig**

    - **BitLocker-Wiederherstellungspaket konfigurieren**
      - **Kennwort und Schlüssel** (*Standardeinstellung*): Sowohl das BitLocker-Wiederherstellungskennwort, das von Administratoren und Benutzern zum Entsperren der geschützten Laufwerke verwendet wird, als auch die Wiederherstellungsschlüsselpakete, die von Administratoren für die Datenwiederherstellung in Active Directory verwendet werden, werden eingefügt.
      - **Nur Kennwort**: Auf die Wiederherstellungsschlüsselpakete kann möglicherweise nicht zugegriffen werden, wenn sie benötigt werden.

    - **Gerät muss Wiederherstellungsinformationen in Azure AD sichern**
      - **Nicht konfiguriert** (*Standardeinstellung*): BitLocker wird auch dann aktiviert, wenn bei der Sicherung des Wiederherstellungsschlüssels in Azure AD ein Fehler auftritt. Dies kann zur Folge haben, dass extern keine Wiederherstellungsinformationen gespeichert werden.
      - **Ja**: Die Aktivierung von BitLocker wird erst dann abgeschlossen, wenn Wiederherstellungsschlüssel erfolgreich in Azure Active Directory gespeichert wurden.

    - **Erstellung des Wiederherstellungskennworts durch den Benutzer**  
      - **Blockiert** (*Standardeinstellung*)
      - **Erforderlich**
      - **Zulässig**

    - **Wiederherstellungsoptionen während der BitLocker-Einrichtung ausblenden**
      - **Nicht konfiguriert** (*Standardeinstellung*): Der Benutzer kann auf zusätzliche Wiederherstellungsoptionen zugreifen.
      - **Ja**: Der Endbenutzer kann keine zusätzlichen Wiederherstellungsoptionen auswählen (z. B. das Drucken von Wiederherstellungsschlüsseln, während der BitLocker-Setup-Assistent ausgeführt wird).

    - **BitLocker nach Speicherung der Wiederherstellungsinformationen im Speicher aktivieren**
      - **Nicht konfiguriert** (*Standardeinstellung*)  
      - **Ja**

    - **Verwendung des zertifikatbasierten Datenwiederherstellungs-Agents (DRA) blockieren**
      - **Nicht konfiguriert** (*Standardeinstellung*): Die Verwendung von DRA kann eingerichtet werden. Für die Einrichtung von DRA sind Unternehmens-PKI und Gruppenrichtlinienobjekte zum Bereitstellen des DRA-Agents und der Zertifikate erforderlich.
      - **Ja**: Es ist nicht möglich, den Datenwiederherstellungs-Agent für die Wiederherstellung von Laufwerken, für die BitLocker aktiviert ist, zu verwenden.

  - **Schreibzugriff auf Festplattenlaufwerke ohne BitLocker-Schutz blockieren**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Diese Einstellung ist verfügbar, wenn *BitLocker: Richtlinie für Festplattenlaufwerk* auf *Konfigurieren* festgelegt ist.

    - **Nicht konfiguriert** (*Standardeinstellung*): Daten können auf nicht verschlüsselte Festplattenlaufwerke geschrieben werden.
    - **Ja**: Windows lässt nicht zu, dass Daten auf Festplattenlaufwerke geschrieben werden, die nicht durch BitLocker geschützt sind. Wenn ein Festplattenlaufwerk nicht verschlüsselt ist, muss der Benutzer den BitLocker-Setup-Assistenten für das Laufwerk ausführen, bevor er Schreibzugriff erhält.

  - **Verschlüsselungsmethode für Festplattenlaufwerke konfigurieren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Konfigurieren Sie die Verschlüsselungsmethode und Verschlüsselungsstärke für Festplattenlaufwerke. *XTS-AES, 128 Bit* ist die Standardverschlüsselungsmethode von Windows und der empfohlene Wert.

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **AES-CBC, 128 Bit**
    - **AES-CBC, 256 Bit**
    - **AES-XTS, 128 Bit**
    - **AES-XTS, 256 Bit**

### <a name="bitlocker---os-drive-settings"></a>BitLocker – Einstellungen für Betriebssystemlaufwerke

- **BitLocker: Richtlinie für Systemlaufwerk**  
  CSP: [BitLocker-Gruppenrichtlinieneinstellungen](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Konfigurieren** (*Standardeinstellung*)  
  - **Nicht konfiguriert**

  Bei Festlegung auf *Konfigurieren* können die folgenden Einstellungen konfiguriert werden:

  - **Startauthentifizierung erforderlich**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Konfigurieren der zusätzlichen Authentifizierungsanforderungen beim Systemstart. Dazu zählen u. a. die Verwendung von TPM oder Start-PIN-Anforderungen.

    Bei Festlegung auf *Ja* können die folgenden Einstellungen konfiguriert werden:

    - **Systemstart für kompatibles TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Es wird empfohlen, ein TPM für BitLocker als erforderlich festzulegen. Diese Einstellung gilt nur für die erstmalige Aktivierung von BitLocker. Sie hat keine Auswirkungen, wenn BitLocker bereits aktiviert ist.

      - **Blockiert** (*Standardeinstellung*): BitLocker verwendet das TPM nicht.
      - **Erforderlich**: BitLocker wird nur aktiviert, wenn ein TPM vorhanden ist und verwendet werden kann.
      - **Zulässig**: BitLocker verwendet das TPM, wenn es vorhanden ist.

    - **Systemstart-PIN für kompatibles TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blockiert** (*Standardeinstellung*): Die Verwendung einer PIN wird blockiert.
      - **Erforderlich**: Für die Aktivierung von BitLocker müssen eine PIN und ein TPM vorhanden sein.
      - **Zulässig**: BitLocker verwendet das TPM, wenn es vorhanden ist und die Konfiguration einer Start-PIN durch den Benutzer zulässig ist.

      Für Szenarien mit automatischer Aktivierung muss diese Einstellung auf *Blockiert* festgelegt werden. Wenn eine Benutzerinteraktion erforderlich ist, treten in Szenarien mit automatischer Aktivierung (einschließlich Autopilot-Szenarien) Fehler auf.

    - **Systemstartschlüssel für kompatibles TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blockiert** (*Standardeinstellung*): Die Verwendung von Systemstartschlüsseln wird blockiert.
      - **Erforderlich**: Für die Aktivierung von BitLocker müssen ein Systemstartschlüssel und ein TPM vorhanden sein.
      - **Zulässig**: BitLocker verwendet das TPM, wenn es vorhanden ist und ein Systemstartschlüssel (z. B. ein USB-Laufwerk) zum Entsperren der Laufwerke vorhanden sein darf.

      Für Szenarien mit automatischer Aktivierung muss diese Einstellung auf *Blockiert* festgelegt werden. Wenn eine Benutzerinteraktion erforderlich ist, treten in Szenarien mit automatischer Aktivierung (einschließlich Autopilot-Szenarien) Fehler auf.

    - **Systemstartschlüssel und -PIN für kompatibles TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blockiert** (*Standardeinstellung*): Die Verwendung einer Kombination aus Systemstartschlüssel und PIN wird blockiert.
      - **Erforderlich**: Für die Aktivierung von BitLocker müssen ein Systemstartschlüssel und eine PIN vorhanden sein.
      - **Zulässig**: BitLocker verwendet das TPM, wenn es vorhanden und eine Kombination aus Systemstartschlüssel und PIN zulässig ist.

      Für Szenarien mit automatischer Aktivierung muss diese Einstellung auf *Blockiert* festgelegt werden. Wenn eine Benutzerinteraktion erforderlich ist, treten in Szenarien mit automatischer Aktivierung (einschließlich Autopilot-Szenarien) Fehler auf.

    - **BitLocker auf Geräten mit inkompatiblem TPM deaktivieren**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Wenn kein TPM vorhanden ist, benötigt BitLocker für den Systemstart ein Kennwort oder ein USB-Laufwerk.

      Diese Einstellung gilt nur für die erstmalige Aktivierung von BitLocker. Sie hat keine Auswirkungen, wenn BitLocker bereits aktiviert ist.

      - **Nicht konfiguriert** (*Standardeinstellung*)
      - **Ja**: BitLocker kann nur mit kompatiblem TPM-Chip konfiguriert werden.

    - **Pre-Boot-Wiederherstellungsmeldung und -URL aktivieren**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **Nicht konfiguriert** (*Standardeinstellung*): Verwendung der standardmäßigen Pre-Boot-Wiederherstellungsinformationen von BitLocker.
      - **Ja**: Ermöglicht die Konfiguration einer benutzerdefinierten Pre-Boot-Wiederherstellungsmeldung und URL, damit Benutzer besser verstehen, wie sie ihr Wiederherstellungskennwort finden. Die Pre-Boot-Meldung und URL werden Benutzern angezeigt, wenn der Zugriff dieser Benutzer auf ihrem PC im Wiederherstellungsmodus gesperrt ist.

      Bei Festlegung auf *Ja* können die folgenden Einstellungen konfiguriert werden:

      - **Meldung für Pre-Boot-Wiederherstellung**  
        Geben Sie eine benutzerdefinierte Pre-Boot-Wiederherstellungsmeldung an.

      - **URL für Pre-Boot-Wiederherstellung**  
        Geben Sie eine benutzerdefinierte URL für die Pre-Boot-Wiederherstellung an.

    - **Wiederherstellung des Systemlaufwerks**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Nicht konfiguriert** (*Standardeinstellung*)  
      - **Konfigurieren**: Ermöglicht die Konfiguration zusätzlicher Einstellungen.

      Wenn diese Einstellung auf *Konfigurieren* festgelegt wird, sind die folgenden Einstellungen verfügbar:

      - **Erstellung des Wiederherstellungsschlüssels durch den Benutzer**  
        - **Blockiert** (*Standardeinstellung*)
        - **Erforderlich**
        - **Zulässig**

      - **BitLocker-Wiederherstellungspaket konfigurieren**
        - **Kennwort und Schlüssel** (*Standardeinstellung*): Sowohl das BitLocker-Wiederherstellungskennwort, das von Administratoren und Benutzern zum Entsperren der geschützten Laufwerke verwendet wird, als auch die Wiederherstellungsschlüsselpakete, die von Administratoren für die Datenwiederherstellung in Active Directory verwendet werden, werden eingefügt.
        - **Nur Kennwort**: Auf die Wiederherstellungsschlüsselpakete kann möglicherweise nicht zugegriffen werden, wenn sie benötigt werden.

      - **Gerät muss Wiederherstellungsinformationen in Azure AD sichern**
        - **Nicht konfiguriert** (*Standardeinstellung*): BitLocker wird auch dann aktiviert, wenn bei der Sicherung des Wiederherstellungsschlüssels in Azure AD ein Fehler auftritt. Dies kann zur Folge haben, dass extern keine Wiederherstellungsinformationen gespeichert werden.
        - **Ja**: Die Aktivierung von BitLocker wird erst dann abgeschlossen, wenn Wiederherstellungsschlüssel erfolgreich in Azure Active Directory gespeichert wurden.

      - **Erstellung des Wiederherstellungskennworts durch den Benutzer**  
        - **Blockiert** (*Standardeinstellung*)
        - **Erforderlich**
        - **Zulässig**

      - **Wiederherstellungsoptionen während der BitLocker-Einrichtung ausblenden**
        - **Nicht konfiguriert** (*Standardeinstellung*): Der Benutzer kann auf zusätzliche Wiederherstellungsoptionen zugreifen.
        - **Ja**: Der Endbenutzer kann keine zusätzlichen Wiederherstellungsoptionen auswählen (z. B. das Drucken von Wiederherstellungsschlüsseln, während der BitLocker-Setup-Assistent ausgeführt wird).

      - **BitLocker nach Speicherung der Wiederherstellungsinformationen im Speicher aktivieren**
        - **Nicht konfiguriert** (*Standardeinstellung*)  
        - **Ja**

      - **Verwendung des zertifikatbasierten Datenwiederherstellungs-Agents (DRA) blockieren**
        - **Nicht konfiguriert** (*Standardeinstellung*): Die Verwendung von DRA kann eingerichtet werden. Für die Einrichtung von DRA sind Unternehmens-PKI und Gruppenrichtlinienobjekte zum Bereitstellen des DRA-Agents und der Zertifikate erforderlich.
        - **Ja**: Es ist nicht möglich, den Datenwiederherstellungs-Agent für die Wiederherstellung von Laufwerken, für die BitLocker aktiviert ist, zu verwenden.

    - **PIN-Mindestlänge**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Geben Sie die Mindestlänge der Systemstart-PIN ein, wenn TPM und PIN während der BitLocker-Aktivierung erforderlich sind. Die PIN-Länge muss zwischen 4 und 20 Zeichen betragen.

      Wenn Sie diese Einstellung nicht konfigurieren, können Benutzer eine Systemstart-PIN mit beliebiger Länge (zwischen 4 und 20 Ziffern) konfigurieren

      Diese Einstellung gilt nur für die erstmalige Aktivierung von BitLocker. Sie hat keine Auswirkungen, wenn BitLocker bereits aktiviert ist.

  - **Verschlüsselungsmethode für Betriebssystemlaufwerke konfigurieren**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Konfigurieren Sie die Verschlüsselungsmethode und Verschlüsselungsstärke für Betriebssystemlaufwerke. *XTS-AES, 128 Bit* ist die Standardverschlüsselungsmethode von Windows und der empfohlene Wert.

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **AES-CBC, 128 Bit**
    - **AES-CBC, 256 Bit**
    - **AES-XTS, 128 Bit**
    - **AES-XTS, 256 Bit**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker – Einstellungen für Wechseldatenträger

- **Verschlüsselungsmethode für Betriebssystemlaufwerke konfigurieren**  
  CSP: [BitLocker-Gruppenrichtlinieneinstellungen](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Nicht konfiguriert** (*Standardeinstellung*)  
  - **Konfigurieren Sie**

  Bei Festlegung auf *Konfigurieren* können die folgenden Einstellungen konfiguriert werden.

  - **Configure encryption method for removable data-drives** (Verschlüsselungsmethode für Wechseldatenträger konfigurieren)  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Wählen Sie die gewünschte Verschlüsselungsmethode für Wechseldatenträger aus.

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **AES-CBC, 128 Bit**
    - **AES-CBC, 256 Bit**
    - **AES-XTS, 128 Bit**
    - **AES-XTS, 256 Bit**

  - **Schreibzugriff auf Wechseldatenträger ohne BitLocker-Schutz blockieren**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Nicht konfiguriert** (*Standardeinstellung*): Daten können auf nicht verschlüsselte Laufwerke von Wechseldatenträgern geschrieben werden.
    - **Ja**: Windows lässt nicht zu, dass Daten auf Wechseldatenträger geschrieben werden, die nicht durch BitLocker geschützt sind. Wenn ein Wechseldatenträger nicht verschlüsselt ist, muss der Benutzer den BitLocker-Setup-Assistenten ausführen, bevor er Schreibzugriff auf das Laufwerk erhält.

    - **Schreibzugriff auf Wechseldatenträger ohne BitLocker-Schutz blockieren**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Nicht konfiguriert** (*Standardeinstellung*): Jedes mit BitLocker verschlüsseltes Laufwerk kann verwendet werden.
      - **Ja**: Der Zugriff auf Wechseldatenträger ist nur dann möglich, wenn diese auf einem Computer verschlüsselt wurden, deren Eigentümer Ihre Organisation ist.

## <a name="next-steps"></a>Nächste Schritte

[Endpunktsicherheitsrichtlinie für die Datenträgerverschlüsselung](../protect/endpoint-security-disk-encryption-policy.md)
