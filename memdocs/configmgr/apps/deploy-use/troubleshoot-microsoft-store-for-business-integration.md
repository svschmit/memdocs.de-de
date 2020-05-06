---
title: Behandeln von Problemen bei der Integration von Microsoft Store für Unternehmen
titleSuffix: Configuration Manager
description: Bietet Vorschläge und Lösungen zur Behandlung einiger der häufigsten Probleme bei der Integration von Microsoft Store für Unternehmen und Bildungseinrichtungen.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149119"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Behandeln von Problemen bei der Integration des Microsoft Store für Unternehmen und Bildungseinrichtungen in Configuration Manager

Dieser Artikel enthält wichtige Tipps zur Problembehandlung und Korrekturen für einige der wichtigsten Probleme, die bei der Integration von Microsoft Store für Unternehmen und Bildungseinrichtungen (MSfB) mit Configuration Manager auftreten können.

Weitere Informationen zur Verwendung von Microsoft Store für Unternehmen und Bildungseinrichtungen mit Configuration Manager finden Sie unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen mit Configuration Manager](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>Überwachen

### <a name="component-status"></a>Komponentenstatus

Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie den **Systemstatus**, und wählen Sie den Knoten **Komponentenstatus** aus. Überwachen Sie den Status der folgenden Komponenten:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Synchronisierungsstatus

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Microsoft Store für Unternehmen** aus. Überprüfen Sie die Spalte **Letzter Synchronisierungsstatus**.

### <a name="view-synchronized-apps"></a>Anzeigen synchronisierter Apps

Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsmanagement**, und wählen Sie anschließend den Knoten **Lizenzinformationen für Store-Apps** aus.


## <a name="log-files"></a>Protokolldateien

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

Diese Protokolldatei befindet sich auf dem Dienstverbindungspunkt unter `\Logs` im Installationsverzeichnis von Configuration Manager. Sie zeichnet Informationen über die Kommunikation mit dem Clouddienst auf. Diese Informationen umfassen Metadaten, Symbole, Pakete und den Abruf von Lizenzdateien.

Ändern Sie die Protokollebene, indem Sie im Registrierungsschlüssel `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` den Wert `LoggingLevel` in `0` ändern. Weitere Informationen finden Sie unter [Konfigurieren von Protokollierungsoptionen](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

Diese Protokolldatei befindet sich auf dem Dienstverbindungspunkt unter `\Logs` im Installationsverzeichnis von Configuration Manager. Wenn der WSfBSyncWorker-Dienst nicht gestartet wird oder wiederholt startet und beendet wird, überprüfen Sie die Einträge in dieser Protokolldatei.

> [!NOTE]
> Diese Protokolldatei wird mit anderen Features gemeinsam genutzt.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

Diese Protokolldatei befindet sich auf dem Standortserver für den Standort der obersten Ebene in der Hierarchie. Sie befindet sich unter `\Logs` im Installationsverzeichnis von Configuration Manager. Sie zeichnet Informationen zu folgenden Prozessen auf:

- Einfügen der von der BusinessAppProcessWorker-Komponente synchronisierten Metadateninformationen in die Datenbank
- Verarbeiten von Dateien in `\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

Diese Protokolldatei befindet sich auf dem Standortserver für den Standort der obersten Ebene in der Hierarchie. Sie befindet sich unter `\Logs` im Installationsverzeichnis von Configuration Manager. Wenn der BusinessAppProcessWorker-Dienst nicht gestartet wird oder wiederholt startet und beendet wird, überprüfen Sie die Einträge in dieser Protokolldatei.



## <a name="last-sync-failed"></a>Fehler bei der letzten Synchronisierung

Wenn der letzte Synchronisierungsstatus *Fehler* ist, beginnen Sie mit der Überprüfung der folgenden [Protokolldateien](#log-files), um das Symptom zu identifizieren:

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Suchen Sie dann in einem der folgenden Abschnitte nach allgemeinen Problemen:

- [Autorisierungsfehler](#bkmk_fail-symptom1)
- [Der geheime Schlüssel ist ungültig](#bkmk_fail-symptom2)
- [Fehler beim Abrufen des Anwendungstokens](#bkmk_fail-symptom3)
- [Speicherort des Inhalts ist nicht vorhanden oder es fehlen Berechtigungen](#bkmk_fail-symptom4)
- [Fehler beim Aufrufen der GET-Methode durch die HTTP-Anforderung](#bkmk_fail-symptom5)
- [Es können keine weiteren Bytes in den Puffer geschrieben werden](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a> Autorisierungsfehler

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn die konfigurierte Azure Active Directory-Anwendung (Azure AD) keine Berechtigungen zur Verwaltung des Microsoft Store für Unternehmen und Bildungseinrichtungen für diesen Mandanten besitzt.

#### <a name="workaround"></a>Problemumgehung

1. Melden Sie sich als Administrator am Portal für den Microsoft Store für Unternehmen und Bildungseinrichtungen an.
1. Wechseln Sie zu **Einstellungen**, und wählen Sie **Verwaltungstools** aus.
1. Wenn die Anwendung nicht aufgeführt ist, wählen Sie **Verwaltungstool hinzufügen** aus. Suchen Sie dann nach dem Namen, und wählen Sie die Azure AD-Anwendung aus, die derselben ClientID wie Configuration Manager zugeordnet ist.
1. Wenn der Status nicht **Aktiv** anzeigt, wählen Sie **Aktivieren** im Abschnitt **Aktion** aus.
1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Microsoft Store für Unternehmen** aus. Führen Sie die Synchronisierung mit dem Store durch, oder warten Sie auf das nächste Synchronisierungsintervall.

> [!Tip]
> So finden Sie die ClientID in Configuration Manager
>
> 1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Clouddienste**, und wählen Sie den Knoten **Azure Active Directory-Mandanten** aus.
> 1. Wählen Sie den Mandanten aus, den Sie für die Integration von Microsoft Store für Unternehmen und Bildungseinrichtungen verwenden.
> 1. Suchen Sie im Ergebnisbereich die passende Anwendung aus, und betrachten Sie die Spalte **Client-ID**.

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a> Der geheime Schlüssel ist ungültig

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn der geheime Schlüssel in der Azure AD-Anwendung für die Konfiguration des Microsoft Store für Unternehmen und Bildungseinrichtungen abgelaufen ist.

#### <a name="resolution"></a>Lösung

Erneuern Sie den geheimen Schlüssel für die Azure AD-Anwendung. Weitere Informationen finden Sie unter [Geheimen Schlüssel erneuern](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a> Fehler beim Abrufen des Anwendungstokens

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn die verbundene App in Azure AD nicht mehr vorhanden ist.

#### <a name="resolution"></a>Lösung

Löschen Sie die Verbindung mit dem Microsoft Store für Unternehmen und Bildungseinrichtungen, und stellen Sie sie wieder her.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Microsoft Store für Unternehmen** aus.
1. Wählen Sie die vorhandene Verbindung aus.
1. Wählen Sie im Menüband **Löschen** aus.

Erstellen Sie die Verbindung dann erneut. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Konfigurieren von Azure-Diensten](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Einrichten der Synchronisierung mit dem Microsoft Store für Unternehmen und Bildungseinrichtungen](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a> Speicherort des Inhalts ist nicht vorhanden oder es fehlen Berechtigungen

#### <a name="cause"></a>Ursache

Wenn Sie die Verbindung mit dem Microsoft Store für Unternehmen und Bildungseinrichtungen einrichten, geben Sie eine Netzwerkfreigabe zum Speichern synchronisierter Inhalte an. Dieses Problem kann auftreten, wenn diese Freigabe nicht vorhanden ist oder falsche Berechtigungen aufweist. Das Computerkonto für den Dienstverbindungspunkt muss der Besitzer dieses Verzeichnisses und aller Unterverzeichnisse sein.<!-- memdocs#146 --> Wenn dies nicht der Fall ist, wird eine Fehlermeldung ähnlich der folgenden angezeigt:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

So zeigen Sie den von Ihnen konfigurierten Standort an

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Microsoft Store für Unternehmen** aus.

1. Wählen Sie das Konto aus, und öffnen Sie dessen **Eigenschaften**.

1. Wechseln Sie zur Registerkarte **Konfiguration**. Die Einstellung **Standort** zeigt den Netzwerkpfad zum Speichern von Anwendungsinhalten, die aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen heruntergeladen wurden.

#### <a name="workaround"></a>Problemumgehung

1. Wenn sie noch nicht vorhanden ist, erstellen Sie die Freigabe.

1. Überprüfen Sie die NTFS-Berechtigungen für den Ordner und die Berechtigungen für die Netzwerkfreigabe. Gewähren Sie dem Computerkonto des Dienstverbindungspunkts die Berechtigungen **Lesen** und **Schreiben**.

Wenn Sie den Standort neu konfigurieren möchten, löschen Sie die Verbindung mit dem neuen Inhaltsort und stellen Sie sie wieder her.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a> Fehler beim Aufrufen der GET-Methode durch die HTTP-Anforderung

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn die Synchronisierung von Anwendungen aus dem Speicher so lange gedauert hat, dass die Inhalts-URL abgelaufen ist.

#### <a name="workaround"></a>Problemumgehung

Wiederholen Sie den Synchronisierungsvorgang.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Microsoft Store für Unternehmen** aus.
1. Wählen Sie die Verbindung aus. Wählen Sie im Menüband **Mit Microsoft Store für Unternehmen synchronisieren** aus.

Mit jedem Mal sollte es noch weiter gehen. Abhängig von den folgenden Faktoren kann es mehrere Wiederholungsversuche erfordern:

- Die Anzahl der Offlineanwendungen
- Der Größe des Pakets
- Der Netzwerkgeschwindigkeit

Bei jedem Versuch sollten Sie den Fehler weniger häufig sehen. Wenn sich die Zahl der Fehler nicht verringert, gibt es ein anderes Problem.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a> Es können keine weiteren Bytes in den Puffer geschrieben werden

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn das Paket der Anwendung größer als 500 MB ist. Configuration Manager unterstützt die automatische Synchronisierung von Offlineanwendungen nur bei Paketen mit weniger als 500 MB.

#### <a name="workaround"></a>Problemumgehung

Diese Apps können nicht automatisch synchronisiert werden. Sie können den Inhalt jedoch herunterladen und die Anwendung manuell erstellen:

1. Sie erhalten die fehlerhafte Anwendungs-ID aus der folgenden Zeile in **WSfbSynWorker.log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Melden Sie sich als Administrator am Portal für den Microsoft Store für Unternehmen und Bildungseinrichtungen an. Suchen Sie die Seite für diese Anwendung.

    > [!Tip]
    > Die URL für die Seite ähnelt Folgendem: `https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Wählen Sie **Offline** aus, sofern diese Option nicht bereits ausgewählt ist. Wählen Sie anschließend **Verwalten** aus.

    1. Erstellen Sie einen separaten Ordner auf Ihrer Anwendungsinhaltsfreigabe für alle unterstützten Plattformen.

    1. Laden Sie das Paket in den Paketordner herunter.

    1. Laden Sie die codierte Lizenzdatei als `.bin`-Datei in den Paketordner herunter.

    1. Laden Sie alle erforderlichen Frameworks in den Paketordner herunter.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus.

1. [Erstellen Sie eine Anwendung](create-applications.md), indem Sie die Anwendungsinformationen manuell angeben.

    1. Erstellen Sie einen Bereitstellungstyp für jede unterstützte Plattform, die Sie zuvor heruntergeladen haben.

    1. Type: **Windows-App-Paket (\*.appx, \*.appxbundle)**

    1. Geben Sie das appx/appxbundle für das eigentliche Anwendungspaket an, nicht ein erforderliches Abhängigkeitspaket.

Bestätigen Sie die folgenden Details auf der letzten Seite **Importinformationen**:

- **Lizenzdatei:** Gibt die `.bin`-Datei an. Diese Lizenzdatei ist für Offlineanwendungen erforderlich.
- **Windows-App-Abhängigkeiten:** Überprüfen Sie, ob alle erforderlichen Abhängigkeiten für dieses Paket heruntergeladen wurden.


## <a name="sync-doesnt-run"></a>Synchronisierung wird nicht ausgeführt

Dieser Abschnitt behandelt die folgenden Synchronisierungsprobleme:

- Sie starten den Synchronisierungsprozess manuell, aber er wird nicht ausgeführt
- Der Standort wird nicht täglich automatisch synchronisiert

Beginnen Sie mit der Überprüfung der folgenden [Protokolldateien](#log-files), um das Symptom zu identifizieren:

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Suchen Sie dann in einem der folgenden Abschnitte nach allgemeinen Problemen:

- [Manuelle Synchronisierung wird nicht gestartet](#bkmk_sync-symptom1)
- [Automatische tägliche Synchronisierung wird nicht ausgeführt und Fehler „# Worker werden heruntergefahren“ in SMS_BUSINESS_APP_PROCESS_MANAGER.log](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a> Manuelle Synchronisierung wird nicht gestartet

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn Sie eine Synchronisierung weniger als 10 Minuten nach der vorherigen Synchronisierung starten. Sie können nicht häufiger als alle 10 Minuten synchronisieren.

#### <a name="resolution"></a>Lösung

Warten Sie mindestens 10 Minuten, bevor Sie eine weitere Synchronisierung starten.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a> Automatische tägliche Synchronisierung wird nicht ausgeführt und Fehler „# Worker werden heruntergefahren“ in SMS_BUSINESS_APP_PROCESS_MANAGER.log

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn die SMS_BUSINESS_APP_PROCESS_MANAGER-Komponente den WsfbSyncWorker-Thread beendet. Der Fehler kann entweder `2` oder `4` Worker angeben.

#### <a name="workaround"></a>Problemumgehung

Starten Sie den Dienst **SMS_EXECUTIVE** neu.

Wenn Sie nicht in der Lage sind, diesen Hauptdienst wieder zu starten, stoppen Sie beide Komponenten mit MSfB-Workern und starten Sie dann beide:

1. Öffnen Sie die Windows-Registrierung auf dem Server, auf dem der Dienstverbindungspunkt ausgeführt wird.

1. Wechseln Sie zu `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`.

    1. Legen Sie den angeforderten Vorgang auf **Beenden** fest.

    1. Aktualisieren zur Überprüfung des aktuellen Status = **Beendet**.

1. Wechseln Sie zu `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`.

    1. Legen Sie den angeforderten Vorgang auf **Beenden** fest.

    1. Aktualisieren zur Überprüfung des aktuellen Status = **Beendet**.

1. Legen Sie in **SMS_CLOUDCONNECTION** den angeforderten Vorgang auf **Starten** fest.

1. Legen Sie in **SMS_BUSINESS_APP_PROCESS_MANAGER** den angeforderten Vorgang auf **Starten** fest.


## <a name="language-related-issues"></a>Sprachbezogene Probleme

Dieser Abschnitt enthält die folgenden allgemeinen Probleme:

- [Die Sprachauswahländerungen werden nicht angewendet](#bkmk_lang-symptom1)
- [Nicht alle ausgewählten Sprachen sind für alle Lizenzinformationen vorhanden](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a> Die Sprachauswahländerungen werden nicht angewendet

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn die Sprachauswahl zwischengespeichert wird und nach dem Ändern der Eigenschaftswerte nicht gelöscht wird.

#### <a name="workaround"></a>Problemumgehung

Starten Sie den Dienst **SMS_Executive** neu, um dieses Problem zu beheben.

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a> Nicht alle ausgewählten Sprachen sind für alle Lizenzinformationen vorhanden

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn die Lizenzinformationen der Anwendung aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen keine lokalisierten Daten für die angegebene Sprache enthalten.

#### <a name="workaround"></a>Problemumgehung

Fügen Sie fehlende Sprachen für erstellte Anwendungen manuell hinzu.


## <a name="offline-applications"></a>Offlineanwendungen

Dieser Abschnitt enthält die folgenden allgemeinen Probleme:

- [Fehler beim Erstellen einer Offlineanwendung, da der Inhalt nicht überprüft werden kann](#bkmk_off-symptom1)
- [Fehler beim Installieren der aus Offlinelizenzinformationen erstellten Anwendung](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a> Fehler beim Erstellen einer Offlineanwendung, da der Inhalt nicht überprüft werden kann

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn der synchronisierte Inhalt der Offlineanwendung beschädigt oder geändert wurde.

#### <a name="workaround"></a>Problemumgehung

Starten Sie eine neue Synchronisierung. Wenn die Synchronisierung abgeschlossen ist, sollte sie alle fehlerhaften Inhaltsdateien überprüfen und herunterladen.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a> Fehler beim Installieren der aus Offlinelizenzinformationen erstellten Anwendung

#### <a name="cause"></a>Ursache

Dieses Problem kann auftreten, wenn Sie die Anwendung auf einem Client bereitstellen, auf dem eine Version von Windows 10 ausgeführt wird, die älter als Version 1511 ist. Offline lizenzierte Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen werden nur unter Windows 10 Version 1511 und höher unterstützt.

#### <a name="resolution"></a>Lösung

Installieren Sie die neueste Version von Windows 10.


## <a name="next-steps"></a>Nächste Schritte

Weitere Hilfe finden Sie unter [Suchen nach Hilfe für die Verwendung von Configuration Manager](../../core/understand/find-help.md).
