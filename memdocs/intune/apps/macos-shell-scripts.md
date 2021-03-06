---
title: Verwenden von Shellskripts auf macOS-Geräten in Microsoft Intune | Microsoft-Dokumentation
description: In diesem Artikel erfahren Sie mehr über das Erstellen, Zuweisen und Überwachen von sowie das Behandeln von Problemen mit Shellskripts für macOS-Geräte in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36b85fa6713af5679e59382efaeb354bb4949705
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990588"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune"></a>Verwenden von Shellskripts auf macOS-Geräten in Intune

Verwenden Sie Shellskripts, um Funktionen zur Geräteverwaltung in Intune über die vom macOS-Betriebssystem unterstützten Funktionen hinaus zu erweitern. 

## <a name="prerequisites"></a>Voraussetzungen
Stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind, wenn Sie Shellskripts erstellen und macOS-Geräten zuweisen. 
 - Auf den Geräten wird macOS 10.12 oder höher ausgeführt.
 - Die Geräte werden von Intune verwaltet. 
 - Die Shellskripts beginnen mit `#!` und müssen sich an einem gültigen Speicherort befinden, z. B. `#!/bin/sh` oder `#!/usr/bin/env zsh`.
 - Für die betreffenden Shells sind Befehlszeileninterpreter installiert.

