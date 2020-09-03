---
title: Referenz zu BitLocker-Einstellungen
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu allen in Configuration Manager verfügbaren Einstellungen für die BitLocker-Verwaltung.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b52fe5a60899d7e871381d1a34a2360bbe68a36c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820475"
---
# <a name="bitlocker-settings-reference"></a>Referenz zu BitLocker-Einstellungen

*Gilt für: Configuration Manager (Current Branch)*

<!-- 5925683 -->

Die BitLocker-Verwaltungsrichtlinien in Configuration Manager umfassen die folgenden Richtliniengruppen:

- Einrichten
- Betriebssystemlaufwerk
- Festplattenlaufwerk
- Wechseldatenträger
- Clientverwaltung

In den folgenden Abschnitten werden Konfigurationen für die Einstellungen in den einzelnen Gruppen beschrieben und Konfigurationsempfehlungen abgegeben.

> [!NOTE]
> Diese Einstellungen beziehen sich auf Version 2002 von Configuration Manager. In Version 1910 sind nicht alle hier beschriebenen Einstellungen enthalten.

## <a name="setup"></a>Einrichten

Mit den Einstellungen auf dieser Seite können Sie globale BitLocker-Verschlüsselungsoptionen konfigurieren.

### <a name="drive-encryption-method-and-cipher-strength"></a>Verschlüsselungsmethode und Verschlüsselungsstärke für Laufwerk

*Empfohlene Konfiguration*: **Aktiviert**, mindestens mit der Standardverschlüsselungsmethode.

> [!NOTE]
> Die **Setup**-Eigenschaftenseite enthält zwei Gruppen von Einstellungen für unterschiedliche Windows-Versionen. In diesem Abschnitt werden die Einstellungen für beide Gruppen beschrieben.

#### <a name="windows-81-devices"></a>Windows 8.1-Geräte

Aktivieren Sie für Windows 8.1-Geräte die Option **Verschlüsselungsmethode und Verschlüsselungsstärke für Laufwerk**, und wählen Sie eine der folgenden Verschlüsselungsmethoden aus:

- AES, 128 Bit, mit Diffusor
- AES, 256 Bit, mit Diffusor
- AES, 128 Bit (Standard)
- AES 256-Bit

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMBLEncryptionMethodPolicy](/powershell/module/configurationmanager/new-cmblencryptionmethodpolicy?view=sccm-ps).

#### <a name="windows-10-devices"></a>Windows 10-Geräte

Aktivieren Sie für Windows 10-Geräte die Option für die **Verschlüsselungsmethode und die Verschlüsselungsstärke für Laufwerke (Windows 10)** . Wählen Sie anschließend jeweils eine der folgenden Verschlüsselungsmethoden für Betriebssystemlaufwerke, Festplattenlaufwerke und Wechseldatenträger aus:

- AES-CBC 128 Bit
- AES-CBC 256 Bit
- XTS-AES, 128 Bit (Standard)
- XTS-AES, 256 Bit

> [!TIP]
> In BitLocker wird der erweiterte Verschlüsselungsstandard (Advanced Encryption Standard, AES) als Verschlüsselungsalgorithmus mit konfigurierbaren Schlüssellängen von 128 oder 256 Bit verwendet. Auf Windows 10-Geräten unterstützt AES die Verschlüsselung im CBC- (Cipher Block Chaining) oder XTS-Modus (Ciphertext Stealing).
>
> Wenn Sie auf einem Gerät, auf dem nicht Windows 10 ausgeführt wird, einen Wechseldatenträger verwenden möchten, wählen Sie dafür AES-CBC aus.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMBLEncryptionMethodWithXts](/powershell/module/configurationmanager/new-cmblencryptionmethodwithxts?view=sccm-ps).

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Allgemeine Hinweise zur Laufwerkverschlüsselung und Verschlüsselungsstärke

- Wenn Sie diese Einstellungen deaktivieren oder nicht konfigurieren, verwendet BitLocker die Standardverschlüsselungsmethode.

- Configuration Manager wendet diese Einstellungen an, wenn Sie BitLocker aktivieren.

- Ist das Laufwerk bereits verschlüsselt oder wird es gerade ausgeführt, wird durch eine Änderung der Richtlinieneinstellungen die Laufwerkverschlüsselung auf dem Gerät nicht geändert.

- Bei Verwendung des Standardwerts wird die Verschlüsselungsstärke im BitLocker-Computerkonformitätsbericht möglicherweise als **unbekannt** angezeigt. Sie können dieses Problem umgehen, indem Sie die Einstellung aktivieren und einen expliziten Wert für die Verschlüsselungsstärke festlegen.

