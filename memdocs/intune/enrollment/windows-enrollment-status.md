---
title: Einrichten der Seite zum Registrierungsstatus
titleSuffix: Microsoft Intune
description: Richten Sie eine Begrüßungsseite für Benutzer ein, die Windows 10-Geräte registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75f6585144f62636033c94f701a57cb70e018c26
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051579"
---
# <a name="set-up-the-enrollment-status-page"></a>Einrichten der Seite zum Registrierungsstatus
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
Auf der Seite zum Registrierungsstatus wird der Bereitstellungsfortschritt angezeigt, wenn ein neues Gerät registriert wurde oder neue Benutzer sich beim Gerät anmelden.  Dies gibt IT-Administratoren die Möglichkeit, den Zugriff auf das Gerät zu verhindern (blockieren), bis es vollständig bereitgestellt wurde, und dabei gleichzeitig die Benutzer über die verbleibenden Tasks im Bereitstellungsprozess zu informieren.

Die Seite zum Registrierungsstatus kann in jedem [Windows Autopilot](../../autopilot/index.yml)-Bereitstellungsszenario verwendet werden und auch unabhängig von Windows Autopilot als Teil der standardmäßigen Windows-Willkommensseite für Azure AD Join sowie für alle neuen Benutzer, die sich zum ersten Mal beim Gerät anmelden.

Sie können mehrere Profile für die Seite zum Registrierungsstatus mit verschiedenen Konfigurationen für die folgenden Aspekte erstellen:

- Anzeigen des Installationsfortschritts
- Blockieren des Zugriffs, bis der Bereitstellungsprozess abgeschlossen ist
- Zeitlimits
- Zulässige Problembehandlungsvorgänge

Diese Profile werden in der Reihenfolge der Priorität angegeben. Es wird jeweils die höchste geltende Priorität verwendet.  Jedes Profil für die Seite zum Registrierungsstatus kann sich auf Gruppen mit Geräten oder Benutzern beziehen.  Beim Bestimmen des zu verwendenden Profils werden die folgenden Kriterien berücksichtigt:

- Das für das Gerät bestimmte Profil mit der höchsten Priorität wird zuerst verwendet.
- Wenn für das Gerät keine Profile vorhanden sind, wird das für den aktuellen Benutzer bestimmte Profil mit der höchsten Priorität verwendet.  (Dies gilt nur für Szenarios, in denen ein Benutzer vorhanden ist. Bei Szenarios mit intensiver Benutzerunterstützung und solchen mit automatischer Bereitstellung können nur Profile für Geräte verwendet werden.)
- Wenn keine Profile für bestimmte Gruppen vorhanden sind, wird das Standardprofil für die Seite zum Registrierungsstatus verwendet.

## <a name="available-settings"></a>Verfügbare Einstellungen

Die folgenden Einstellungen können konfiguriert werden, um das Verhalten der Seite zum Registrierungsstatus anzupassen:

