---
title: Verschlüsseln von Windows 10-Geräten mit BitLocker in Intune
titleSuffix: Microsoft Intune
description: Verschlüsseln Sie Geräte mithilfe der integrierten BitLocker-Verschlüsselungsmethode, und verwalten Sie die Wiederherstellungsschlüssel für diese verschlüsselten Geräte über das Intune-Portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 8843ab5c8bf3d0e6970398c1ad81a8a2b3b8f9cb
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193962"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Verwalten der BitLocker-Richtlinie für Windows 10 in Intune

Verwenden Sie Intune, um die BitLocker-Laufwerkverschlüsselung auf Geräten unter Windows 10 zu konfigurieren.

BitLocker ist auf Geräten verfügbar, auf denen Windows 10 oder höher ausgeführt wird. Einige Einstellungen für BitLocker erfordern, dass das Gerät über ein unterstütztes TPM verfügt.

Verwenden Sie einen der folgenden Richtlinientypen, um BitLocker auf Ihren verwalteten Geräten zu konfigurieren:

- **[Endpunktsicherheit-Datenträgerverschlüsselungsrichtlinie für Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)** . Das BitLocker-Profil in *Endpunktsicherheit* ist eine fokussierte Gruppe von Einstellungen, die für die Konfiguration von BitLocker vorgesehen ist.

  Sehen Sie sich die BitLocker-Einstellungen an, die in [BitLocker-Profile aus der Datenträgerverschlüsselungsrichtlinie](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) verfügbar sind.