### <a name="prevent-memory-overwrite-on-restart"></a>Überschreiben des Arbeitsspeichers beim Neustart verhindern

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Konfigurieren Sie diese Richtlinie, um die Leistung beim Neustart zu erhöhen, indem geheime BitLocker-Informationen im Arbeitsspeicher beim Neustart nicht überschrieben werden.

Wird diese Richtlinie nicht konfiguriert, entfernt BitLocker beim Neustart des Computers die Geheimnisse aus dem Arbeitsspeicher.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMNoOverwritePolicy](/powershell/module/configurationmanager/new-cmnooverwritepolicy?view=sccm-ps).

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Einhaltung der Regel zur Smartcard-Zertifikatverwendung überprüfen

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Konfigurieren Sie diese Richtlinie, um den BitLocker-Schutz mit Smartcard-Zertifikat zu verwenden. Geben Sie anschließend das Zertifikat **Objektbezeichner** an.

Wird diese Richtlinie nicht konfiguriert, verwendet BitLocker den Standardobjektbezeichner `1.3.6.1.4.1.311.67.1.1`, um ein Zertifikat anzugeben.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMScCompliancePolicy](/powershell/module/configurationmanager/new-cmsccompliancepolicy?view=sccm-ps).

### <a name="organization-unique-identifiers"></a>Eindeutige Organisationsbezeichner

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Konfigurieren Sie diese Richtlinie, um einen zertifikatbasierten Datenwiederherstellungs-Agent oder das BitLocker To Go-Lesetool zu verwenden.

Wird diese Richtlinie nicht konfiguriert, verwendet BitLocker das Feld **Identifikation** nicht.

Sind für Ihre Organisation höhere Sicherheitsmaßnahmen erforderlich, konfigurieren Sie das Feld **Identifikation**. Legen Sie dieses Feld auf allen USB-Zielgeräten fest, und geben Sie für diese Einstellung einen übereinstimmenden Wert an.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMUidPolicy](/powershell/module/configurationmanager/new-cmuidpolicy?view=sccm-ps).

## <a name="os-drive"></a>Betriebssystemlaufwerk

Mit den Einstellungen auf dieser Seite werden die Verschlüsselungseinstellungen für das Laufwerk konfiguriert, auf dem Windows installiert ist.

### <a name="operating-system-drive-encryption-settings"></a>Einstellungen für die Verschlüsselung des Betriebssystemlaufwerks

*Empfohlene Konfiguration*: **Enabled**

Wenn Sie diese Einstellung aktivieren, muss der Benutzer das Betriebssystemlaufwerk schützen, und BitLocker verschlüsselt das Laufwerk. Wenn Sie sie deaktivieren, kann der Benutzer das Laufwerk nicht schützen. Wenn Sie diese Richtlinie nicht konfigurieren, wird BitLocker-Schutz auf dem Betriebssystemlaufwerk nicht angefordert.

> [!NOTE]
> Wenn das Laufwerk bereits verschlüsselt ist und Sie diese Einstellung deaktivieren, entschlüsselt BitLocker das Laufwerk.  

Verwenden Sie bei Geräten ohne [Trusted Platform Module (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-top-node) die Option **BitLocker ohne kompatibles TPM zulassen (Kennwort erforderlich)** . Mit dieser Einstellung kann BitLocker das Betriebssystemlaufwerk auch dann verschlüsseln, wenn das Gerät über kein TPM verfügt. Wenn Sie diese Option zulassen, wird der Benutzer von Windows aufgefordert, ein BitLocker-Kennwort anzugeben.

Auf Geräten mit kompatiblem TPM können zwei Typen von Authentifizierungsmethoden beim Systemstart verwendet werden, um verschlüsselte Daten zusätzlich zu schützen. Beim Starten des Computers kann nur das TPM zur Authentifizierung verwendet werden, oder es kann zusätzlich die Eingabe einer persönlichen Identifikationsnummer (PIN) angefordert werden. Konfigurieren Sie die folgenden Einstellungen:

- **Select protector for operating system drive** (Schutzkomponente für Betriebssystemlaufwerk auswählen): Wählen Sie aus, ob TPM und PIN oder nur TPM verwendet werden soll.

- **Minimale PIN-Länge für Systemstart konfigurieren**: Wenn Sie eine PIN anfordern, ist dieser Wert die kürzeste Länge, die der Benutzer angeben kann. Der Benutzer gibt diese PIN ein, wenn der Computer hochfährt, um das Laufwerk zu entsperren. Die Standardeinstellung für die minimale PIN-Länge ist `4`.

> [!TIP]
> Bei Geräten mit aktivierter TPM- und PIN-Schutzvorrichtung sollten Sie aus Sicherheitsgründen erwägen, die folgenden Gruppenrichtlinieneinstellungen unter **System** > **Energieverwaltung** > **Energiesparmoduseinstellungen** zu *deaktivieren*:
>
> - Verschiedene Statusoptionen (S1-S3) beim Wechsel in den Energiesparmodus zulassen (Netzbetrieb)
>
> - Verschiedene Statusoptionen (S1-S3) beim Wechsel in den Energiesparmodus zulassen (Akkubetrieb)

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMBMSOSDEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsosdencryptionpolicy?view=sccm-ps).

