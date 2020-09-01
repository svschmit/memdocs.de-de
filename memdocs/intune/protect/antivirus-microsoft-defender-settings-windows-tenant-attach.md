---
title: 'Windows 10: Richtlinieneinstellungen von Microsoft Defender Antivirus für mandantenbasiert angefügte Geräte | Microsoft-Dokumentation'
description: Hier finden Sie eine Liste der Einstellungen im Microsoft Defender Antivirus-Profil für Windows 10-Geräte, die von Configuration Manager verwaltet werden. Sie können diese Einstellungen im Rahmen der Antivirus-Richtlinie für die Endpunktsicherheit in Microsoft Intune konfigurieren, nachdem Sie die Mandantenanfügung für Configuration Manager konfiguriert haben.
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
ms.openlocfilehash: 966c3f21505cbbe1573abd47fb7081c5e97cc3c1
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823517"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Einstellungen für Microsoft Defender Antivirus-Richtlinien für mandantenbasiert angefügte Geräte in Microsoft Intune

Sehen Sie sich die Microsoft Defender Antivirus-Einstellungen an, die Sie über das Profil **Microsoft Defender Antivirus-Richtlinie (Configuration Manager)** in Intune verwalten können. Dieses Profil ist verfügbar, wenn Sie die [Antivirus-Richtlinie für die Endpunktsicherheit](../protect/endpoint-security-antivirus-policy.md) in Intune konfigurieren. Die Richtlinie wird auf Geräten bereitgestellt, die Sie über Configuration Manager verwalten, wenn Sie das Szenario der [Mandantenanfügung](../protect/tenant-attach-intune.md) konfiguriert haben.

## <a name="cloud-protection"></a>Cloudschutz

- **Von der Cloud bereitgestellten Schutz aktivieren**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standardmäßig sendet Defender auf Windows 10-Desktop-Geräten Informationen zu allen gefundenen Problemen an Microsoft. Microsoft analysiert diese Informationen, um mehr über die Probleme zu erfahren, die Sie und andere Kunden betreffen, und dann verbesserte Lösungen anzubieten.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.** Deaktiviert Microsoft Active Protection Service.
  - **Zugelassen**:  Aktiviert Microsoft Active Protection Service.

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
  - **Nicht zulässig.** Deaktiviert den Echtzeitüberwachungsdienst.
  - **Zugelassen**: Aktiviert den Echtzeitüberwachungsdienst und führt ihn aus.

- **Zugriffsschutz aktivieren**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Konfigurieren Sie einen Virenschutz, der im Gegensatz zum bedarfsgesteuerten Schutz kontinuierlich aktiv ist.

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Richtlinie ändert den Status dieser Einstellung auf einem Gerät nicht. Der vorhandene Status auf dem Gerät bleibt unverändert.
  - **Nicht zulässig.** Deaktiviert den Echtzeitüberwachungsdienst.
  - **Zugelassen**:

- **Überwachung für eingehende und ausgehende Dateien**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Konfigurieren Sie diese Einstellung, um festzulegen, welche NTFS-Datei- und Programmaktivität überwacht werden soll.
  - **Alle Dateien überwachen (bidirektional)** . (*Standard*)
  - **Eingehende Dateien überwachen**.
  - **Ausgehende Dateien überwachen**.

- **Verhaltensüberwachung aktivieren**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Standardmäßig verwendet Defender auf Windows 10-Desktop-Geräten die Funktion der Verhaltensüberwachung.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.** Deaktiviert die Verhaltensüberwachung.
  - **Zugelassen**: Aktiviert die Echtzeitverhaltensüberwachung.

- **Eindringschutzsystem zulassen**  
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.**
  - **Zugelassen**:

- **Alle heruntergeladenen Dateien und Anlagen überprüfen**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Konfigurieren Sie Defender so, dass alle heruntergeladenen Dateien und Anlagen überprüft werden.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.**
  - **Zugelassen**:

- **In Microsoft-Browsern verwendete Skripts überprüfen**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Konfigurieren Sie Defender für die Überprüfung von Skripts.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.**
  - **Zugelassen**:

