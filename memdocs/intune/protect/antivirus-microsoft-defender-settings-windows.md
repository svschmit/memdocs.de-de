---
title: 'Windows 10: Virenschutzrichtlinien-Einstellungen für Microsoft Defender Antivirus für Intune | Microsoft-Dokumentation'
description: Hier finden Sie eine Liste der Einstellungen im Microsoft Defender Antivirus-Profil für Windows 10. Sie können diese Einstellungen im Rahmen der Virenschutzrichtlinie für Endpunktsicherheit in Microsoft Intune konfigurieren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: 0eae6837ff2ef1d8b2e47118a20d4aa4e6b0f22b
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461282"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Einstellungen für die Microsoft Defender Antivirus-Richtlinie unter Windows 10 in Microsoft Intune

Zeigen Sie die Virenschutzrichtlinien-Einstellungen für Endpunktsicherheit an, die Sie für das Microsoft Defender Antivirus-Profil für Windows 10 in Microsoft Intune als Teil einer [Endpunktsicherheitsrichtlinie](../protect/endpoint-security-policy.md) konfigurieren können.

## <a name="cloud-protection"></a>Cloudschutz

- **Von der Cloud bereitgestellten Schutz aktivieren**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standardmäßig sendet Defender auf Windows 10-Desktop-Geräten Informationen zu allen gefundenen Problemen an Microsoft. Microsoft analysiert diese Informationen, um mehr über die Probleme zu erfahren, die Sie und andere Kunden betreffen, und dann verbesserte Lösungen anzubieten.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Der von der Cloud bereitgestellte Schutz ist aktiviert.  Gerätebenutzer können diese Einstellung nicht ändern.

- **Von der Cloud bereitgestellte Schutzebene**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Konfigurieren Sie, wie aggressiv Defender Antivirus beim Blockieren und Überprüfen verdächtiger Dateien vorgehen soll.
  - **Nicht konfiguriert** (*Standardeinstellung*): Standardmäßige Blockierungsebene von Defender.
  - **Hoch**: Unbekannte Dateien werden aggressiv blockiert, gleichzeitig wird die Clientleistung optimiert. Dies beinhaltet eine höhere Wahrscheinlichkeit falsch positiver Ergebnisse.
  - **Hoher Zuwachs**: Unbekannte Dateien werden aggressiv blockiert, und es werden zusätzliche Schutzmaßnahmen angewendet, die möglicherweise die Clientleistung beeinträchtigen.
  - **Keine Toleranz**: Alle unbekannten ausführbaren Dateien werden blockiert.

- **Defender: Erweitertes Timeout für Cloud in Sekunden**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blockiert verdächtige Dateien automatisch 10 Sekunden lang, um die Dateien in der Cloud zu überprüfen und sicherzustellen, dass sie sicher sind. Bei dieser Einstellung können Sie dieses Timeout um 50 Sekunden verlängern.

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender Antivirus-Ausschlüsse

Sie können jede Einstellung in dieser Gruppe erweitern, **Hinzufügen** auswählen und einen Wert für den Ausschluss angeben.