### <a name="allow-enhanced-pins-for-startup"></a>Erweiterte PINs für Systemstart zulassen

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Konfigurieren Sie BitLocker so, dass erweiterte Systemstart-PINs zulässig sind. Mit diesen PINs ist die Verwendung zusätzlicher Zeichen wie z. B. Groß- und Kleinbuchstaben, Symbole, Zahlen und Leerzeichen zulässig. Diese Einstellung wird angewendet, wenn Sie BitLocker aktivieren.

> [!IMPORTANT]
> Nicht alle Computer unterstützen erweiterte PINs in der Pre-Boot-Umgebung. Bevor Sie deren Verwendung aktivieren, sollten Sie die Kompatibilität Ihrer Geräte mit diesem Feature überprüfen.

Wenn Sie diese Einstellung aktivieren, kann der Benutzer bei allen neu festgelegten BitLocker-Systemstart-PINs erweiterte PINs erstellen.

- **Nur aus ASCII-Zeichen bestehende PINs anfordern**: Dadurch erhöht sich die Kompatibilität erweiterter PINs mit Computern, die Art und Anzahl der Zeichen begrenzen, die in der Pre-Boot-Umgebung eingegeben werden können.

Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, verwendet BitLocker keine erweiterten PINs.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMEnhancedPIN](/powershell/module/configurationmanager/new-cmenhancedpin?view=sccm-ps).

### <a name="operating-system-drive-password-policy"></a>Kennwortrichtlinie für Betriebssystemlaufwerk

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Mit diesen Einstellungen legen Sie die Einschränkungen für Kennwörter fest, die zum Entsperren von Betriebssystemlaufwerken mit BitLocker-Schutz verwendet werden. Wenn Sie für Betriebssystemlaufwerke Schutzvorrichtungen ohne TPM zulassen, konfigurieren Sie die folgenden Einstellungen:

- **Kennwortkomplexität für Betriebssystemlaufwerke konfigurieren**: Wenn Sie Anforderungen für die Komplexität eines Kennworts erzwingen möchten, klicken Sie auf **Kennwortkomplexität anfordern**.

- **Minimale Kennwortlänge für Betriebssystemlaufwerk**: Die Standardeinstellung für die minimale Kennwortlänge ist `8`.

- **Nur ASCII-Kennwörter für Betriebssystem-Wechseldatenträger anfordern**

Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer ein Kennwort konfigurieren, das den von Ihnen definierten Anforderungen entspricht.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMOSPassphrase](/powershell/module/configurationmanager/new-cmospassphrase?view=sccm-ps).

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Allgemeine Hinweise zur Kennwortrichtlinie für Betriebssystemlaufwerke

- Damit die festgelegten Einstellungen für die Komplexitätsanforderungen wirksam werden, aktivieren Sie auch die Gruppenrichtlinieneinstellung **Kennwort muss Komplexitätsanforderungen erfüllen** unter **Computerkonfiguration** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Kontorichtlinien** > **Kennwortrichtlinie**.

- Diese Einstellungen werden beim Aktivieren von BitLocker erzwungen, nicht beim Entsperren eines Volumes. Mit BitLocker können Sie ein Laufwerk mit einer der auf dem Laufwerk verfügbaren Schutzvorrichtungen entschlüsseln.

- Wenn Sie eine Gruppenrichtlinie verwenden, um FIPS-konforme Algorithmen für Verschlüsselung, Hashing und Signatur zu aktivieren, sind Kennwörter als BitLocker-Schutzvorrichtung nicht zulässig.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Plattformvalidierungsdaten nach BitLocker-Wiederherstellung zurücksetzen

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Hiermit steuern Sie, ob Windows Daten für die Plattformvalidierung aktualisiert, wenn es nach der BitLocker-Wiederherstellung gestartet wird.

Wird diese Einstellung aktiviert oder nicht konfiguriert, aktualisiert Windows in diesem Fall die Daten für die Plattformvalidierung.

Wenn Sie diese Richtlinieneinstellung deaktivieren, werden die Daten für die Plattformvalidierung von Windows in diesem Fall nicht aktualisiert.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMTpmAutoResealPolicy](/powershell/module/configurationmanager/new-cmtpmautoresealpolicy?view=sccm-ps).