- **Netzwerkdateien überprüfen**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Konfigurieren Sie Defender für die Überprüfung von Netzwerkdateien.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.** Deaktiviert das Überprüfen von Netzwerkdateien.
  - **Zugelassen**: Überprüft Netzwerkdateien.

- **E-Mails überprüfen**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Konfigurieren Sie Defender für die Überprüfung von eingehenden E-Mails.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Nicht zulässig.** Deaktiviert die E-Mail-Überprüfung.
  - **Zugelassen**: Aktiviert die E-Mail-Überprüfung.

## <a name="remediation"></a>Wartung

- **Anzahl von Tagen (0–90) zum Aufbewahren der unter Quarantäne gestellten Schadsoftware**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Geben Sie an, für wie viele Tage – von 0 bis 90 – das System unter Quarantäne gestellte Elemente speichern soll, bevor sie automatisch entfernt werden. Bei Angabe des Werts 0 verbleiben Elemente in der Quarantäne und werden nicht automatisch entfernt.

- **Zustimmung für Stichproben senden**  

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Immer nachfragen**.
  - **Sichere Beispiele automatisch senden**.
  - **Nie senden**.
  - **Alle Beispiele automatisch senden**.

- **Aktion für potenziell unerwünschte Apps**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Geben Sie den Erkennungsgrad für potenziell unerwünschte Anwendungen (Potentially Unwanted Applications, PUAs) an. Defender warnt Benutzer, wenn potenziell unerwünschte Software heruntergeladen oder versucht wird, solche Software auf einem Gerät zu installieren.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt, d. h. der PUA-Schutz ist deaktiviert.
  - **PUA-Schutz deaktiviert**. Windows Defender bietet keinen Schutz vor potenziell unerwünschten Anwendungen.
  - **PUA-Schutz aktiviert**. Erkannte Elemente werden blockiert. Sie werden zusammen mit anderen Bedrohungen im Verlauf angezeigt.
  - **Überwachungsmodus**. Defender erkennt potenziell unerwünschte Anwendungen, ergreift aber keine Maßnahmen. Sie finden Informationen zu den Anwendungen, bei denen Defender Aktionen ausgeführt hätte, indem Sie nach Ereignissen suchen, die von Defender in der Ereignisanzeige erstellt wurden.

- **Vor dem Bereinigen von Computern einen Systemwiederherstellungspunkt erstellen**  
  - **Ja** (*Standardeinstellung*)
  - **Nein**
  - **Nicht konfiguriert**

- **Aktionen bei erkannten Bedrohungen**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Geben Sie die Aktion an, die Defender bei erkannter Schadsoftware basierend auf der Bedrohungsstufe der Schadsoftware ausführen soll.
  
  Defender klassifiziert erkannte Schadsoftware nach den folgenden Schweregraden:
  - **Geringe Bedrohung**
  - **Mäßige Bedrohung**
  - **Hohe Bedrohung**
  - **Schwerwiegende Bedrohung**

  Geben Sie für jeden Schweregrad die auszuführende Aktion an. Die Standardeinstellung für alle Schweregrade lautet *Nicht konfiguriert*.

  - **Nicht konfiguriert** (*Standardeinstellung*)
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

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. archivierte Dateien werden überprüft. Der Benutzer kann die Überprüfung jedoch deaktivieren.
Weitere Informationen
  - **Nicht zugelassen**: Deaktiviert die Überprüfung archivierter Dateien.
  - **Zugelassen**: Überprüft die Archivdateien.

- **Niedrige CPU-Priorität für geplante Überprüfungen aktivieren**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Konfigurieren Sie eine niedrige CPU-Priorität für geplante Überprüfungen.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Systems zurückgesetzt, d. h. die CPU-Priorität wird nicht geändert.
  - **Disabled**
  - **Aktiviert**