<table>
<th align="left">Einstellung<th align="left">Ja<th align="left">Nein
<tr><td>Installationsfortschritt für Apps und Profile anzeigen<td>Die Seite zum Registrierungsstatus wird angezeigt.<td>Die Seite zum Registrierungsstatus wird nicht angezeigt.
<tr><td>Geräteverwendung blockieren, bis alle Apps und Profile installiert sind<td>Die Einstellungen in dieser Tabelle werden zur Verfügung gestellt, um das Verhalten der Seite zum Registrierungsstatus anzupassen, sodass der Benutzer mögliche Installationsprobleme beheben kann.
<td>Die Seite zum Registrierungsstatus wird ohne zusätzliche Optionen zum Beheben von Installationsproblemen angezeigt.
<tr><td>Benutzern bei Installationsfehlern das Zurücksetzen des Geräts erlauben<td>Bei einem Installationsfehler wird die Schaltfläche <b>Gerät zurücksetzen</b> angezeigt.<td>Bei einem Installationsfehler wird die Schaltfläche <b>Gerät zurücksetzen</b> nicht angezeigt.
<tr><td>Benutzern bei Installationsfehlern Geräteverwendung erlauben<td>Bei einem Installationsfehler wird die Schaltfläche <b>Trotzdem fortfahren</b> angezeigt.<td>Bei einem Installationsfehler wird die Schaltfläche <b>Trotzdem fortfahren</b> nicht angezeigt.
<tr><td>Timeoutfehler anzeigen, wenn die Installation länger als die angegebene Anzahl von Minuten dauert<td colspan="2">Geben Sie die Anzahl der Minuten an, die auf den Abschluss der Installation gewartet werden soll. 60 Minuten ist als Standardwert vorgegeben.
<tr><td>Bei einem Fehler benutzerdefinierte Meldung anzeigen<td>Ein Textfeld steht bereit, in das Sie eine benutzerdefinierte Meldung eingeben können, die angezeigt wird, sobald ein Installationsfehler auftritt.<td>Die Standardmeldung wird angezeigt: <br><b>Die Installation hat das von Ihrer Organisation festgelegte Zeitlimit überschritten. Versuchen Sie es nochmals, oder wenden Sie sich an Ihren IT-Support.<b>
<tr><td>Benutzern das Erfassen von Protokollen zu Installationsfehlern erlauben<td>Bei einem Installationsfehler wird die Schaltfläche <b>Protokolle sammeln</b> angezeigt. <br>Wenn der Benutzer auf diese Schaltfläche klickt, wird er aufgefordert, einen Speicherort für die Protokolldatei <b>MDMDiagReport.cab</b> auszuwählen.<td>Bei einem Installationsfehler wird die Schaltfläche <b>Protokolle sammeln</b> nicht angezeigt.
<tr><td>Geräteverwendung blockieren, bis diese erforderlichen Apps installiert sind, wenn sie dem Benutzer/Gerät zugewiesen sind<td colspan="2">Wählen Sie <b>Alle</b> oder <b>Ausgewählt</b> aus. <br><br>Bei Wahl von <b>Ausgewählt</b> wird die Schaltfläche <b>Anwendungen auswählen</b> eingeblendet, über die Sie bestimmen können, welche Apps vor der Aktivierung des Geräts installiert werden müssen.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>Aktivieren der standardmäßigen Seite zum Registrierungsstatus für alle Benutzer

Führen Sie die folgenden Schritte aus, um die Seite zum Registrierungsstatus zu aktivieren.
 
1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Seite zum Registrierungsstatus**.
2. Klicken Sie auf dem Blatt **Seite zum Registrierungsstatus** auf **Standard** > **Einstellungen**.
3. Klicken Sie für **Show app and profile installation progress** (Installationsfortschritt für die App und das Profil anzeigen) auf **Ja**.
4. Wählen Sie die anderen Einstellungen aus, die Sie aktivieren wollen, und klicken Sie anschließend auf **Speichern**.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Erstellen eines Profils des Typs „Seite zum Registrierungsstatus“ und Zuweisen zu einer Gruppe

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Seite zum Registrierungsstatus** > **Profil erstellen**.
2. Geben Sie einen **Namen** und eine **Beschreibung** an.
3. Wählen Sie **Erstellen** aus.
4. Wählen Sie das neue Profil in der Liste der **Seite zum Registrierungsstatus** aus.
5. Klicken Sie auf **Zuweisungen** > **Gruppen auswählen**. Wählen Sie dann die Gruppen aus, für die dieses Profil übernommen werden soll, und klicken Sie abschließend auf **Auswählen** > **Speichern**.
6. Wählen Sie **Einstellungen** und dann die Einstellungen aus, die Sie auf dieses Profil anwenden möchten. Klicken Sie auf **Speichern** aus.

## <a name="set-the-enrollment-status-page-priority"></a>Festlegen der Priorität von Registrierungsstatusseiten

Ein Gerät oder Benutzer kann zu vielen Gruppen gehören und über mehrere Profile für die Seite zum Registrierungsstatus verfügen. Sie können steuern, welche Profile zuerst berücksichtigt werden, indem Sie die Prioritäten für jedes Profil festlegen. Die Profile mit höheren Prioritäten werden zuerst berücksichtigt.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Seite zum Registrierungsstatus**.
2. Zeigen Sie auf das Profil in der Liste.
3. Ziehen Sie mithilfe der drei vertikalen Punkte das Profil an die gewünschte Position in der Liste.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Blockieren des Zugriffs auf ein Gerät, bis eine bestimmte Anwendung installiert ist

Sie können angeben, welche Apps installiert sein müssen, bevor die Seite zum Registrierungsstatus geschlossen wird.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Seite zum Registrierungsstatus**.
2. Wählen Sie ein Profil und dann **Einstellungen** aus.
3. Wählen Sie **Ja** für **Installationsfortschritt für Apps und Profile anzeigen** aus.
4. Wählen Sie **Ja** für **Geräteverwendung blockieren, bis alle Apps und Profile installiert sind** aus.
5. Wählen Sie **Ausgewählt** für **Geräteverwendung blockieren, bis diese erforderlichen Apps installiert sind, wenn sie dem Benutzer/Gerät zugewiesen sind** aus.
6. Wählen Sie **Apps auswählen**, wählen Sie die Apps und dann **Auswählen** > **Speichern** aus.