### <a name="pre-boot-recovery-message-and-url"></a>Pre-Boot-Wiederherstellungsmeldung und -URL

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Mit dieser Einstellung können Sie bei einer Sperrung des Betriebssystemlaufwerks durch BitLocker auf dem Pre-Boot-BitLocker-Wiederherstellungsbildschirm eine benutzerdefinierte Wiederherstellungsmeldung oder -URL anzeigen. Diese Einstellung gilt nur für Windows 10-Geräte.

Wenn Sie diese Einstellung aktivieren, wählen Sie für die Pre-Boot-Wiederherstellungsmeldung eine der folgenden Optionen aus:

- **Standard-Wiederherstellungsmeldung und -URL verwenden**: Auf dem Pre-Boot-BitLocker-Wiederherstellungsbildschirm werden die Standard-BitLocker-Wiederherstellungsmeldung und -URL angezeigt. Wenn Sie zuvor eine benutzerdefinierte Wiederherstellungsmeldung oder -URL konfiguriert haben, können Sie mit dieser Option die Standardmeldung wiederherstellen.

- **Benutzerdefinierte Wiederherstellungsmeldung verwenden**: Fügen Sie dem Pre-Boot-BitLocker-Wiederherstellungsbildschirm eine benutzerdefinierte Meldung hinzu.

  - **Option für benutzerdefinierte Wiederherstellungsmeldung**: Geben Sie die benutzerdefinierte Meldung ein, die angezeigt werden soll. Wenn Sie auch eine Wiederherstellungs-URL angeben möchten, fügen Sie diese als Teil der benutzerdefinierten Wiederherstellungsmeldung hinzu. Die maximale Zeichenfolgenlänge beträgt 32.768 Zeichen.

- **Benutzerdefinierte Wiederherstellungs-URL verwenden**: Hiermit wird die Standard-URL ersetzt, die auf dem Pre-Boot-BitLocker-Wiederherstellungsbildschirm angezeigt wird.

  - **Option für benutzerdefinierte Wiederherstellungs-URL**: Geben Sie die URL ein, die angezeigt werden soll. Die maximale Zeichenfolgenlänge beträgt 32.768 Zeichen.

> [!NOTE]
> In der Pre-Boot-Meldung werden nicht alle Zeichen und Sprachen unterstützt. Testen Sie die benutzerdefinierte Meldung oder URL vorab, um sicherzustellen, dass sie auf dem Pre-Boot-BitLocker-Wiederherstellungsbildschirm korrekt angezeigt wird.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMPrebootRecoveryInfo](/powershell/module/configurationmanager/new-cmprebootrecoveryinfo?view=sccm-ps).

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Einstellungen für die Erzwingung von Verschlüsselungsrichtlinien (Betriebssystemlaufwerk)

*Empfohlene Konfiguration*: **Enabled**

Konfigurieren Sie die Anzahl der Tage, die Benutzer die BitLocker-Konformität für das Betriebssystemlaufwerk verschieben können. Die **Karenzzeit für Nichtkonformität** beginnt zu dem Zeitpunkt, wenn Configuration Manager die Nichtkonformität das erste Mal feststellt. Nach Ablauf der Karenzzeit können Benutzer die erforderliche Aktion weder verschieben noch eine Ausnahme davon anfordern.

Ist für den Verschlüsselungsprozess eine Benutzereingabe erforderlich, wird in Windows ein Dialogfeld angezeigt, das erst nach Eingabe der erforderlichen Informationen geschlossen werden kann. Zukünftige Fehler- oder Statusbenachrichtigungen weisen diese Einschränkung nicht auf.

Ist für das Hinzufügen einer Schutzvorrichtung durch BitLocker keine Benutzerinteraktion erforderlich, startet BitLocker nach Ablauf der Karenzzeit die Verschlüsselung im Hintergrund.

Wird diese Einstellung deaktiviert oder nicht konfiguriert, fordert Configuration Manager die Benutzer nicht zur Einhaltung von BitLocker-Richtlinien auf.

Wenn Sie die Richtlinie sofort erzwingen möchten, legen Sie die Karenzzeit auf `0` fest.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMUseOsEnforcePolicy](/powershell/module/configurationmanager/new-cmuseosenforcepolicy?view=sccm-ps).

## <a name="fixed-drive"></a>Festplattenlaufwerk

Mit den Einstellungen auf dieser Seite wird die Verschlüsselung für zusätzliche Laufwerke eines Geräts konfiguriert.

### <a name="fixed-data-drive-encryption"></a>Verschlüsselung für Festplattenlaufwerke

*Empfohlene Konfiguration*: **Enabled**

Hiermit verwalten Sie die Verschlüsselungsanforderung für Festplattenlaufwerke. Wenn Sie diese Einstellung aktivieren, fordert BitLocker den Schutz aller Festplattenlaufwerke an. Anschließend werden die Laufwerke von BitLocker verschlüsselt.