- **[Gerätekonfigurationprofil für Endpunktschutz für Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)** . Die BitLocker-Einstellungen gehören zu den verfügbaren Einstellungskategorien für Windows 10-Endpunktschutz.

  Zeigen Sie die [BitLocker-Einstellungen an, die in Endpunktschutzprofilen für die Gerätekonfigurationsrichtlinie für BitLocker verfügbar sind](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune beinhaltet einen integrierten [Verschlüsselungsbericht](encryption-monitor.md), in dem Details zum Verschlüsselungsstatus Ihrer verwalteten Geräte angezeigt werden. Sobald Intune ein Windows 10-Gerät mit BitLocker verschlüsselt, können Sie die BitLocker-Wiederherstellungsschlüssel im Verschlüsselungsbericht einsehen und abrufen.
>
> Sie können über Ihre Geräte wie bei Azure Active Directory (Azure AD) auch auf wichtige Informationen zu BitLocker zugreifen.
[Verschlüsselungsbericht](encryption-monitor.md), in dem Details zum Verschlüsselungsstatus Ihrer verwalteten Geräte angezeigt werden.

## <a name="permissions-to-manage-bitlocker"></a>Berechtigungen zum Verwalten von BitLocker

Damit Sie BitLocker in Intune verwalten können, muss Ihr Konto in Intune über die entsprechenden Berechtigungen für [rollenbasierte Zugriffssteuerung](../fundamentals/role-based-access-control.md) (RBAC) verfügen.

Im Folgenden werden die BitLocker-Berechtigungen aufgelistet, die zur Kategorie der Remoteaufgaben gehören, sowie die integrierten RBAC-Rollen für das Erteilen der jeweiligen Berechtigung:

- **Rotieren von BitLocker-Schlüsseln**
  - Helpdesk-Operator

## <a name="create-and-deploy-policy"></a>Erstellen und Bereitstellen einer Richtlinie

Verwenden Sie eines der folgenden Verfahren, um den von Ihnen bevorzugten Richtlinientyp zu erstellen.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Erstellen einer Endpunktsicherheitsrichtlinie für BitLocker

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Datenträgerverschlüsselung** > **Richtlinie erstellen** aus.

3. Legen Sie die folgenden Optionen fest:
   1. **Plattform**: Windows 10 oder höher
   2. **Profil**: BitLocker

   ![Auswählen des BitLocker-Profils](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. Konfigurieren Sie auf der Seite **Konfigurationseinstellungen** die Einstellungen für BitLocker entsprechend Ihren Geschäftsanforderungen.  

   Wenn Sie BitLocker unbeaufsichtigt aktivieren möchten, finden Sie weitere Informationen zu weiteren Voraussetzungen und den jeweils zu verwendenden Einstellungskonfigurationen unter [Unbeaufsichtigtes Aktivieren von BitLocker auf Geräten](#silently-enable-bitlocker-on-devices) in diesem Artikel.

   Wählen Sie **Weiter** aus.

5. Klicken Sie auf der Seite **Bereich (Markierungen)** auf **Bereichstags auswählen**, um den Bereich „Markierungen auswählen“ zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

6. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter „Zuweisen von Benutzer- und Geräteprofilen“.

   Wählen Sie **Weiter** aus.

7. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Erstellen eines Gerätekonfigurationsprofils für BitLocker

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Legen Sie die folgenden Optionen fest:
   1. **Plattform**: Windows 10 und höher
   2. **Profiltyp**: Endpoint Protection

   ![Auswählen des Profils](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Klicken Sie auf **Einstellungen** > **Windows-Verschlüsselung**.

   ![BitLocker-Einstellungen](./media/encrypt-devices/bitlocker-settings.png)

5. Konfigurieren Sie die Einstellungen für BitLocker entsprechend Ihren Geschäftsanforderungen.

   Wenn Sie BitLocker unbeaufsichtigt aktivieren möchten, finden Sie weitere Informationen zu weiteren Voraussetzungen und den jeweils zu verwendenden Einstellungskonfigurationen unter [Unbeaufsichtigtes Aktivieren von BitLocker auf Geräten](#silently-enable-bitlocker-on-devices) in diesem Artikel.

6. Klicken Sie auf **OK**.

7. Schließen Sie die Konfiguration zusätzlicher Einstellungen ab, und speichern Sie anschließend das Profil.

## <a name="manage-bitlocker"></a>Verwalten von BitLocker

Informationen zu Geräten, die die BitLocker-Richtlinie erhalten, finden Sie unter [Überwachen der Datenträgerverschlüsselung](../protect/encryption-monitor.md). Sie können die BitLocker-Wiederherstellungsschlüssel auch anzeigen und abrufen, wenn Sie den Verschlüsselungsbericht anzeigen.

### <a name="silently-enable-bitlocker-on-devices"></a>Aktivieren von BitLocker auf Geräten ohne Meldung

Sie können eine BitLocker-Richtlinie konfigurieren, die automatisch und ohne Meldung BitLocker auf einem Gerät aktivieren. Das bedeutet, dass BitLocker erfolgreich aktiviert wird, ohne dem Endbenutzer eine Benutzeroberfläche anzuzeigen, auch wenn der Benutzer kein lokaler Administrator auf dem Gerät ist.

**Voraussetzungen für Geräte:**

Ein Gerät muss die folgenden Bedingungen erfüllen, damit BitLocker ohne Meldung aktiviert werden kann:

- Wenn sich Endbenutzer beim Gerät als Administrator anmelden, muss auf dem Gerät Windows 10, Version 1803 oder höher ausgeführt werden.
- Wenn sich Endbenutzer beim Gerät als Standardbenutzer anmelden, muss auf dem Gerät Windows 10, Version 1809 oder höher ausgeführt werden.
- Das Gerät muss in Azure AD eingebunden sein.  

**BitLocker-Richtlinienkonfiguration:**

Die folgenden zwei Einstellungen der *BitLocker-Grundeinstellungen* müssen in der BitLocker-Richtlinie konfiguriert:

- **Warnung zu anderer Datenträgerverschlüsselung** = *Blockieren*.
- **Standardbenutzern das Aktivieren der Verschlüsselung bei Azure AD-Verknüpfung erlauben** = *Zulassen*

Die Verwendung einer Systemstart-PIN oder eines Systemstartschlüssels **darf nicht von der BitLocker-Richtlinie erfordert werden**. Wenn eine TPM-Start-PIN oder ein Startschlüssel *erforderlich* ist, kann BitLocker nicht unbeaufsichtigt aktiviert werden und erfordert einen Eingriff vom Endbenutzer.  Diese Anforderung wird mithilfe der folgenden drei *BitLocker-Einstellungen für das Betriebssystemlaufwerk* in derselben Richtlinie erfüllt:

- **Systemstart-PIN für kompatibles TPM** darf nicht auf *Systemstart-PIN mit TPM erforderlich* festgelegt sein.
- **Systemstartschlüssel für kompatibles TPM** darf nicht auf *Systemstartschlüssel mit TPM erforderlich* festgelegt sein.
- **Systemstartschlüssel und -Systemstart-PIN für kompatibles TPM** darf nicht auf *Systemstartschlüssel und -PIN mit TPM erforderlich* festgelegt sein.

### <a name="view-details-for-recovery-keys"></a>Anzeigen von Details zu Wiederherstellungsschlüsseln

Intune gewährt Zugriff auf das Azure AD-Blatt für BitLocker, sodass Sie sich über das Intune-Portal die BitLocker-Schlüssel-IDs und -Wiederherstellungsschlüssel für Ihre Windows 10-Geräte ansehen können. Damit auf ein Gerät zugegriffen werden kann, müssen die dazugehörigen Schlüssel in Azure AD hinterlegt sein.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie auf **Geräte** > **Alle Geräte**.

3. Wählen Sie ein Gerät aus der Liste aus, und wählen Sie dann unter *Überwachung* die Option **Recovery keys** (Wiederherstellungsschlüssel) aus.
  
   Wenn Schlüssel in Azure AD verfügbar sind, sind die folgenden Informationen verfügbar:
   - BitLocker-Schlüssel-ID
   - BitLocker-Wiederherstellungsschlüssel
   - Laufwerkstyp

   Wenn keine Schlüssel in Azure AD verfügbar sind, zeigt Intune die Meldung *Für dieses Gerät wurde kein BitLocker-Schlüssel gefunden* an.

Informationen zu BitLocker stehen über den [BitLocker-Konfigurationsdienstanbieter](/windows/client-management/mdm/bitlocker-csp) (Configuration Service Provider, CSP) zur Verfügung. Der BitLocker-CSP wird ab der Windows 10-Version 1703 unterstützt, und ab der Windows 10 Pro-Version 1809.

### <a name="rotate-bitlocker-recovery-keys"></a>Drehen von BitLocker-Wiederherstellungsschlüsseln

Sie können mithilfe einer Intune-Geräteaktion über eine Remoteverbindung den BitLocker-Wiederherstellungsschlüssel eines Geräts mit Windows 10, Version 1909 oder höher drehen.

#### <a name="prerequisites"></a>Voraussetzungen

Geräte müssen die folgenden Voraussetzungen erfüllen, damit der BitLocker-Wiederherstellungsschlüssel gedreht werden kann:

- Sie müssen Windows 10, Version 1909 oder höher ausführen.

- In Azure AD und hybrid eingebundene Geräte müssen die Schlüsselrotation über eine BitLocker-Richtlinienkonfiguration unterstützen:

  - **Vom Client gesteuerte Rotation des Wiederherstellungskennworts**, festgelegt auf *Rotation auf in Azure AD eingebundenen Geräten aktivieren* oder *Rotation auf in Azure AD und hybrid eingebundenen Geräten aktivieren*
  - **BitLocker-Wiederherstellungsinformationen in Azure Active Directory speichern**, festgelegt auf *Aktiviert*
  - **Vor dem Aktivieren von BitLocker Wiederherstellungsinformationen in Azure Active Directory speichern**, festgelegt auf *Erforderlich*

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>So drehen Sie den BitLocker-Wiederherstellungsschlüssel

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie auf **Geräte** > **Alle Geräte**.

3. Wählen Sie in der Liste der von Ihnen verwalteten Geräte ein Gerät aus, und klicken Sie erst auf **Mehr** und anschließend auf die Remotegeräteaktion **BitLocker-Schlüsselrotation**.

4. Wählen Sie auf der Seite **Übersicht** des Geräts die Option **BitLocker-Schlüsselrotation** aus. Wenn diese Option nicht angezeigt wird, wählen Sie die Auslassungspunkte ( **...** ) aus, um zusätzliche Optionen anzuzeigen, und wählen Sie dann die **BitLocker-Schlüsselrotation**-Remotegeräteaktion aus.

   ![Auswählen der Auslassungspunkte, um weitere Optionen anzuzeigen](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Nächste Schritte

[Verwalten der FileVault-Richtlinie](../protect/encrypt-devices-filevault.md)

[Überwachen der Datenträgerverschlüsselung](../protect/encryption-monitor.md)
