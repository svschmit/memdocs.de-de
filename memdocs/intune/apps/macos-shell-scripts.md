---
title: Verwenden von Shellskripts auf macOS-Geräten in Microsoft Intune | Microsoft-Dokumentation
description: In diesem Artikel erfahren Sie mehr über das Erstellen, Zuweisen und Überwachen von sowie das Behandeln von Problemen mit Shellskripts für macOS-Geräte in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
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
ms.openlocfilehash: ba099e3614c11e10ce4cd9ae94668a1648bfc150
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808053"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Verwenden von Shellskripts auf macOS-Geräten in Intune (Public Preview)

> [!NOTE]
> Shellskripts für macOS-Geräte befinden sich derzeit in der Vorschauphase. Überprüfen Sie die Liste der [bekannten Probleme in der Vorschauversion](macos-shell-scripts.md#known-issues), bevor Sie dieses Feature verwenden.

Verwenden Sie Shellskripts, um Funktionen zur Geräteverwaltung in Intune über die vom macOS-Betriebssystem unterstützten Funktionen hinaus zu erweitern. 

## <a name="prerequisites"></a>Voraussetzungen
Stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind, wenn Sie Shellskripts erstellen und macOS-Geräten zuweisen. 
 - Auf den Geräten wird macOS 10.12 oder höher ausgeführt.
 - Die Geräte werden von Intune verwaltet. 
 - Die Shellskripts beginnen mit `#!` und müssen sich an einem gültigen Speicherort befinden, z. B. `#!/bin/sh` oder `#!/usr/bin/env zsh`.
 - Für die betreffenden Shells sind Befehlszeileninterpreter installiert.

## <a name="important-considerations-before-using-shell-scripts"></a>Wichtige Überlegungen vor der Verwendung von Shellskripts
 - Für die Verwendung von Shellskripts ist eine erfolgreiche Installation des MDM-Agents von Microsoft Intune auf dem macOS-Gerät erforderlich. Weitere Informationen finden Sie unter [MDM-Agent von Microsoft Intune für macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
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
6. Klicken Sie auf **Zuweisungen** > **Select groups to include** (Gruppen auswählen, die hinzugefügt werden sollen). Dann wird eine vorhandene Liste mit Azure AD Gruppen angezeigt. Wählen Sie mindestens eine Gerätegruppe aus, die die Benutzer enthält, deren macOS-Geräte das Skript erhalten sollen. Klicken Sie auf **Auswählen**. Die Gruppen, die Sie ausgewählt haben, werden in der Liste angezeigt und Ihrer Skriptrichtlinie zugeordnet.
   > [!NOTE]
   > - Shellskripts in Intune können nur Azure AD-Gerätesicherheitsgruppen zugewiesen werden. Die Benutzergruppenzuweisung wird in der Vorschauversion nicht unterstützt. 
   > - Beim Aktualisieren von Zuweisungen für Shellskripts werden auch die Zuweisungen für den [MDM-Agent von Microsoft Intune für macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos) aktualisiert.
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

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Warum werden zugewiesene Shellskripts auf dem Gerät nicht ausgeführt?
Hierfür kann es mehrere Gründe geben:
* Der Agent muss möglicherweise einchecken, um neue oder aktualisierte Skripts zu erhalten. Dieser Check-In-Vorgang erfolgt alle 8 Stunden und unterscheidet sich vom MDM-Check-In. Stellen Sie für einen erfolgreichen Check-In des Agents sicher, dass das Gerät aktiv und mit einem Netzwerk verbunden ist, und warten Sie, bis der Agent eingecheckt wurde.
* Der Agent ist möglicherweise nicht installiert. Vergewissern Sie sich, dass der Agent unter `/Library/Intune/Microsoft Intune Agent.app` auf dem macOS-Gerät installiert ist.
* Der Agent befindet sich möglicherweise nicht in einem fehlerfreien Zustand. Der Agent versucht 24 Stunden lang sich wiederherzustellen, entfernt sich selbst und installiert sich neu, falls immer noch Shellskripts zugewiesen sind.

### <a name="how-frequently-is-script-run-status-reported"></a>Wie häufig wird der Skriptausführungsstatus gemeldet?
Der Skriptausführungsstatus wird an die Microsoft Endpoint Manager-Verwaltungskonsole gemeldet, sobald die Skriptausführung abgeschlossen ist. Wenn ein Skript regelmäßig mit einer festgelegten Häufigkeit ausgeführt wird, wird der Status nur bei der ersten Ausführung gemeldet.

### <a name="when-are-shell-scripts-run-again"></a>Wann werden Shellskripts noch mal ausgeführt?
Ein Skript wird nur dann noch mal ausgeführt, wenn die Einstellung **Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern** konfiguriert ist und ein Fehler bei der Skriptausführung auftritt. Wenn die Einstellung **Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern** nicht konfiguriert ist und bei einer Skriptausführung ein Fehler auftritt, wird dieses nicht noch mal ausgeführt, und der Status der Ausführung wird als **Fehlerhaft** gemeldet. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Welche Intune-Rollenberechtigungen sind für Shellskripts erforderlich?
Die zugewiesene Intune-Rolle erfordert Berechtigungen zur **Gerätekonfiguration** zum Löschen, Zuweisen, Erstellen, Aktualisieren oder Lesen von Shellskripts.

## <a name="microsoft-intune-mdm-agent-for-macos"></a>MDM-Agent von Microsoft Intune für macOS
 ### <a name="why-is-the-agent-required"></a>Warum ist der Agent erforderlich?
 Der MDM-Agent von Microsoft Intune muss auf verwalteten macOS-Geräten installiert werden, um erweiterte Funktionen für die Geräteverwaltung zu aktivieren, die vom nativen macOS-Betriebssystem nicht unterstützt werden.
 
 ### <a name="how-is-the-agent-installed"></a>Wie wird der Agent installiert?
 Der Agent wird automatisch im Hintergrund auf von Intune verwalteten macOS-Geräten installiert, denen Sie im Microsoft Endpoint Manager Admin Center mindestens ein Shellskript zuweisen. Der Agent wird auf macOS-Geräten ggf. unter `/Library/Intune/Microsoft Intune Agent.app` installiert und nicht unter **Finder** > **Anwendungen** angezeigt. Der Agent wird bei der Ausführung auf macOS-Geräten als `IntuneMdmAgent` im **Aktivitätsmonitor** angezeigt.

### <a name="what-does-the-agent-do"></a>Welche Funktion hat der Agent?
 - Der Agent wird im Hintergrund bei Intune-Diensten authentifiziert, bevor er eincheckt, um zugewiesene Shellskripts für das macOS-Gerät zu empfangen.
 - Der Agent empfängt zugewiesene Shellskripts und führt die Skripts basierend auf dem konfigurierten Zeitplan, den Wiederholungsversuchen, den Benachrichtigungseinstellungen und anderen Einstellungen aus, die vom Administrator festgelegt werden.
 - Der Agent überprüft die Intune-Dienste in der Regel alle 8 Stunden auf neue oder aktualisierte Skripts. Dieser Check-In-Vorgang ist unabhängig vom MDM-Check-In. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Wie kann ich ein Agent-Einchecken manuell von einem Mac aus initiieren?
Öffnen Sie auf einem verwalteten Mac, auf dem der Agent installiert ist, **Terminal**, und führen Sie den `sudo killall IntuneMdmAgent`-Befehl aus, um den `IntuneMdmAgent`-Prozess zu beenden. Der `IntuneMdmAgent`-Prozess wird sofort neu gestartet, wodurch ein Einchecken mit Intune initiiert wird.

Alternativ können Sie Folgendes tun:
1. **Aktivitätsmonitor** > **Ansicht** öffnen >  ***Alle Prozesse** auswählen.* 
2. Suchen Sie nach Prozessen mit dem Namen `IntuneMdmAgent`. 
3. Beenden Sie den Prozess, der für **Root-Benutzer** ausgeführt wird. 

> [!NOTE]
> Mit der Aktion **Einstellungen überprüfen** im Unternehmensportal und der Aktion **Synchronisierung** für Geräte in der Microsoft Endpoint Manager-Verwaltungskonsole wird ein MDM-Einchecken initiiert, und ein Agent-Einchecken wird nicht erzwungen.

 ### <a name="when-is-the-agent-removed"></a>Wann wird der Agent entfernt?
 Es gibt mehrere Bedingungen, die dazu führen können, dass der Agent vom Gerät entfernt wird, z. B.:
 - Dem Gerät werden keine Shellskripts mehr zugewiesen. 
 - Das macOS-Gerät wird nicht mehr verwaltet.
 - Der Agent befindet sich länger als 24 Stunden (Aktivzeit des Geräts) in einem nicht wiederherstellbaren Zustand.

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Wie werden die an Microsoft gesendeten Nutzungsdaten für Shellskripts deaktiviert?
 Zum Deaktivieren der vom MDM-Agent von Intune an Microsoft gesendeten Nutzungsdaten öffnen Sie das Unternehmensportal, klicken auf **Menü** > **Einstellungen** >  *und deaktivieren die Option „Erlauben Sie Microsoft die Erfassung von Nutzungsdaten“* . Dadurch werden die sowohl für den MDM-Agent von Intune als auch für das Unternehmensportal gesendeten Nutzungsdaten deaktiviert.

## <a name="known-issues"></a>Bekannte Probleme
- **Benutzergruppenzuweisung:** Benutzergruppen zugewiesene Shellskripts gelten nicht für Geräte. Die Zuweisung von Benutzergruppen wird in der Vorschauversion derzeit nicht unterstützt. Verwenden Sie die Gerätegruppenzuweisung, um Skripts zuzuweisen.
- **Protokolle sammeln:** Die Aktion „Protokolle sammeln“ ist sichtbar. Wird jedoch der Versuch einer Protokollsammlung gestartet, wird die Meldung „Es ist ein Fehler aufgetreten“ angezeigt, und es werden keine Protokolle erfasst. Die Protokollsammlung wird in der Vorschauversion derzeit nicht unterstützt.
- **Kein Skriptausführungsstatus:** Im unwahrscheinlichen Fall, dass ein Skript auf dem Gerät empfangen wird und das Gerät offline geschaltet wird, bevor der Ausführungsstatus gemeldet wird, meldet das Gerät den Ausführungsstatus des Skripts nicht in der Verwaltungskonsole.
- **Benutzerstatusbericht:** Es ist ein Problem mit einem leeren Bericht aufgetreten. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Überwachen**. Der Benutzerstatus zeigt einen leeren Bericht an.

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen einer Konformitätsrichtlinie in Microsoft Intune](..\protect\create-compliance-policy.md)