Wenn Sie diese Richtlinie aktivieren, aktivieren Sie entweder die automatische Entsperrung oder die Einstellungen für eine **Kennwortrichtlinie für Festplattenlaufwerke**.

- **Configure auto-unlock for fixed data drive** (Automatische Entsperrung für Festplattenlaufwerk konfigurieren): Hiermit wird BitLocker das automatische Entsperren aller verschlüsselter Laufwerke gestattet oder vorgegeben. Für die automatische Entsperrung ist es auch erforderlich, dass BitLocker das [Betriebssystemlaufwerk](#os-drive) verschlüsselt.

Wenn Sie diese Einstellung nicht konfigurieren, fordert BitLocker keinen Schutz für Festplattenlaufwerke an.

Wenn Sie diese Einstellung deaktivieren, können Benutzer ihre Festplattenlaufwerke nicht unter BitLocker-Schutz stellen. Wenn Sie diese Richtlinie nach der Verschlüsselung der Festplattenlaufwerke durch BitLocker deaktivieren, entschlüsselt BitLocker die Festplattenlaufwerke.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMBMSFDVEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsfdvencryptionpolicy?view=sccm-ps).

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Schreibzugriff auf Festplattenlaufwerke verweigern, die nicht durch BitLocker geschützt sind

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Hiermit ist zum Schreiben von Daten auf Festplattenlaufwerke des Geräts BitLocker-Schutz erforderlich. BitLocker wendet diese Richtlinie bei der Aktivierung an.

Wird diese Einstellung aktiviert,

- stellt Windows ein Festplattenlaufwerk, das von BitLocker geschützt wird, mit Lese- und Schreibzugriff bereit.

- stellt Windows Festplattenlaufwerke, die nicht von BitLocker geschützt werden, schreibgeschützt bereit.

Wenn Sie diese Einstellung nicht konfigurieren, stellt Windows alle Festplattenlaufwerke mit Lese- und Schreibzugriff bereit.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMFDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmfdvdenywriteaccesspolicy?view=sccm-ps).

### <a name="fixed-data-drive-password-policy"></a>Kennwortrichtlinie für Festplattenlaufwerke

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Mit diesen Einstellungen legen Sie die Einschränkungen für Kennwörter fest, die zum Entsperren von Festplattenlaufwerken mit BitLocker-Schutz verwendet werden.

Wenn Sie diese Einstellung aktivieren, können Benutzer ein Kennwort konfigurieren, das den von Ihnen definierten Anforderungen entspricht.

Aktivieren Sie diese Einstellung, um die Sicherheit zu erhöhen, und konfigurieren Sie anschließend die folgenden Einstellungen:

- **Kennwort für Festplattenlaufwerk anfordern**: Benutzer müssen ein Kennwort angeben, um ein Festplattenlaufwerk mit BitLocker-Schutz zu entsperren.

- **Kennwortkomplexität für Festplattenlaufwerke konfigurieren**: Wenn Sie Anforderungen für die Komplexität eines Kennworts erzwingen möchten, klicken Sie auf **Kennwortkomplexität anfordern**.

- **Minimale Kennwortlänge für Festplattenlaufwerk**: Die Standardeinstellung für die minimale Kennwortlänge ist `8`.

Wenn Sie diese Einstellung deaktivieren, können Benutzer kein Kennwort konfigurieren.

Wird die Richtlinie nicht konfiguriert, unterstützt BitLocker Kennwörter gemäß den Standardeinstellungen. Die Standardeinstellungen enthalten keine Komplexitätsanforderungen für Kennwörter und erfordern nur acht Zeichen.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMFDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmfdvpassphrasepolicy?view=sccm-ps).

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Allgemeine Hinweise zur Kennwortrichtlinie für Festplattenlaufwerke

- Damit die festgelegten Einstellungen für die Komplexitätsanforderungen wirksam werden, aktivieren Sie auch die Gruppenrichtlinieneinstellung **Kennwort muss Komplexitätsanforderungen erfüllen** unter **Computerkonfiguration** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Kontorichtlinien** > **Kennwortrichtlinie**.

- Diese Einstellungen werden beim Aktivieren von BitLocker erzwungen, nicht beim Entsperren eines Volumes. Mit BitLocker können Sie ein Laufwerk mit einer der auf dem Laufwerk verfügbaren Schutzvorrichtungen entschlüsseln.

- Wenn Sie eine Gruppenrichtlinie verwenden, um FIPS-konforme Algorithmen für Verschlüsselung, Hashing und Signatur zu aktivieren, sind Kennwörter als BitLocker-Schutzvorrichtung nicht zulässig.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Einstellungen für die Erzwingung von Verschlüsselungsrichtlinien (Festplattenlaufwerk)