Die in dieser Liste enthaltenen Apps werden von Intune verwendet, um die Liste zu filtern, die als blockierend betrachtet werden soll.  Es wird nicht angegeben, welche Apps installiert werden sollen.  Wenn Sie diese Liste z. B. so konfigurieren, dass sie „App 1“, „App 2“ und „App 3“ enthält und „App 3“ und „App 4“ auf das Gerät oder den Benutzer ausgerichtet sind, verfolgt die Seite zum Registrierungsstatus nur „App 3“.  „App 4“ wird weiterhin installiert, aber die Seite zum Registrierungsstatus wartet nicht auf ihren Abschluss.

Es können maximal 100 Apps angegeben werden.

## <a name="enrollment-status-page-tracking-information"></a>Auf der Seite zum Registrierungsstatus nachverfolgte Informationen

Auf der Seite zum Registrierungsstatus werden Informationen in drei Phasen nachverfolgt: Gerätevorbereitung, Geräteeinrichtung und Kontoeinrichtung.

### <a name="device-preparation"></a>Gerätevorbereitung

Zur Vorbereitung des Geräts wird auf der Seite zum Registrierungsstatus Folgendes nachverfolgt:

- TPM-Schlüsselnachweis (Trusted Platform Module) (falls zutreffend)
- Azure Active Directory-Beitrittsprozess
- Intune-(MDM-)Registrierung
- Installation der Intune-Verwaltungserweiterungen (verwendet zum Installieren von Win32-Apps)

### <a name="device-setup"></a>Geräteeinrichtung

Auf der Seite zum Registrierungsstatus wird der Status der folgenden Geräteeinrichtungselemente angezeigt:

- Sicherheitsrichtlinien
  - Ein Konfigurationsanbieter für alle Registrierungen
  - Tatsächliche CSPs, die von Intune konfiguriert wurden, werden an dieser Stelle nicht nachverfolgt.
- Applications
  - Branchenspezifische MSI-Apps („pro Computer“)
  - Branchenspezifische Store-Apps mit dem Installationskontext „Gerät“
  - Branchenspezifische und Offline Store-Apps mit dem Installationskontext „Gerät“
  - Win32-Anwendungen (ab Windows 10, Version 1903) 
- Konnektivitätsprofile
  - VPN- oder WLAN-Profile, die **allen Geräten** oder einer Gerätegruppe zugewiesen sind, in der das zu registrierende Gerät ein Mitglied ist, jedoch nur für Autopilot-Geräte
- Zertifikat-Profile, die **allen Geräten** oder einer Gerätegruppe zugewiesen sind, in der das zu registrierende Gerät ein Mitglied ist, jedoch nur für Autopilot-Geräte

### <a name="account-setup"></a>Kontoeinrichtung

Für die Kontoeinrichtung werden die folgenden Elemente auf der Seite zum Registrierungsstatus nachverfolgt, wenn diese dem derzeit angemeldeten Benutzer zugewiesen sind:

- Sicherheitsrichtlinien
  - Ein CSP für alle Registrierungen
  - Tatsächliche CSPs, die von Intune konfiguriert wurden, werden an dieser Stelle nicht nachverfolgt.
- Applications
  - Branchenspezifische MSI-Apps („pro Benutzer“), die „Allen Geräten“, „Allen Benutzern“ oder einer „Benutzergruppe“ zugewiesen sind, der der sich registrierende Benutzer angehört
  - Branchenspezifische MSI-Apps („pro Computer“), die „Allen Benutzern“ oder einer „Benutzergruppe“ zugewiesen sind, der der sich registrierende Benutzer angehört
  - Branchenspezifische Store-, Onlinestore- und Offlinestore-Apps, die einem der folgenden Objekte zugewiesen sind:
    - Alle Geräte
    - Allen Benutzern
    - Eine Benutzergruppe, zu der der Benutzer gehört, der das Gerät registriert, wobei der Installationskontext auf „Benutzer“ festgelegt ist.
  - Win32-Anwendungen (ab Windows 10, Version 1903) 
- Konnektivitätsprofile
  - VPN- oder WLAN-Profile, die „Allen Benutzern“ oder einer „Benutzergruppe“ zugewiesen sind, der der sich registrierende Benutzer angehört