## <a name="important-considerations-before-using-shell-scripts"></a>Wichtige Überlegungen vor der Verwendung von Shellskripts
 - Für die Verwendung von Shellskripts ist eine erfolgreiche Installation des Verwaltungs-Agents von Microsoft Intune auf dem macOS-Gerät erforderlich. Weitere Informationen finden Sie unter [MDM-Agent von Microsoft Intune für macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Shellskripts werden auf Geräten als separate Prozesse parallel ausgeführt.
 - Shellskripts, die als angemeldeter Benutzer ausgeführt werden, werden für alle zum Zeitpunkt der Durchführung auf dem Gerät angemeldeten Benutzerkonten ausgeführt.
 - Ein Endbenutzer muss sich beim Gerät anmelden, um Skripts auszuführen, die als angemeldeter Benutzer ausgeführt werden.
 - Wenn das Skript erfordert, dass Änderungen vorgenommen werden, die ein Standardbenutzer nicht vornehmen darf, werden Root-Benutzerberechtigungen benötigt.
 - Shellskripts werden unter bestimmten Bedingungen versuchen, häufiger ausgeführt zu werden als durch die Häufigkeit der Skriptausführung festgelegt. Dies gilt beispielsweise, wenn der Datenträger voll ist, der Speicherort manipuliert wurde, der lokale Cache gelöscht wurde oder das macOS-Gerät neu gestartet wird.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Erstellen und Zuweisen einer Shellskriptrichtlinie
1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Klicken Sie auf **Geräte** > **macOS** > **Skripts** > **Hinzufügen**.
3. Geben Sie unter **Basics** (Grundlegende Einstellungen) die folgenden Eigenschaften ein, und klicken Sie auf **Weiter**:
   - **Name:** Geben Sie einen Namen für das Shellskript ein.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Shellskript ein. Diese Einstellung ist optional, wird jedoch empfohlen.
4. Geben Sie unter **Skripteinstellungen** die folgenden Eigenschaften ein, und klicken Sie auf **Weiter**:
   - **Skript hochladen:** Navigieren Sie zum Shellskript. Die Skriptdatei muss kleiner als 200 KB sein.
   - **Skript als angemeldeter Benutzer ausführen:** Klicken Sie auf **Ja**, um das Skript mit den Anmeldeinformationen des Benutzers auf dem Gerät auszuführen. Klicken Sie auf **Nein** (Standardeinstellung), um das Skript als Root-Benutzer auszuführen. 
   - **Skriptbenachrichtigungen auf Geräten ausblenden**: Standardmäßig werden für jedes Skript, das ausgeführt wird, Skriptbenachrichtigungen angezeigt. Endbenutzern wird eine Benachrichtigung *IT konfiguriert Ihren Computer* von Intune auf macOS-Geräten angezeigt.
   - **Häufigkeit der Skriptausführung**: Wählen Sie aus, wie oft das Skript ausgeführt werden soll. Wählen Sie **Nicht konfiguriert** (Standard) aus, um ein Skript nur einmal auszuführen.
   - **Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern**: Wählen Sie aus, wie oft das Skript ausgeführt werden soll, wenn es einen Exitcode ungleich 0 (null) zurückgibt (null steht für Erfolg). Wählen Sie **Nicht konfiguriert** (Standard) aus, um ein Skript nicht erneut auszuführen, wenn bei der Ausführung ein Fehler auftritt.
5. Fügen Sie unter **Bereichsmarkierungen** optional Bereichsmarkierungen für das Skript hinzu, und klicken Sie auf **Weiter**. Sie können Bereichsmarkierungen verwenden, um zu bestimmen, wer Skripts in Intune anzeigen kann. Ausführliche Informationen zu Bereichsmarkierungen finden Sie unter [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Verwenden der rollenbasierten Zugriffssteuerung und von Bereichsmarkierungen für verteilte IT).
6. Klicken Sie auf **Zuweisungen** > **Select groups to include** (Gruppen auswählen, die hinzugefügt werden sollen). Dann wird eine vorhandene Liste mit Azure AD Gruppen angezeigt. Wählen Sie mindestens eine Benutzer- oder Gerätegruppe aus, die das Skript erhalten soll. Klicken Sie auf **Auswählen**. Die Gruppen, die Sie ausgewählt haben, werden in der Liste angezeigt und Ihrer Skriptrichtlinie zugeordnet.
   > [!NOTE]
   > - Benutzergruppen zugewiesene Shellskripts gelten für alle Benutzer, die sich beim Mac anmelden.  
   > - Beim Aktualisieren von Zuweisungen für Shellskripts werden auch die Zuweisungen für den [MDM-Agent von Microsoft Intune für macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos) aktualisiert.

7. Unter **Überprüfen + hinzufügen** wird eine Zusammenfassung der Einstellungen angezeigt, die Sie konfiguriert haben. Klicken Sie auf **Hinzufügen**, um das Skript zu speichern. Wenn Sie auf **Hinzufügen** klicken, wird die Skriptrichtlinie für die ausgewählten Gruppen bereitgestellt.

Das von Ihnen erstellte Skript wird nun in der Liste von Skripts angezeigt. 

## <a name="monitor-a-shell-script-policy"></a>Überwachen einer Shellskriptrichtlinie
Sie können den Ausführungsstatus aller zugewiesenen Skripts für Benutzer und Geräte überwachen, indem Sie einen der folgenden Berichte auswählen:
- **Skripts** > **zu überwachendes Skript auswählen** > **Gerätestatus**
- **Skripts** > **zu überwachendes Skript auswählen** > **Benutzerstatus**

>[!IMPORTANT]
> Unabhängig von der ausgewählten **Häufigkeit der Skriptausführung** wird der Status der Skriptausführung nur beim ersten Ausführen eines Skripts gemeldet. Der Status der Skriptausführung wird bei nachfolgenden Ausführungen nicht aktualisiert. Aktualisierte Skripts werden jedoch als neue Skripts behandelt und melden den Ausführungsstatus noch mal.

Wenn ein Skript ausgeführt wird, gibt es einen der folgenden Status zurück:
- Der Skriptausführungsstatus **Fehlerhaft** gibt an, dass das Skript einen Exitcode ungleich 0 zurückgegeben hat oder das Skript falsch formatiert ist. 
- Der Skriptausführungsstatus **Erfolgreich** gibt an, dass das Skript 0 als Exitcode zurückgegeben hat. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Behandeln von Problemen mit macOS-Shellskriptrichtlinien mithilfe einer Protokollsammlung

Sie können Geräteprotokolle sammeln, um bei der Behandlung von Skriptproblemen auf macOS-Geräten zu helfen. 

### <a name="requirements-for-log-collection"></a>Anforderungen an die Protokollsammlung
Die folgenden Elemente sind erforderlich, um Protokolle auf einem macOS-Gerät zu sammeln:
- Sie müssen den vollständigen absoluten Pfad der Protokolldatei angeben.
- Dateipfade dürfen nur durch ein Semikolon (;) getrennt werden.
- Die maximale Größe der hochzuladenden Protokollsammlung beträgt 60 MB (komprimiert) oder 25 Dateien, je nachdem, was zuerst eintritt.
- Zu den Dateitypen, die für die Protokollsammlung zulässig sind, gehören die folgenden Erweiterungen *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*

#### <a name="collect-device-logs"></a>Erfassen von Geräteprotokollen
1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie im Bericht **Gerätestatus** oder **Benutzerstatus** ein Gerät aus.
3. Wählen Sie **Protokolle sammeln** aus, geben Sie Ordnerpfade von Protokolldateien an, die nur durch ein Semikolon (;) ohne Leerzeichen oder Zeilenvorschübe zwischen den Pfaden getrennt sind.<br>Beispielsweise sollten mehrere Pfade als `/Path/to/logfile1.zip;/Path/to/logfile2.log` geschrieben werden. 

   >[!IMPORTANT]
   > Mehrere Protokolldateipfade, die durch Komma, Punkt, Zeilenvorschub oder Anführungszeichen mit oder ohne Leerzeichen getrennt sind, führen zu Fehlern bei der Protokollsammlung. Leerzeichen sind auch als Trennzeichen zwischen Pfaden nicht zulässig.

4. Klicken Sie auf **OK**. Protokolle werden gesammelt, wenn der Verwaltungs-Agent von Intune auf dem Gerät das nächste Mal bei Intune eincheckt. Dieser Check-In erfolgt in der Regel alle acht Stunden.

   >[!NOTE]
   > 
   > - Gesammelte Protokolle werden auf dem Gerät verschlüsselt, übermittelt und in Microsoft Azure Storage für 30 Tage gespeichert. Gespeicherte Protokolle werden bei Bedarf entschlüsselt und über das Microsoft Endpoint Manager Admin Center heruntergeladen.
   > - Zusätzlich zu den vom Administrator angegebenen Protokollen werden auch die Protokolle des Verwaltungs-Agents von Intune in diesen Ordnern gesammelt: `/Library/Logs/Microsoft/Intune` und `~/Library/Logs/Microsoft/Intune`. Die Namen der Agent-Protokolldateien lauten `IntuneMDMDaemon date--time.log` und `IntuneMDMAgent date--time.log`. 
   > - Wenn eine vom Administrator angegebene Datei fehlt oder die falsche Dateierweiterung aufweist, sind diese Dateinamen unter `LogCollectionInfo.txt` aufgelistet.     

### <a name="log-collection-errors"></a>Fehler bei der Protokollsammlung
Die Protokollsammlung kann aus einem der folgenden Gründe, die in der nachstehenden Tabelle aufgeführt sind, nicht erfolgreich sein. Befolgen Sie zur Behebung dieser Fehler die Schritte zur Bereinigung.

| Fehlercode (Hex) | Fehlercode (Dez) | Fehlermeldung | Schritte zur Bereinigung |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Die Größe der Protokolldatei darf 60 MB nicht überschreiten. | Stellen Sie sicher, dass komprimierte Protokolle kleiner als 60 MB sind. |
| 0X87D300D1 | 2016214831 | Der angegebene Protokolldateipfad muss vorhanden sein. Der Systembenutzerordner ist ein ungültiger Speicherort für Protokolldateien. | Stellen Sie sicher, dass der angegebene Dateipfad gültig und zugänglich ist. |
| 0X87D300D2 | 2016214830 | Fehler beim Upload der Protokollsammlungsdatei, weil die Upload-URL abgelaufen ist. | Wiederholen Sie die Aktion **Protokolle sammeln**. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Fehler beim Upload der Protokollsammlungsdatei aufgrund eines Verschlüsselungsfehlers. Wiederholen Sie den Protokollupload. | Wiederholen Sie die Aktion **Protokolle sammeln**. |
| | 2016214828 | Die Anzahl von Protokolldateien hat den zulässigen Grenzwert von 25 Dateien überschritten. | Es können nur bis zu 25 Protokolldateien gleichzeitig gesammelt werden. |
| 0X87D300D6 | 2016214826 | Fehler beim Upload der Protokollsammlungsdatei aufgrund eines ZIP-Fehlers. Wiederholen Sie den Protokollupload. | Wiederholen Sie die Aktion **Protokolle sammeln**. |
| | 2016214740 | Die Protokolle konnten nicht verschlüsselt werden, weil keine komprimierten Protokolle gefunden wurden. | Wiederholen Sie die Aktion **Protokolle sammeln**. |
| | 2016214739 | Die Protokolle wurden gesammelt, konnten jedoch nicht gespeichert werden. | Wiederholen Sie die Aktion **Protokolle sammeln**. |

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Warum werden zugewiesene Shellskripts auf dem Gerät nicht ausgeführt?
Hierfür kann es mehrere Gründe geben:
* Der Agent muss möglicherweise einchecken, um neue oder aktualisierte Skripts zu erhalten. Dieser Check-In-Vorgang erfolgt alle 8 Stunden und unterscheidet sich vom MDM-Check-In. Stellen Sie für einen erfolgreichen Check-In des Agents sicher, dass das Gerät aktiv und mit einem Netzwerk verbunden ist, und warten Sie, bis der Agent eingecheckt wurde. Sie können vom Endbenutzer auch verlangen, das Unternehmensportal auf dem Mac zu öffnen, das Gerät auszuwählen und auf **Einstellungen überprüfen** zu klicken.
* Der Agent ist möglicherweise nicht installiert. Vergewissern Sie sich, dass der Agent unter `/Library/Intune/Microsoft Intune Agent.app` auf dem macOS-Gerät installiert ist.
* Der Agent befindet sich möglicherweise nicht in einem fehlerfreien Zustand. Der Agent versucht 24 Stunden lang sich wiederherzustellen, entfernt sich selbst und installiert sich neu, falls immer noch Shellskripts zugewiesen sind.

### <a name="how-frequently-is-script-run-status-reported"></a>Wie häufig wird der Skriptausführungsstatus gemeldet?
Der Skriptausführungsstatus wird an die Microsoft Endpoint Manager-Verwaltungskonsole gemeldet, sobald die Skriptausführung abgeschlossen ist. Wenn ein Skript regelmäßig mit einer festgelegten Häufigkeit ausgeführt wird, wird der Status nur bei der ersten Ausführung gemeldet.

### <a name="when-are-shell-scripts-run-again"></a>Wann werden Shellskripts noch mal ausgeführt?
Ein Skript wird nur dann noch mal ausgeführt, wenn die Einstellung **Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern** konfiguriert ist und ein Fehler bei der Skriptausführung auftritt. Wenn die Einstellung **Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern** nicht konfiguriert ist und bei einer Skriptausführung ein Fehler auftritt, wird dieses nicht noch mal ausgeführt, und der Status der Ausführung wird als **Fehlerhaft** gemeldet. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Welche Intune-Rollenberechtigungen sind für Shellskripts erforderlich?
Die zugewiesene Intune-Rolle erfordert Berechtigungen zur **Gerätekonfiguration** zum Löschen, Zuweisen, Erstellen, Aktualisieren oder Lesen von Shellskripts.

## <a name="microsoft-intune-management-agent-for-macos"></a>Verwaltungs-Agent von Microsoft Intune für macOS
 ### <a name="why-is-the-agent-required"></a>Warum ist der Agent erforderlich?
Der Verwaltungs-Agent von Microsoft Intune muss auf verwalteten macOS-Geräten installiert werden, um erweiterte Funktionen für die Geräteverwaltung zu aktivieren, die vom nativen macOS-Betriebssystem nicht unterstützt werden.
 
 ### <a name="how-is-the-agent-installed"></a>Wie wird der Agent installiert?
 Der Agent wird automatisch im Hintergrund auf von Intune verwalteten macOS-Geräten installiert, denen Sie im Microsoft Endpoint Manager Admin Center mindestens ein Shellskript zuweisen. Der Agent wird auf macOS-Geräten ggf. unter `/Library/Intune/Microsoft Intune Agent.app` installiert und nicht unter **Finder** > **Anwendungen** angezeigt. Der Agent wird bei der Ausführung auf macOS-Geräten als `IntuneMdmAgent` im **Aktivitätsmonitor** angezeigt.

### <a name="what-does-the-agent-do"></a>Welche Funktion hat der Agent?
 - Der Agent wird im Hintergrund bei Intune-Diensten authentifiziert, bevor er eincheckt, um zugewiesene Shellskripts für das macOS-Gerät zu empfangen.
 - Der Agent empfängt zugewiesene Shellskripts und führt die Skripts basierend auf dem konfigurierten Zeitplan, den Wiederholungsversuchen, den Benachrichtigungseinstellungen und anderen Einstellungen aus, die vom Administrator festgelegt werden.
 - Der Agent überprüft die Intune-Dienste in der Regel alle 8 Stunden auf neue oder aktualisierte Skripts. Dieser Check-In-Vorgang ist unabhängig vom MDM-Check-In. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Wie kann ich ein Agent-Einchecken manuell von einem Mac aus initiieren?
Öffnen Sie auf einem verwalteten Mac, auf dem der Agent installiert ist, das **Unternehmensportal**, wählen Sie das lokale Gerät aus, und klicken Sie auf **Einstellungen überprüfen**. Dadurch wird ein MDM-Check-In sowie ein Agent-Check-In initiiert.

Öffnen Sie alternativ das **Terminal**, und führen Sie den Befehl `sudo killall IntuneMdmAgent` aus, um den `IntuneMdmAgent`-Prozess zu beenden. Der `IntuneMdmAgent`-Prozess wird sofort neu gestartet, wodurch ein Einchecken mit Intune initiiert wird.

> [!NOTE]
> Mit der Aktion **Synchronisieren** für Geräte in der Microsoft Endpoint Manager-Verwaltungskonsole wird ein MDM-Check-In initiiert, und ein Agent-Check-In wird nicht erzwungen.

 ### <a name="when-is-the-agent-removed"></a>Wann wird der Agent entfernt?
 Es gibt mehrere Bedingungen, die dazu führen können, dass der Agent vom Gerät entfernt wird, z. B.:
 - Dem Gerät werden keine Shellskripts mehr zugewiesen. 
 - Das macOS-Gerät wird nicht mehr verwaltet.
 - Der Agent befindet sich länger als 24 Stunden (Aktivzeit des Geräts) in einem nicht wiederherstellbaren Zustand.

 ### <a name="why-are-scripts-running-even-though-the-mac-is-no-longer-managed"></a>Warum werden Skripts ausgeführt, obwohl der Mac nicht mehr verwaltet wird?
 Wenn ein Mac mit zugewiesenen Skripts nicht mehr verwaltet wird, wird der Agent nicht sofort entfernt. Der Agent erkennt beim nächsten Agent-Check-In (normalerweise alle 8 Stunden), dass der Mac nicht verwaltet wird, und bricht geplante Skriptausführungen ab. Alle lokal gespeicherten Skripts, die für eine häufigere Ausführung als das nächste geplante Agent-Check-In geplant sind, werden also ausgeführt. Wenn der Agent nicht einchecken kann, führt er bis zu 24 Stunden lang (Aktivzeit des Geräts) Wiederholungsversuche durch und entfernt sich dann vom Mac.
 
 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Wie werden die an Microsoft gesendeten Nutzungsdaten für Shellskripts deaktiviert?
 Zum Deaktivieren der vom Verwaltungs-Agent von Intune an Microsoft gesendeten Nutzungsdaten öffnen Sie das Unternehmensportal, klicken auf **Menü** > **Einstellungen** >  *und deaktivieren die Option „Erlauben Sie Microsoft die Erfassung von Nutzungsdaten“* . Dadurch werden die sowohl für den Agent als auch für das Unternehmensportal gesendeten Nutzungsdaten deaktiviert.

## <a name="known-issues"></a>Bekannte Probleme
- **Kein Skriptausführungsstatus:** Im unwahrscheinlichen Fall, dass ein Skript auf dem Gerät empfangen wird und das Gerät offline geschaltet wird, bevor der Ausführungsstatus gemeldet wird, meldet das Gerät den Ausführungsstatus des Skripts nicht in der Verwaltungskonsole.

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen einer Konformitätsrichtlinie in Microsoft Intune](..\protect\create-compliance-policy.md)