*Empfohlene Konfiguration*: **Enabled**

Konfigurieren Sie die Anzahl der Tage, die Benutzer die BitLocker-Konformität für Festplattenlaufwerke verschieben können. Der **Karenzzeit für Nichtkonformität** beginnt zu dem Zeitpunkt, wenn Configuration Manager die Nichtkonformität des Festplattenlaufwerks das erste Mal feststellt. Die Richtlinie für Festplattenlaufwerke wird erst erzwungen, wenn das Betriebssystemlaufwerk konform ist. Nach Ablauf der Karenzzeit können Benutzer die erforderliche Aktion weder verschieben noch eine Ausnahme davon anfordern.

Ist für den Verschlüsselungsprozess eine Benutzereingabe erforderlich, wird in Windows ein Dialogfeld angezeigt, das erst nach Eingabe der erforderlichen Informationen geschlossen werden kann. Zukünftige Fehler- oder Statusbenachrichtigungen weisen diese Einschränkung nicht auf.

Ist für das Hinzufügen einer Schutzvorrichtung durch BitLocker keine Benutzerinteraktion erforderlich, startet BitLocker nach Ablauf der Karenzzeit die Verschlüsselung im Hintergrund.

Wird diese Einstellung deaktiviert oder nicht konfiguriert, fordert Configuration Manager die Benutzer nicht zur Einhaltung von BitLocker-Richtlinien auf.

Wenn Sie die Richtlinie sofort erzwingen möchten, legen Sie die Karenzzeit auf `0` fest.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMUseFddEnforcePolicy](/powershell/module/configurationmanager/new-cmusefddenforcepolicy?view=sccm-ps).

## <a name="removable-drive"></a>Wechseldatenträger

Mit den Einstellungen auf dieser Seite wird die Verschlüsselung für Wechseldatenträger, wie z. B. USB-Sticks, konfiguriert.

### <a name="removable-data-drive-encryption"></a>Verschlüsselung für Wechseldatenträger

*Empfohlene Konfiguration*: **Enabled**

Mit dieser Einstellung können Sie die Verwendung von BitLocker auf Wechseldatenträgern steuern.

- **Benutzer können BitLocker-Schutz auf Wechseldatenträger anwenden:** Benutzer können den BitLocker-Schutz für einen Wechseldatenträger aktivieren.

- **Benutzer können BitLocker-Schutz auf Wechseldatenträgern anhalten und entschlüsseln**: Benutzer können die BitLocker-Laufwerkverschlüsselung für einen Wechseldatenträger entfernen oder temporär anhalten.

Wenn Sie diese Einstellung aktivieren und Benutzern die Anwendung des BitLocker-Schutzes erlauben, speichert der Konfigurations-Manager-Client Wiederherstellungsinformationen zu den Wechseldatenträgern im Wiederherstellungsdienst auf dem Verwaltungspunkt. Dadurch können Benutzer das Laufwerk wiederherstellen, wenn sie das Kennwort der Schutzvorrichtung vergessen oder verloren haben.

Wird diese Einstellung aktiviert,

- aktivieren Sie die Einstellungen für die **Kennwortrichtlinie für Wechseldatenträger**.

- *deaktivieren* Sie die folgenden Gruppenrichtlinieneinstellungen unter **System** > **Zugriff auf Wechselmedien** für Benutzer- und Computerkonfigurationen:

  - **Alle Wechselmedienklassen: Jeglichen Zugriff verweigern**
  - **Wechseldatenträger: Schreibzugriff verweigern**
  - **Wechseldatenträger: Lesezugriff verweigern**

Wenn Sie diese Einstellung deaktivieren, können Benutzer BitLocker auf Wechseldatenträgern nicht verwenden.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMRDVConfigureBDEPolicy](/powershell/module/configurationmanager/new-cmrdvconfigurebdepolicy?view=sccm-ps).

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Verweigern des Schreibzugriffs auf Wechseldatenträger, die nicht von BitLocker geschützt werden

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Hiermit ist zum Schreiben von Daten auf Wechseldatenträger des Geräts BitLocker-Schutz erforderlich. BitLocker wendet diese Richtlinie bei der Aktivierung an.

Wird diese Einstellung aktiviert,

- stellt Windows einen Wechseldatenträger, der von BitLocker geschützt wird, mit Lese- und Schreibzugriff bereit.

- stellt Windows Wechseldatenträger, die nicht von BitLocker geschützt werden, schreibgeschützt bereit.