- **Vollständige Aufholüberprüfung deaktivieren**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Konfigurieren Sie Aufholüberprüfungen für geplante vollständige Überprüfungen. Eine Aufholüberprüfung ist eine Überprüfung, die gestartet wird, weil eine regulär geplante Überprüfung ausgelassen wurde. In der Regel werden diese geplanten Überprüfungen ausgelassen, weil der Computer zum geplanten Zeitpunkt ausgeschaltet war.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Aufholüberprüfungen für vollständige Überprüfungen sind aktiviert. Der Benutzer kann diese jedoch deaktivieren.
  - **Disabled**
  - **Aktiviert**

- **Schnelle Aufholüberprüfung deaktivieren**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Konfigurieren Sie Aufholüberprüfungen für geplante Schnellüberprüfungen. Eine Aufholüberprüfung ist eine Überprüfung, die gestartet wird, weil eine regulär geplante Überprüfung ausgelassen wurde. In der Regel werden diese geplanten Überprüfungen ausgelassen, weil der Computer zum geplanten Zeitpunkt ausgeschaltet war.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Aufholüberprüfungen für Schnellüberprüfungen sind aktiviert. Der Benutzer kann diese jedoch deaktivieren.
  - **Disabled**
  - **Aktiviert**

- **CPU-Nutzungslimit (0–100 Prozent) pro Überprüfung**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Geben Sie den durchschnittlichen CPU-Auslastungsfaktor für die Defender-Überprüfung als Prozentwert zwischen 0 und 100 an.

- **Bei einer vollständigen Überprüfung auch die Überprüfung zugeordneter Netzlaufwerke aktivieren**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Konfigurieren Sie Defender für die Überprüfung von zugeordneten Netzwerklaufwerken.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt, d. h. die Überprüfung auf zugeordneten Netzlaufwerken ist deaktiviert.
  - **Nicht zulässig.** Deaktiviert die Überprüfung auf zugeordneten Netzwerklaufwerken.
  - **Zugelassen**: Überprüft zugeordnete Netzwerklaufwerke.

- **Tägliche Schnellüberprüfung ausführen um**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Wählen Sie die Uhrzeit aus, zu der Defender-Schnellüberprüfungen ausgeführt werden sollen.
  Die Standardeinstellung für diese Option ist **Nicht konfiguriert**.

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
  - **Disabled**
  - **Aktiviert**

- **Startzeiten für geplante Überprüfungen und Security Intelligence-Updates zufällig festlegen**  
  -**Nicht konfiguriert** (*Standardeinstellung*) – **Ja**
  -**Nein**

- **Bei vollständiger Überprüfung Wechseldatenträger überprüfen**
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Nicht zulässig.** Deaktiviert die Überprüfung auf Wechseldatenträgern.
  - **Zugelassen**: Überprüft Wechseldatenträger.

## <a name="updates"></a>Updates

- **Eingeben, wie oft (0–24 Stunden) nach Security Intelligence-Updates gesucht wird**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Geben Sie ein Intervall zwischen 0 und 24 Stunden an, in dem nach Signaturen gesucht werden soll. Der Wert 0 führt dazu, dass nicht nach neuen Signaturen gesucht wird. Beim Wert 2 erfolgt alle zwei Stunden eine Suche usw.

- **Fallbackreihenfolge für Signaturaktualisierung (Gerät)**

- **Dateifreigabequellen für Signaturaktualisierung (Gerät)**

- **Security Intelligence-Standort (Gerät)**  

## <a name="user-experience"></a>Benutzererfahrung

- **Benutzerzugriff auf Microsoft Defender-App blockieren**  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Nicht zulässig.** Hindert Benutzer am Zugriff auf die Benutzeroberfläche.
  - **Zugelassen**: Ermöglicht Benutzern den Zugriff auf die Benutzeroberfläche.

- **Benachrichtigungen auf dem Clientcomputer anzeigen, wenn der Benutzer eine vollständige Überprüfung ausführen, Security Intelligence aktualisieren oder Windows Defender Offline ausführen muss**  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**
  - **Nein**

- **Clientbenutzeroberfläche deaktivieren**  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**
  - **Nein**

- **Benutzern die Anzeige der vollständigen Verlaufsergebnisse erlauben**
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**
  - **Nein**