- **Defender: auszuschließende Prozesse**  
  CSP: [ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Geben Sie eine Liste mit von Prozessen geöffneten Dateien an, die während einer Überprüfung ignoriert werden sollen. Der Prozess selbst wird nicht von der Überprüfung ausgeschlossen.

- **Dateierweiterungen, die bei Überprüfungen und Echtzeitschutz ausgeschlossen werden sollen**  
  CSP: [ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Geben Sie eine Liste mit Dateityperweiterungen an, die während einer Überprüfung ignoriert werden sollen.

- **Defender: auszuschließende Dateien und Ordner**  
  CSP: [ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Geben Sie eine Liste mit Dateien und Verzeichnispfaden an, die während einer Überprüfung ignoriert werden sollen.

## <a name="real-time-protection"></a>Echtzeitschutz

- **Echtzeitschutz aktivieren**  
  CSP: [AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Hiermit fordern Sie an, dass Defender auf Windows 10-Desktop-Geräten die Funktion der Echtzeitüberwachung verwenden muss.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Die Verwendung der Echtzeitüberwachung wird erzwungen. Gerätebenutzer können diese Einstellung nicht ändern.

- **Zugriffsschutz aktivieren**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Konfigurieren Sie einen Virenschutz, der im Gegensatz zum bedarfsgesteuerten Schutz kontinuierlich aktiv ist.

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Richtlinie ändert den Status dieser Einstellung auf einem Gerät nicht. Der vorhandene Status auf dem Gerät bleibt unverändert.
  - **Nein**: Blockiert den Zugriffsschutz auf Geräten. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Zugriffsschutz ist auf Geräten aktiv.

- **Überwachung für eingehende und ausgehende Dateien**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Konfigurieren Sie diese Einstellung, um festzulegen, welche NTFS-Datei- und Programmaktivität überwacht werden soll.
  - **Alle Dateien überwachen** (*Standardeinstellung*)
  - **Nur eingehende Dateien überwachen**
  - **Nur ausgehende Dateien überwachen**

- **Verhaltensüberwachung aktivieren**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Standardmäßig verwendet Defender auf Windows 10-Desktop-Geräten die Funktion der Verhaltensüberwachung.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Die Verwendung der Echtzeit-Verhaltensüberwachung wird erzwungen. Gerätebenutzer können diese Einstellung nicht ändern.

- **Netzwerkschutz aktivieren**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Schützen Sie Gerätebenutzer, die eine beliebige App verwenden, vor betrügerischen Phishing-Versuchen, Websites mit Exploits und schädlichen Inhalten im Internet. Dieser Schutz verhindert auch, dass Browser von Drittanbietern Verbindungen mit gefährlichen Websites herstellen.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Der Netzwerkschutz ist aktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **Alle heruntergeladenen Dateien und Anlagen überprüfen**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Konfigurieren Sie Defender so, dass alle heruntergeladenen Dateien und Anlagen überprüft werden.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Defender überprüft alle heruntergeladenen Dateien und Anlagen. Gerätebenutzer können diese Einstellung nicht ändern.

- **In Microsoft-Browsern verwendete Skripts überprüfen**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Konfigurieren Sie Defender für die Überprüfung von Skripts.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Defender überprüft Skripts. Gerätebenutzer können diese Einstellung nicht ändern.

- **Netzwerkdateien überprüfen**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Konfigurieren Sie Defender für die Überprüfung von Netzwerkdateien.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Die Überprüfung von Netzwerkdateien ist aktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **E-Mails überprüfen**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Konfigurieren Sie Defender für die Überprüfung von eingehenden E-Mails.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Die E-Mail-Überprüfung ist aktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

## <a name="remediation"></a>Wartung

- **Anzahl von Tagen (0–90) zum Aufbewahren der unter Quarantäne gestellten Schadsoftware**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Geben Sie an, für wie viele Tage – von 0 bis 90 – das System unter Quarantäne gestellte Elemente speichern soll, bevor sie automatisch entfernt werden. Bei Angabe des Werts 0 verbleiben Elemente in der Quarantäne und werden nicht automatisch entfernt.

- **Zustimmung für Stichproben senden**  

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Sichere Beispiele automatisch senden**
  - **Immer bestätigen**
  - **Nie senden**
  - **Alle Beispiele automatisch senden**

- **Aktion für potenziell unerwünschte Apps**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Geben Sie den Erkennungsgrad für potenziell unerwünschte Anwendungen (Potentially Unwanted Applications, PUAs) an. Defender warnt Benutzer, wenn potenziell unerwünschte Software heruntergeladen oder versucht wird, solche Software auf einem Gerät zu installieren.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt, d. h. der PUA-Schutz ist deaktiviert.
  - **Deaktivieren**
  - **Aktivieren**: Erkannte Elemente werden blockiert und im Verlauf zusammen mit anderen Bedrohungen angezeigt.
  - **Überwachungsmodus**: Defender erkennt potenziell unerwünschte Anwendungen, führt aber keine Aktion aus. Sie finden Informationen zu den Anwendungen, bei denen Defender Aktionen ausgeführt hätte, indem Sie nach Ereignissen suchen, die von Defender in der Ereignisanzeige erstellt wurden.

- **Aktionen bei erkannten Bedrohungen**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Geben Sie die Aktion an, die Defender bei erkannter Schadsoftware basierend auf der Bedrohungsstufe der Schadsoftware ausführen soll.
  
  Defender klassifiziert erkannte Schadsoftware nach den folgenden Schweregraden:
  - **Niedriger Schweregrad**
  - **Mittlerer Schweregrad**
  - **Hoher Schweregrad**
  - **Sehr hoher Schweregrad**

  Geben Sie für jeden Schweregrad die auszuführende Aktion an. Die Standardeinstellung für alle Schweregrade lautet *Nicht konfiguriert*.

  - **Nicht konfiguriert**
  - **Bereinigen**: Der Dienst versucht, Dateien wiederherzustellen und zu desinfizieren.
  - **Quarantäne**: Dateien werden in die Quarantäne verschoben.
  - **Entfernen**: Dateien werden vom Gerät entfernt.
  - **Zulassen**: Die Datei wird zugelassen, und es werden keine weiteren Aktionen ausgeführt.
  - **Benutzerdefiniert**: Der Gerätebenutzer trifft die Entscheidung, welche Aktion ausgeführt werden soll.
  - **Blockieren**: Die Dateiausführung wird blockiert.

## <a name="scan"></a>Überprüfen

- **Archivdateien überprüfen**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Konfigurieren Sie Defender so, dass Archivdateien wie z. B. ZIP- oder CAB-Dateien überprüft werden.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. archivierte Dateien werden überprüft. Der Benutzer kann dies jedoch deaktivieren.
Erfahren Sie mehr
  - **Nein**: Dateiarchive werden nicht überprüft. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Die Überprüfung von Archivdateien wird aktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **Niedrige CPU-Priorität für geplante Überprüfungen verwenden**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Konfigurieren Sie eine niedrige CPU-Priorität für geplante Überprüfungen.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Systems zurückgesetzt, d. h. die CPU-Priorität wird nicht geändert.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Bei geplanten Überprüfungen wird eine niedrige CPU-Priorität verwendet. Gerätebenutzer können diese Einstellung nicht ändern.

- **Vollständige Aufholüberprüfung deaktivieren**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Konfigurieren Sie Aufholüberprüfungen für geplante vollständige Überprüfungen. Eine Aufholüberprüfung ist eine Überprüfung, die gestartet wird, da eine reguläre Überprüfung ausgelassen wurde. In der Regel werden diese geplanten Überprüfungen ausgelassen, weil der Computer zum geplanten Zeitpunkt ausgeschaltet war.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Aufholüberprüfungen für vollständige Überprüfungen sind aktiviert. Der Benutzer kann diese jedoch deaktivieren.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Aufholüberprüfungen für geplante vollständige Überprüfungen werden erzwungen und können vom Benutzer nicht deaktiviert werden. Wenn ein Computer bei zwei aufeinanderfolgenden geplanten Überprüfungen offline ist, wird eine Aufholüberprüfung gestartet, sobald sich der nächste Benutzer am Computer anmeldet. Wenn keine geplante Überprüfung konfiguriert wurde, werden auch keine Aufholüberprüfungen durchgeführt. Gerätebenutzer können diese Einstellung nicht ändern.

- **Schnelle Aufholüberprüfung deaktivieren**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Konfigurieren Sie Aufholüberprüfungen für geplante Schnellüberprüfungen. Eine Aufholüberprüfung ist eine Überprüfung, die gestartet wird, da eine reguläre Überprüfung ausgelassen wurde. In der Regel werden diese geplanten Überprüfungen ausgelassen, weil der Computer zum geplanten Zeitpunkt ausgeschaltet war.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Aufholüberprüfungen für Schnellüberprüfungen sind aktiviert. Der Benutzer kann diese jedoch deaktivieren.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Aufholüberprüfungen für geplante Schnellüberprüfungen werden erzwungen und können vom Benutzer nicht deaktiviert werden. Wenn ein Computer bei zwei aufeinanderfolgenden geplanten Überprüfungen offline ist, wird eine Aufholüberprüfung gestartet, sobald sich der nächste Benutzer am Computer anmeldet. Wenn keine geplante Überprüfung konfiguriert wurde, werden auch keine Aufholüberprüfungen durchgeführt. Gerätebenutzer können diese Einstellung nicht ändern.

- **CPU-Auslastungslimit pro Überprüfung**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Geben Sie den durchschnittlichen CPU-Auslastungsfaktor für die Defender-Überprüfung als Prozentwert zwischen 0 und 100 an.

- **Bei vollständiger Überprüfung zugeordnete Netzlaufwerke überprüfen**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Konfigurieren Sie Defender für die Überprüfung von zugeordneten Netzwerklaufwerken.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt, d. h. die Überprüfung auf zugeordneten Netzlaufwerken ist deaktiviert.
  - **Nein**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Ja**: Überprüfungen von zugeordneten Netzwerklaufwerken sind aktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **Tägliche Schnellüberprüfung ausführen um**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Wählen Sie die Uhrzeit aus, zu der Defender-Schnellüberprüfungen ausgeführt werden sollen.
  Die Standardeinstellung ist **Nicht konfiguriert**.

- **Überprüfungstyp**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Wählen Sie aus, welche Art von Überprüfung Defender ausführen soll.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Schnellüberprüfung**
  - **Vollständige Überprüfung**

- **Wochentag zum Ausführen einer geplanten Überprüfung**  
  - **Nicht konfiguriert** (*Standardeinstellung*)

- **Tageszeit zum Ausführen einer geplanten Überprüfung**  
  - **Nicht konfiguriert** (*Standardeinstellung*)

- **Vor dem Ausführen einer Überprüfung nach Signaturupdates suchen**  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **No**
  - **Ja**

## <a name="updates"></a>Updates

- **Eingeben, wie oft (0–24 Stunden) nach Security Intelligence-Updates gesucht wird**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Geben Sie ein Intervall zwischen 0 und 24 Stunden an, in dem nach Signaturen gesucht werden soll. Der Wert 0 führt dazu, dass nicht nach neuen Signaturen gesucht wird. Beim Wert 2 erfolgt alle zwei Stunden eine Suche usw.

- **Dateifreigaben zum Herunterladen von Definitionsupdates definieren**  
  CSP: [SignatureUpdateFallbackOrder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

  Verwalten Sie Orte, z. B. eine UNC-Dateifreigabe, als Quellort für das Herunterladen von Definitionsupdates. Wenn die Definitionsupdates erfolgreich aus einer angegebenen Quelle heruntergeladen wurden, wird mit den übrigen Quellen in der Liste keine Verbindung mehr hergestellt.

  Sie können einzelne Orte **hinzufügen** oder eine Liste mit Orten als CSV-Datei **importieren**.

- **Reihenfolge der Quellen zum Herunterladen von Definitionsupdates definieren**  
  CSP: [SignatureUpdateFileSharesSources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)

  Geben Sie die Reihenfolge an, in der eine Verbindung mit den von Ihnen angegebenen Quellorten hergestellt werden soll, um Definitionsupdates abzurufen. Wenn die Definitionsupdates erfolgreich aus einer angegebenen Quelle heruntergeladen wurden, wird mit den übrigen Quellen in der Liste keine Verbindung mehr hergestellt.

## <a name="user-experience"></a>Benutzerfreundlichkeit

- **Benutzerzugriff auf Microsoft Defender-App zulassen**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Benutzeroberfläche und Benachrichtigungen sind zulässig.
  - **Nein**: Auf die Benutzeroberfläche von Defender kann nicht zugegriffen werden, und Benachrichtigungen werden unterdrückt.
  - **Ja**