- Wenn Sie die Option **Schreibzugriff auf Geräte verweigern, die in einer anderen Organisation konfiguriert wurden** aktivieren, gewährt BitLocker nur Wechseldatenträgern Schreibzugriff, deren Identifikationsfelder mit den zulässigen Identifikationsfeldern übereinstimmen. Definieren Sie diese Felder mithilfe der globalen Einstellungen der **eindeutigen Organisationsbezeichner** im Abschnitt [Setup](#setup).

Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, stellt Windows alle Wechseldatenträger mit Lese- und Schreibzugriff bereit.

> [!NOTE]
> Sie können diese Einstellung mit den Gruppenrichtlinieneinstellungen unter **System** > **Zugriff auf Wechselmedien** überschreiben. Wenn Sie die Gruppenrichtlinieneinstellung **Wechseldatenträger: Schreibzugriff verweigern** aktivieren, ignoriert BitLocker diese Configuration Manager-Einstellung.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMRDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmrdvdenywriteaccesspolicy?view=sccm-ps).

### <a name="removable-data-drive-password-policy"></a>Kennwortrichtlinie für Wechseldatenträger

*Empfohlene Konfiguration*: **Enabled**

Mit diesen Einstellungen legen Sie die Einschränkungen für Kennwörter fest, die zum Entsperren von Wechseldatenträgern mit BitLocker-Schutz verwendet werden.

Wenn Sie diese Einstellung aktivieren, können Benutzer ein Kennwort konfigurieren, das den von Ihnen definierten Anforderungen entspricht.

Aktivieren Sie diese Einstellung, um die Sicherheit zu erhöhen, und konfigurieren Sie anschließend die folgenden Einstellungen:

- **Kennwort für Wechseldatenträger anfordern**: Benutzer müssen ein Kennwort angeben, um einen Wechseldatenträger mit BitLocker-Schutz zu entsperren.

- **Kennwortkomplexität für Wechseldatenträger konfigurieren**: Wenn Sie Anforderungen für die Komplexität eines Kennworts erzwingen möchten, klicken Sie auf **Kennwortkomplexität anfordern**.

- **Minimale Kennwortlänge für Wechseldatenträger**: Die Standardeinstellung für die minimale Kennwortlänge ist `8`.

Wenn Sie diese Einstellung deaktivieren, können Benutzer kein Kennwort konfigurieren.

Wird die Richtlinie nicht konfiguriert, unterstützt BitLocker Kennwörter gemäß den Standardeinstellungen. Die Standardeinstellungen enthalten keine Komplexitätsanforderungen für Kennwörter und erfordern nur acht Zeichen.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMRDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmrdvpassphrasepolicy?view=sccm-ps).

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Allgemeine Hinweise zur Kennwortrichtlinie für Wechseldatenträger

- Damit die festgelegten Einstellungen für die Komplexitätsanforderungen wirksam werden, aktivieren Sie auch die Gruppenrichtlinieneinstellung **Kennwort muss Komplexitätsanforderungen erfüllen** unter **Computerkonfiguration** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Kontorichtlinien** > **Kennwortrichtlinie**.

- Diese Einstellungen werden beim Aktivieren von BitLocker erzwungen, nicht beim Entsperren eines Volumes. Mit BitLocker können Sie ein Laufwerk mit einer der auf dem Laufwerk verfügbaren Schutzvorrichtungen entschlüsseln.

- Wenn Sie eine Gruppenrichtlinie verwenden, um FIPS-konforme Algorithmen für Verschlüsselung, Hashing und Signatur zu aktivieren, sind Kennwörter als BitLocker-Schutzvorrichtung nicht zulässig.

## <a name="client-management"></a>Clientverwaltung

Mit den Einstellungen auf dieser Seite können Sie BitLocker-Verwaltungsdienste und -Clients konfigurieren.

### <a name="bitlocker-management-services"></a>BitLocker-Verwaltungsdienste

*Empfohlene Konfiguration*: **Enabled**

Wenn Sie diese Einstellung aktivieren, sichert Configuration Manager die Schlüsselwiederherstellungsinformationen automatisch und ohne Meldung in der Standortdatenbank. Wird diese Einstellung deaktiviert oder nicht konfiguriert, speichert Configuration Manager die Schlüsselwiederherstellungsinformationen nicht.

- **Select BitLocker recovery information to store** (Zu speichernde BitLocker-Wiederherstellungsinformationen auswählen): Hiermit können Sie den Schlüsselwiederherstellungsdienst zum Sichern der BitLocker-Wiederherstellungsinformationen konfigurieren. Die Richtlinie stellt eine Verwaltungsmethode zum Wiederherstellen von mit BitLocker verschlüsselten Daten bereit, um Datenverluste aufgrund fehlender Schlüsselinformationen zu vermeiden.