- Zertifikate
  - Zertifikatprofile, die „Allen Benutzern“ oder einer „Benutzergruppe“ zugewiesen sind, der der sich registrierende Benutzer angehört

### <a name="troubleshooting"></a>Problembehandlung

Im Folgenden sind häufig gestellte Fragen zur Behandlung von Problemen im Zusammenhang mit der Seite zum Registrierungsstatus aufgeführt.

- Warum wurden meine Anwendungen nicht über die Seite „Registrierungsstatus“ installiert und nachverfolgt?
  - Stellen Sie Folgendes sicher, um zu gewährleisten, dass Anwendungen über die Seite „Registrierungsstatus“ installiert und nachverfolgt werden:
      - Die Apps werden über eine „erforderliche“ Zuweisung einer Azure AD-Gruppe zugewiesen, die das Gerät (für geräteorientierte Apps) oder den Benutzer (für benutzerorientierte Apps) enthält.  (Geräteorientierte Apps werden Während der Gerätephase von ESP nachverfolgt, während benutzerorientierte Apps während der Benutzerphase von ESP nachverfolgt werden.)
      - Entweder Sie geben **Geräteverwendung blockieren, bis alle Apps und Profile installiert sind** an oder schließen die App in die Liste **Block device use until these required apps are installed** (Geräteverwendung blockieren, bis diese erforderlichen Apps installiert wurden) ein.
      - Diese Apps werden im Gerätekontext installiert und verfügen nicht über Anwendbarkeitsregeln im Benutzerkontext.

- Warum wird die Seite zum Registrierungsstatus für Bereitstellungen ohne Autopilot angezeigt, z. B. wenn sich ein Benutzer zum ersten Mal auf einem registrierten Gerät anmeldet, das gemeinsam mit Configuration Manager verwaltet wird?  
  - Auf der Seite zum Registrierungsstatus wird der Installationsstatus für alle Registrierungsmethoden angezeigt, einschließlich
      - Autopilot
      - Co-Verwaltung mit Configuration Manager
      - wenn sich ein neuer Benutzer bei dem Gerät anmeldet, auf dem die Richtlinie „Seite zum Registrierungsstatus“ zum ersten Mal angewendet wird
      - wenn die Einstellung **Seite nur für Geräte anzeigen, die über die Willkommensseite bereitgestellt wurden** aktiviert ist und für die Richtlinie festgelegt ist, dass nur dem ersten Benutzer, der sich auf dem Gerät anmeldet, die Seite zum Registrierungsstatus angezeigt wird.

- Wie kann ich die Seite zum Registrierungsstatus deaktivieren, wenn sie auf dem Gerät konfiguriert wurde?
  - Die Richtlinie „Seite zum Registrierungsstatus“ wird zum Zeitpunkt der Registrierung auf einem Gerät festgelegt. Um die Seite zum Registrierungsstatus zu deaktivieren, müssen Sie deren Abschnitte „Benutzer“ und „Gerät“ deaktivieren. Sie deaktivieren die Abschnitte, indem Sie benutzerdefinierte OMA-URI-Einstellungen mit den folgenden Konfigurationen erstellen.

      Deaktivieren der Seite zum Registrierungsstatus für Benutzer:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Deaktivieren der Seite zum Registrierungsstatus für Geräte:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- Wie kann ich Protokolldateien sammeln?
  - Es gibt zwei Möglichkeiten zur Erfassung von Protokolldateien zur Seite zum Registrierungsstatus (Enrollment Status Page, ESP):
      - Aktivieren Sie in der ESP-Richtlinie, dass Benutzer Protokolle sammeln dürfen. Wenn auf der Seite zum Registrierungsstatus ein Timeout auftritt, kann der Endbenutzer die Option **Protokolle sammeln** wählen. Nach Herstellen einer Verbindung mit einem USB-Laufwerk können die Protokolldateien darauf kopiert werden.
      - Öffnen Sie eine Eingabeaufforderung, indem Sie UMSCHALTTASTE+F10 drücken und dann die folgende Befehlszeile eingeben, um die Protokolldateien zu generieren: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>Bekannte Probleme

Im Folgenden sind bekannte Probleme im Zusammenhang mit der Seite zum Registrierungsstatus aufgeführt.

