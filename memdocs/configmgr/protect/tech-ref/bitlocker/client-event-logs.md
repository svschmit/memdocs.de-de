---
title: Clientereignisprotokolle
titleSuffix: Configuration Manager
description: Eine technische Referenz für die möglichen BitLocker-Clienteinträge (MBAM) im Windows-Ereignisprotokoll
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705968"
---
# <a name="client-event-logs"></a>Clientereignisprotokolle

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Verwenden Sie auf einem Configuration Manager-Client, auf dem Sie eine BitLocker-Verwaltungsrichtlinie bereitstellen, die Windows-Ereignisanzeige, um BitLocker-Clientereignisprotokolle anzuzeigen. Wechseln Sie zu **Anwendungs- und Dienstprotokolle**, **Microsoft**, **Windows**, **MBAM** für Ereignisprotokolle vom Typ [Admin](#admin) als auch [Betriebsbereit](#operational).

## <a name="admin"></a>Administrator

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Beim Anwenden der MBAM-Richtlinien ist ein Fehler aufgetreten.

#### <a name="error-code--2144272219"></a>Fehlercode: -2144272219

Details: Die BitLocker-Laufwerkverschlüsselung unterstützt nur „Nur verwendeten Speicherplatz verschlüsseln“ für die schlanke Speicherzuweisung.

Dieser Fehler tritt auf, wenn Sie versuchen, BitLocker zum Verschlüsseln eines virtuellen Computers zu verwenden, auf dem Windows 10, Version 1803 oder früher, ausgeführt wird. Frühere Versionen von Windows 10 unterstützen keine vollständige Datenträgerverschlüsselung. Die BitLocker-Verwaltungsrichtlinien erzwingen die vollständige Datenträgerverschlüsselung.

#### <a name="error-code--2147024774"></a>Fehlercode: -2147024774

Details: Der an einen Systemaufruf übergebene Datenbereich ist zu klein.

Starten Sie den Computer neu, um dieses Problem zu beheben.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Bei der Übertragung von Verschlüsselungsstatusdaten ist ein Fehler aufgetreten.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Das Systemvolume fehlt. Das Systemvolume ist erforderlich, um das Betriebssystemlaufwerk zu verschlüsseln.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

Die TPM-Hardware fehlt. TPM ist erforderlich, um das Betriebssystemlaufwerk mit einer TPM-Schutzvorrichtung zu verschlüsseln.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

Der Computer ist von der Verschlüsselung ausgenommen. Hardwarestatus des Computers: Ausgenommen

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

Der Computer ist von der Verschlüsselung ausgenommen. Hardwarestatus des Computers: Unbekannt

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Die Hardwareausnahmeprüfung ist fehlgeschlagen.

### <a name="13-userisexempted"></a>13: UserIsExempted

Der Benutzer ist von der Verschlüsselung ausgenommen.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

Der Benutzer hat eine Ausnahme angefordert.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Die Benutzerausnahmeprüfung ist fehlgeschlagen.

### <a name="16-userpostponed"></a>16: UserPostponed

Der Benutzer hat den Verschlüsselungsprozess verschoben.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

Die TPM-Initialisierung ist fehlgeschlagen. Der Benutzer hat die BIOS-Änderungen abgelehnt.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Es konnte keine Verbindung zu MBAM Recovery And Hardware Service hergestellt werden.

#### <a name="error-code--2147024809"></a>Fehlercode: -2147024809

Details: Der Parameter ist falsch.

Dieser Fehler tritt auf, wenn die Website nicht HTTPS verwendet oder der Client nicht über ein PKI-Zertifikat verfügt.

### <a name="20-policymismatch"></a>20: PolicyMismatch

Die BitLocker-Verwaltungsrichtlinie befindet sich in einem Konflikt oder ist beschädigt.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Es ist ein Konflikt bei erkannten Betriebssystemlaufwerks-Richtlinien aufgetreten. Prüfen Sie die BitLocker-Richtlinien für den Schutz von Betriebssystemlaufwerken.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Es ist ein Konflikt bei erkannten Festplattenlaufwerks-Richtlinien aufgetreten. Prüfen Sie die BitLocker-Richtlinien für den Schutz von Festplattenlaufwerken.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Bei der Verschlüsselung ist ein Fehler aufgetreten. Bei Computern mit Betriebssystemen niedriger als Windows 8.1 ist Schutz durch einen Datenwiederherstellungs-Agent im FIPS-Modus erforderlich.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Fehler beim Zurücksetzen der TPM-Sperre.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Fehler beim Abrufen von TPM OwnerAuth aus MBAM-Diensten.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Fehler beim Aktualisieren des DLL-Suchpfads für den WMI-Anbieter.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Der Agent wird beendet. Timeout beim Warten auf die MBAM-WMI-Anbieterinstanz.

## <a name="operational"></a>Betriebsbereit

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

Die BitLocker-Verwaltungsrichtlinien wurden erfolgreich angewendet.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

Die Verschlüsselungsstatusdaten wurden erfolgreich übertragen.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Es konnte erfolgreich eine Verbindung zu MBAM Recovery And Hardware Service hergestellt werden.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

Die TPM OwnerAuth wurde hinterlegt.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

Der BitLocker-Wiederherstellungsschlüssel für das Volume wurde hinterlegt.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

Der BitLocker-Wiederherstellungsschlüssel für das Volume wurde aktualisiert.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

Das Datum für die Umsetzung der Richtlinie wurde für das Volume festgelegt.

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

Das Datum für die Umsetzung der Richtlinie wurde für das Volume gelöscht.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

Die TPM-Sperre wurde erfolgreich zurückgesetzt.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

TPM OwnerAuth wurde erfolgreich aus MBAM-Diensten abgerufen.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

Wechseldatenträger wurde eingebunden.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

Die Einbindung des Wechseldatenträgers wurde aufgehoben.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

Fehler beim Herstellen einer Verbindung mit dem MBAM-Wiederherstellungs- und Hardwaredienst verhinderten, dass die BitLocker-Verwaltungsrichtlinien erfolgreich auf das Volume angewendet werden konnten.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Der Status des gesperrten Volumes verhinderte, dass die BitLocker-Verwaltungsrichtlinien erfolgreich auf das Volume angewendet werden konnten.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

Die fehlende Verbindung zum MBAM-Konformitäts- und -Statusdienst verhinderte die Übertragung von Verschlüsselungsstatusdaten.

## <a name="see-also"></a>Weitere Informationen:

Weitere Informationen zur Verwendung dieser Protokolle finden Sie unter [BitLocker-Ereignisprotokolle](about-event-logs.md).

Weitere Informationen zur Problembehandlung finden Sie unter [Problembehandlung für BitLocker](troubleshoot.md).