- **Speicherung von Wiederherstellungsinformationen im Nur-Text-Format zulassen**: Ohne Verschlüsselungszertifikat für die BitLocker-Verwaltung für SQL Server speichert Configuration Manager die Schlüsselwiederherstellungsinformationen im Nur-Text-Format. Weitere Informationen finden Sie unter [Verschlüsseln von Wiederherstellungsdaten](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **Häufigkeit für die Überprüfung des Clientstatus in Minuten eingeben**: Der Client überprüft mit der konfigurierten Häufigkeit die BitLocker-Schutzrichtlinien sowie den Status auf dem Computer und sichert den Clientwiederherstellungsschlüssel. Die Standardeinstellung des Configuration Manager-Clients für die Aktualisierung der BitLocker-Wiederherstellungsinformationen beträgt 90 Minuten.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter:

- [Set-CMBlmPlaintextStorage](/powershell/module/configurationmanager/set-cmblmplaintextstorage?view=sccm-ps)
- [New-CMBMSClientConfigureCheckIntervalPolicy](/powershell/module/configurationmanager/new-cmbmsclientconfigurecheckintervalpolicy?view=sccm-ps)

### <a name="user-exemption-policy"></a>Benutzerausnahmerichtlinie

*Empfohlene Konfiguration*: **Nicht konfiguriert**

Konfigurieren Sie eine Kontaktmethode, über die Benutzer eine Ausnahme von der BitLocker-Verschlüsselung anfordern können.

Geben Sie bei der Aktivierung dieser Richtlinieneinstellung folgende Informationen an:

- **Maximale Anzahl von Tagen für die Verschiebung**: Anzahl der Tage, die Benutzer eine erzwungene Richtlinie verschieben können. Die Standardeinstellung dieses Werts ist `7` Tage (eine Woche).

- **Kontaktmethode**: Geben Sie an, auf welchem Weg Benutzer eine Ausnahme anfordern können: URL, E-Mail-Adresse oder Telefonnummer.

- **Kontakt**: Geben Sie die URL, E-Mail-Adresse oder Telefonnummer für die Kontaktaufnahme an. Fordert ein Benutzer eine Ausnahme vom BitLocker-Schutz an, wird ein Windows-Dialogfeld mit Anweisungen angezeigt. Die von Ihnen eingegebenen Informationen werden von Configuration Manager nicht überprüft.

  - **URL**: Verwenden Sie das URL-Standardformat (`https://website.domain.tld`). In Windows wird die URL als Hyperlink angezeigt.

  - **E-Mail-Adresse:** Verwenden Sie das Standardformat für E-Mail-Adressen (`user@domain.tld`). In Windows wird die Adresse in Form des folgenden Hyperlinks angezeigt: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`.

  - **Telefonnummer**: Geben Sie die Telefonnummer an, die die Benutzer wählen sollen. In Windows wird die Telefonnummer mit folgendem Text angezeigt: `Please call <your number> for applying exemption`.

Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, zeigt Windows den Benutzern keine Anweisungen für das Anfordern einer Ausnahme an.

> [!NOTE]
> BitLocker verwaltet Ausnahmen benutzerbezogen, nicht computerbezogen. Wenn sich mehrere Benutzer beim gleichen Computer anmelden und für einen dieser Benutzer keine Ausnahme besteht, verschlüsselt BitLocker den Computer.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMBMSUserExemptionPolicy](/powershell/module/configurationmanager/new-cmbmsuserexemptionpolicy?view=sccm-ps).

### <a name="url-for-the-security-policy-link"></a>URL für den Link zur Sicherheitsrichtlinie

*Empfohlene Konfiguration*: **Enabled**

Geben Sie eine URL an, die Benutzern in Windows als **Sicherheitsrichtlinie Ihres Unternehmens** angezeigt werden soll. Stellen Sie über diesen Link Ihren Benutzern Informationen zu den Verschlüsselungsanforderungen bereit. Die URL wird angezeigt, wenn Benutzer von BitLocker zum Verschlüsseln eines Laufwerks aufgefordert werden.

Wenn Sie diese Einstellung aktivieren, konfigurieren Sie die **URL für den Link zur Sicherheitsrichtlinie**.

Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, zeigt BitLocker den Link zur Sicherheitsrichtlinie nicht an.

Weitere Informationen zum Erstellen dieser Richtlinie mit Windows PowerShell finden Sie unter [New-CMMoreInfoUrlPolicy](/powershell/module/configurationmanager/new-cmmoreinfourlpolicy?view=sccm-ps).

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie Windows PowerShell zum Erstellen dieser Richtlinienobjekte verwenden, verwenden Sie das [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting?view=sccm-ps)-Cmdlet. Dieses Cmdlet erstellt ein Einstellungsobjekt für BitLocker-Verwaltungsrichtlinien, das alle angegebenen Richtlinien enthält. Verwenden Sie zur Bereitstellung dieser Richtlinieneinstellungen für eine Sammlung das Cmdlet [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment?view=sccm-ps).