- Durch das Deaktivieren des ESP-Profils wird die zugehörige Richtlinie nicht von den Geräten entfernt, und den Benutzern wird weiterhin die Seite zum Registrierungsstatus angezeigt, wenn sie sich zum ersten Mal am Gerät anmelden. Die Richtlinie wird nicht entfernt, wenn das ESP-Profil deaktiviert wird. Sie müssen den OMA-URI bereitstellen, um die Seite zum Registrierungsstatus zu deaktivieren. Weitere Informationen zum Deaktivieren der Seite zum Registrierungsstatus mithilfe des OMA-URI finden Sie weiter oben. 
- Ein Neustart während der Geräteeinrichtung zwingt den Benutzer vor dem Übergang zur Phase „Kontoeinrichtung“ zur Eingabe seiner Anmeldeinformationen. Benutzeranmeldeinformationen werden während des Neustarts nicht beibehalten. Lassen Sie den Benutzer seine Anmeldeinformationen eingeben, damit die Seite zum Registrierungsstatus fortgesetzt werden kann. 
- Für die Seite zum Registrierungsstatus unter Windows 10-Versionen vor 1903 erfolgt während einer Registrierung des Typs „Geschäfts-, Schul- oder Unikonto hinzufügen“ immer ein Timeout. Die Seite zum Registrierungsstatus wartet auf den Abschluss der Azure AD Registrierung. Das Problem wurde für Windows 10 ab Version 1903 behoben.  
- Azure AD Hybrid-Autopilot-Bereitstellung mit Seite zum Registrierungsstatus dauert länger als die Timeoutdauer, die im ESP-Profil angegeben ist. Bei Azure AD Hybrid-Autopilot-Bereitstellungen benötigt die Seite zum Registrierungsstatus 40 Minuten länger als der im ESP-Profil festgelegte Wert. Diese Verzögerung gibt dem lokalen AD-Connector Zeit zum Erstellen des neuen Gerätedatensatzes für Azure AD. 
- Windows-Anmeldeseite wird im benutzergesteuerten Autopilot-Modus nicht mit dem Benutzernamen vorausgefüllt. Bei einem Neustart in der Phase „Geräteeinrichtung“ der Seite zum Registrierungsstatus gilt Folgendes:
  - Benutzeranmeldeinformationen werden nicht beibehalten.
  - Der Benutzer muss die Anmeldeinformationen vor dem Wechsel von der Phase „Geräteeinrichtung“ zur Phase „Kontoeinrichtung“ erneut eingeben.
- Die Seite zum Registrierungsstatus ist lange im Stillstand oder beendet nie die Phase „Identifying“ (Identifizierung). Intune berechnet die ESP-Richtlinien in der Phase „Identifizierung“. Ein Gerät schließt das Berechnungen der ESP-Richtlinien ggf. nie ab, wenn dem aktuellen Benutzer keine Intune-Lizenz zugewiesen ist.  
- Die Konfiguration der Microsoft Defender-Anwendungssteuerung bewirkt eine Aufforderung zum Neustart im Autopilot-Modus. Das Konfigurieren der Microsoft Defender-Anwendung (mit AppLocker als Kryptografiedienstanbieter) erfordert einen Neustart. Wenn diese Richtlinie konfiguriert ist, kann dies dazu führen, dass ein Gerät im Autopilot-Modus neu gestartet wird. Derzeit gibt es keine Möglichkeit, den Neustart zu unterdrücken oder zu verschieben.
- Wenn die DeviceLock-Richtlinie (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) als Teil eines ESP-Profils aktiviert ist, kann die Windows-Willkommensseite oder automatische Anmeldung am Benutzerdesktop aus zwei Gründen unerwartet fehlschlagen.
  - Wenn das Gerät nicht neu gestartet wurde, bevor die ESP-Phase „Geräteeinrichtung“ beendet wurde, wird der Benutzer möglicherweise aufgefordert, seine Azure AD-Anmeldeinformationen einzugeben. Diese Eingabeaufforderung erfolgt anstelle einer erfolgreichen automatischen Anmeldung, bei der der Benutzer die Animation zur ersten Anmeldung unter Windows sieht.
  - Bei der automatischen Anmeldung tritt ein Fehler auf, wenn das Gerät neu gestartet wird, nachdem der Benutzer seine Azure AD-Anmeldeinformationen eingegeben, aber die ESP-Phase „Geräteeinrichtung“ noch nicht beendet hat. Dieser Fehler tritt auf, weil die ESP-Phase „Geräteeinrichtung“ nie abgeschlossen wurde. Die Problemumgehung besteht im Zurücksetzen des Geräts.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie die Windows-Registrierungsseiten eingerichtet haben, sollten Sie sich informieren, wie Sie Windows-Geräte verwalten. Weitere Informationen finden Sie unter [Was ist die Microsoft Intune-Geräteverwaltung?](../remote-actions/device-management.md).
