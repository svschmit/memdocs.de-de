---
title: Die Website „BitLocker Administration and Monitoring“ (Verwaltung und Überwachung von BitLocker)
titleSuffix: Configuration Manager
description: Verwenden der Website zur Verwaltung und Überwachung von BitLocker (Helpdeskportal) in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b64e09561def3d19c306b9cfcd4f7eb808763fd
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129255"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Die Website „BitLocker Administration and Monitoring“ (Verwaltung und Überwachung von BitLocker)

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Die Website zur Verwaltung und Überwachung von BitLocker ist eine administrative Schnittstelle für die BitLocker-Laufwerkverschlüsselung. Sie wird auch als Helpdeskportal bezeichnet. Verwenden Sie diese Website, um Berichte zu prüfen, die Laufwerke von Benutzern wiederherzustellen und Geräte-TPMs zu verwalten.

[![Screenshot der Standardwebsite zur Verwaltung und Überwachung von BitLocker](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Bevor Sie sie verwenden können, installieren Sie diese Komponente auf einem Webserver. Weitere Informationen finden Sie unter [Einrichten von BitLocker-Berichten und -Portalen](setup-websites.md).

Greifen Sie über die folgende URL auf die Website zur Verwaltung und Überwachung zu: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Sie können den **Überwachungsbericht für die Wiederherstellung** auf der Website für die Überwachung und Verwaltung anzeigen. Sie fügen weitere BitLocker-Verwaltungsberichte zum Reporting Services-Punkt hinzu. Weitere Informationen finden Sie unter [Anzeigen von BitLocker-Berichten](view-reports.md).

## <a name="groups"></a>Gruppen

Um auf bestimmte Bereiche der Website zur Verwaltung und Überwachung zugreifen zu können, muss Ihr Benutzerkonto einer der folgenden Gruppen angehören. Erstellen Sie diese Gruppen in Active Directory unter einem beliebigen Namen. Wenn Sie diese Website installieren, geben Sie diese Gruppennamen an. Weitere Informationen finden Sie unter [Einrichten von BitLocker-Berichten und -Portalen](setup-websites.md).

|Gruppe|Beschreibung|
|--- |--- |
|BitLocker-Helpdeskadministratoren|Ermöglicht den Zugang zu allen Bereichen der Website „Administration and Monitoring“ (Verwaltung und Überwachung). Wenn Sie einem Benutzer bei der Wiederherstellung seiner Laufwerke helfen, geben Sie nur den Wiederherstellungsschlüssel ein, nicht aber die Domäne und den Benutzernamen. Wenn ein Benutzer sowohl Mitglied dieser Gruppe als auch der Gruppe der BitLocker-Helpdeskbenutzer ist, haben die Berechtigungen der Administratorgruppe Vorrang vor den Berechtigungen der Benutzergruppe.|
|BitLocker-Helpdeskbenutzer|Bietet Zugriff auf die Bereiche **Manage TPM** (TPM verwalten) und **Drive Recovery** (Laufwerkswiederherstellung) der Website „Administration and Monitoring“ (Verwaltung und Überwachung). Wenn Sie einen der beiden Bereiche verwenden, müssen Sie alle Felder ausfüllen, einschließlich der Domäne und des Kontonamens des Benutzers. Wenn ein Benutzer sowohl Mitglied dieser Gruppe als auch der Gruppe der BitLocker-Helpdeskadministratoren ist, haben die Berechtigungen der Administratorgruppe Vorrang vor den Berechtigungen der Benutzergruppe.|
|BitLocker-Berichtsbenutzer|Bietet Zugriff auf den Bereich **Berichte** auf der Website „Administration and Monitoring“ (Verwaltung und Überwachung).|

## <a name="manage-tpm"></a>Verwalten von TPM

Wenn ein Benutzer die falsche PIN zu oft eingibt, kann er die TPM sperren. Wie oft dies geschehen darf, bevor die Sperre eintritt, unterscheidet sich von Hersteller zu Hersteller. Greifen Sie vom Bereich **TPM verwalten** der Website zur Verwaltung und Überwachung auf das zentralisierte Datensystem zur Schlüsselwiederherstellung zu.

Weitere Informationen zum TPM-Besitz finden Sie unter [Konfigurieren von MBAM, um die TPM zu hinterlegen und OwnerAuth-Kennwörter zu speichern](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> Ab Windows 10, Version 1607, behält Windows das TPM-Besitzerkennwort bei der Bereitstellung der TPM nicht bei.

1. Wechseln Sie im Webbrowser zur Website zur Verwaltung und Überwachung, z. B. `https://webserver.contoso.com/HelpDesk`.

1. Wählen Sie im linken Fensterbereich den Bereich **TPM verwalten** aus.

    ![Website zur Verwaltung und Überwachung von BitLocker – Seite „TPM verwalten“](media/bitlocker-admin-manage-tpm.png)

1. Geben Sie den vollqualifizierten Domänennamen für den Computer und den Computernamen ein.

1. Geben Sie bei Bedarf die Domäne und den Benutzernamen des Benutzers ein, um die Kennwortdatei des TPM-Besitzers abzurufen.

1. Wählen Sie eine der folgenden Optionen für den **Grund für die Anforderung der Kennwortdatei des TPM-Besitzers** aus:

    - PIN-Sperrung zurücksetzen
    - TPM aktivieren
    - TPM deaktivieren
    - TPM-Kennwort ändern
    - TPM löschen
    - Andere

    Nachdem Sie das Formular **übermittelt** haben, gibt die Website eine der folgenden Antworten zurück:

    - Wenn sie keine passende TPM-Besitzerkennwortdatei finden kann, gibt sie eine Fehlermeldung zurück.

    - Die TPM-Besitzerkennwortdatei für den entsprechenden Computer

    Nachdem Sie die TPM-Besitzerkennwortdatei abgerufen haben, zeigt die Website das Besitzerkennwort an.

1. Zum Speichern des Kennworts in einer Datei klicken Sie auf **Speichern**.

1. Wählen Sie im Bereich **TPM verwalten** die Option **TPM-Sperre zurücksetzen** aus, und geben Sie die TPM-Besitzerkennwortdatei an.

    Die TPM-Sperre wird zurückgesetzt. BitLocker stellt den Zugriff des Benutzers auf das Gerät wieder her.

    > [!IMPORTANT]
    > Geben Sie weder den TPM-Hashwert noch die TPM-Besitzerkennwortdatei weiter.

## <a name="drive-recovery"></a>Laufwerkswiederherstellung

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> Wiederherstellen eines Laufwerks im Wiederherstellungsmodus

Laufwerke wechseln in den folgenden Szenarien in den Wiederherstellungsmodus:

- Der Benutzer verliert oder vergisst seine PIN oder sein Kennwort.
- Die TPM (Trusted Module Platform) erkennt Änderungen am BIOS oder an den Startdateien des Computers.

Sie können das Wiederherstellungskennwort im Bereich **Laufwerkswiederherstellung** der Website „Administration and Monitoring“ (Verwaltung und Überwachung) abrufen.

> [!IMPORTANT]
> Wiederherstellungskennwörter laufen nach einmaliger Verwendung ab. Auf Betriebssystemlaufwerken und Festplattenlaufwerken gilt automatisch die Regel der einmaligen Verwendung. Bei Wechseldatenträgern gilt sie, wenn Sie das Laufwerk entfernen und wieder einsetzen.

1. Wechseln Sie im Webbrowser zur Website zur Verwaltung und Überwachung, z. B. `https://webserver.contoso.com/HelpDesk`.

1. Wählen Sie im linken Fensterbereich den Bereich **Laufwerkswiederherstellung** aus.

    ![Website zur Verwaltung und Überwachung von BitLocker – Seite „Laufwerkswiederherstellung“](media/bitlocker-admin-drive-recovery.png)

1. Falls erforderlich, geben Sie die Domäne und den Benutzernamen des Benutzers ein, um die Wiederherstellungsinformationen anzuzeigen.

1. Geben Sie die ersten acht Ziffern der Wiederherstellungsschlüssel-ID ein, um eine Liste möglicher passender Wiederherstellungsschlüssel anzuzeigen. Geben Sie die gesamte Wiederherstellungsschlüssel-ID ein, um den genauen Wiederherstellungsschlüssel zu erhalten.

1. Wählen Sie eine der folgenden Optionen als **Grund für die Laufwerksentsperrung** aus:

    - Startreihenfolge des Betriebssystems wurde geändert
    - BIOS wurde geändert
    - Betriebssystemdateien wurden geändert
    - Schlüssel für den Systemstart ist verloren gegangen
    - PIN ist verloren gegangen
    - TPM-Zurücksetzung
    - Passphrase ist verloren gegangen
    - Smartcard ist verloren gegangen
    - Andere

    Nachdem Sie das Formular **übermittelt** haben, gibt die Website eine der folgenden Antworten zurück:

    - Es werden mehrere mögliche Treffer zurückgegeben, wenn für den Benutzer mehrere passende Wiederherstellungskennwörter vorhanden sind.

    - Das Wiederherstellungskennwort und das Wiederherstellungspaket für den entsprechenden Benutzer

        > [!NOTE]
        > Wenn Sie ein beschädigtes Laufwerk wiederherstellen, werden BitLocker durch die Wiederherstellungspaketoption wichtige, für den Wiederherstellungsversuch erforderliche Informationen bereitgestellt.

    - Wenn sie kein passendes Wiederherstellungskennwort finden kann, gibt sie eine Fehlermeldung zurück.

    Nachdem Sie das Wiederherstellungskennwort und das Wiederherstellungspaket abgerufen haben, zeigt die Website das Wiederherstellungskennwort an.

1. Wählen Sie zum Kopieren des Kennworts **Schlüssel kopieren** aus. Zum Speichern des Wiederherstellungskennworts in einer Datei klicken Sie auf **Speichern**.

Um das Laufwerk zu entsperren, geben Sie das Wiederherstellungskennwort ein, oder verwenden Sie das Wiederherstellungspaket.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> Wiederherstellen von verschobenen Laufwerken

Wenn Sie ein Laufwerk auf einen neuen Computer verschieben, da die TPM anders ist, akzeptiert BitLocker die vorherige PIN nicht. Sie können verschobene Laufwerke wiederherstellen, indem Sie mithilfe der Wiederherstellungsschlüssel-ID das Wiederherstellungskennwort abrufen.

Sie können verschobene Laufwerke über den Bereich **Drive recovery** (Laufwerkswiederherstellung) der Website „Administration and Monitoring“ (Verwaltung und Überwachung) wiederherstellen.

1. Starten Sie auf dem Computer mit dem verschobenen Laufwerk den Computer im Modus „Windows-Wiederherstellungsumgebung“ (WinRE).

1. In WinRE behandelt BitLocker das verschobene Betriebssystemlaufwerk wie ein Festplattenlaufwerk. BitLocker zeigt die Wiederherstellungskennwort-ID des Laufwerks an und fordert zur Eingabe des Wiederherstellungskennworts auf.

    > [!NOTE]
    > In einigen Situationen wählen Sie während des Startvorgangs die Option **Ich habe mein Kennwort vergessen** aus, wenn die Option verfügbar ist. Wechseln Sie dann in den Wiederherstellungsmodus, um die Wiederherstellungsschlüssel-ID anzuzeigen.

1. Verwenden Sie die Wiederherstellungsschlüssel-ID, um das Wiederherstellungskennwort von der Website zur Verwaltung und Überwachung zu erhalten. Weitere Informationen finden Sie unter [Wiederherstellen eines Laufwerks im Wiederherstellungsmodus](#bkmk_recovery).

Wenn das verschobene Laufwerk für die Verwendung eines TPM-Chips konfiguriert war, führen Sie die folgenden Schritte aus. Andernfalls ist das Wiederherstellungsverfahren abgeschlossen.

1. Nachdem Sie das Laufwerk entsperrt haben, starten Sie den Computer im WinRE-Modus. Öffnen Sie eine Eingabeaufforderung in WinRE, und verwenden Sie den Befehl `manage-bde`, um das Laufwerk zu entschlüsseln. Dieses Tools stellt die einzige Möglichkeit dar, den Schutz mit **TPM + PIN** ohne den ursprünglichen TPM-Chip aufzuheben. Weitere Informationen zu diesem Befehl finden Sie unter [Manage-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Wenn der Vorgang abgeschlossen ist, starten Sie den Computer normal. Configuration Manager erzwingt die BitLocker-Richtlinie, um das Laufwerk mit der TPM und PIN des neuen Computers zu verschlüsseln.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> Wiederherstellen eines beschädigten Laufwerks

Verwenden Sie die Wiederherstellungsschlüssel-ID, um ein Wiederherstellungsschlüsselpaket von der Website zur Verwaltung und Überwachung zu erhalten. Weitere Informationen finden Sie unter [Wiederherstellen eines Laufwerks im Wiederherstellungsmodus](#bkmk_recovery).

1. Speichern Sie das **Wiederherstellungsschlüsselpaket** auf Ihrem Computer, und kopieren Sie es dann auf den Computer mit dem beschädigten Laufwerk.

1. Öffnen Sie eine Eingabeaufforderung als Administrator, und geben Sie den folgenden Befehl ein:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Ersetzen Sie die folgenden Werte:

    - `<corrupted drive>`: Der Laufwerksbuchstabe des beschädigten Laufwerks, z. B. `D:`.
    - `<fixed drive>`: Der Laufwerksbuchstabe eines verfügbaren Festplattenlaufwerks, das ähnlich groß oder größer als das beschädigte Laufwerk ist. BitLocker stellt Daten auf dem beschädigten Laufwerk wieder her und verschiebt sie auf das angegebene Laufwerk. Alle Daten auf diesem Laufwerk werden überschrieben.
    - `<key package>`: Der Standort des Wiederherstellungsschlüsselpakets.
    - `<recovery password>`: Das zugehörige Wiederherstellungskennwort.

    Beispiel:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Weitere Informationen zu diesem Befehl finden Sie unter [Repair-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Berichte

Die Website zur Verwaltung und Überwachung enthält den **Überwachungsbericht für die Wiederherstellung**. Weitere Berichte sind über den Reporting Services-Punkt von Configuration Manager erhältlich. Weitere Informationen finden Sie unter [Anzeigen von BitLocker-Berichten](view-reports.md).

1. Wechseln Sie im Webbrowser zur Website zur Verwaltung und Überwachung, z. B. `https://webserver.contoso.com/HelpDesk`.

1. Wählen Sie im linken Fensterbereich den Bereich **Berichte** aus.

1. Wählen Sie in der oberen Menüleiste den **Überwachungsbericht für die Wiederherstellung** aus.

Weitere Informationen finden Sie unter [Überwachungsbericht für die Wiederherstellung](view-reports.md#bkmk-audit).

> [!TIP]
> Wählen Sie zum Speichern von Berichtsergebnissen **Exportieren** in der Menüleiste **Berichte** aus.
