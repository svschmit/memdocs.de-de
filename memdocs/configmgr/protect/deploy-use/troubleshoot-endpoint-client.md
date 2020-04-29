---
title: Beheben von Problemen mit Endpoint Protection
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Fehler bei Windows Defender und Endpoint Protection beheben.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709418"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Fehlerbehebung für Windows Defender oder Endpoint Protection-Client

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie auf Probleme mit Windows Defender oder Endpoint Protection stoßen, verwenden Sie diesen Artikel, um die folgenden Probleme zu behandeln:  

- [Aktualisieren von Windows Defender oder Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [Starten von Windows Defender oder des Endpoint Protection-Diensts](#starting-windows-defender-or-endpoint-protection-service)  
- [Internetverbindungsprobleme](#internet-connection-issues)  
- [Erkannte Bedrohung kann nicht beseitigt werden](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>Aktualisieren von Windows Defender oder Endpoint Protection

### <a name="symptoms"></a>Symptome

Windows Defender oder Endpoint Protection werden automatisch zusammen mit Microsoft Update verwendet, um zu gewährleisten, dass die Virus- und Spywaredefinitionen stets auf dem neuesten Stand sind.  

In diesem Abschnitt werden allgemeine Probleme mit automatischen Updates behandelt, einschließlich der folgenden Situationen:  

- Es werden Fehlermeldungen mit dem Hinweis auf nicht erfolgreiche Updates angezeigt.  

- Bei der Überprüfung auf Updates erhalten Sie eine Fehlermeldung mit dem Hinweis, dass die Definitionsupdates für Viren und Spyware nicht überprüft, heruntergeladen oder installiert werden können.  

- Die Updates sind nicht erfolgreich, obwohl eine Verbindung des Geräts mit dem Internet besteht.  

- Updates werden nicht automatisch gemäß Zeitplan installiert.  

### <a name="causes"></a>Ursachen

Meist sind Probleme mit Updates auf Probleme mit der Internetverbindung zurückzuführen. Wenn Sie sicher sind, dass Ihr Gerät mit dem Internet verbunden ist, weil Sie andere Websites besuchen können, ist das Problem unter Umständen auf Konflikte mit den Interneteinstellungen in Windows zurückzuführen.  

### <a name="options-to-resolve"></a>Aufzulösende Optionen

#### <a name="step-1-reset-your-internet-settings"></a>Schritt 1: Zurücksetzen Ihrer Interneteinstellungen  

1. Beenden Sie alle geöffneten Programme, einschließlich des Webbrowsers.  

    > [!NOTE]  
    > Wenn Sie diese Interneteinstellungen zurücksetzen, werden möglicherweise die temporären Dateien, Cookies, der Browserverlauf und die Onlinekennwörter Ihres Browsers gelöscht. Ihre Favoriten werden dabei nicht gelöscht.  

2. Wechseln Sie zum Menü **Start**, und öffnen Sie `inetcpl.cpl`.  

3. Wechseln Sie zur Registerkarte **Erweitert**.  

4. Wählen Sie im Abschnitt zum **Zurücksetzen der Internet Explorer-Einstellungen** die Option **Zurücksetzen** aus. Anschließend wählen Sie zur Bestätigung erneut **Zurücksetzen** aus.  

5. Wählen Sie **OK** aus, wenn die Einstellungen zurückgesetzt werden.

6. Versuchen Sie erneut, Windows Defender zu aktualisieren.

Wenn das Problem weiterhin besteht, fahren Sie mit dem nächsten Schritt fort.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Schritt 2: Sicherstellen, dass Uhrzeit und Datum auf dem Computer richtig festgelegt sind  

Wenn die Fehlermeldung den Code 0x80072f8f enthält, wird der Fehler mit hoher Wahrscheinlichkeit durch eine fehlerhafte Einstellung für Datum oder Uhrzeit auf dem Computer verursacht. Wechseln Sie zum Menü **Start**, wählen Sie **Einstellungen**, **Uhrzeit und Sprache** und dann **Datum und Uhrzeit** aus.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Schritt 3: Umbenennen des Softwareverteilungsordners auf dem Computer  

1. Beenden Sie den **Windows Update**-Dienst.  

    1. Wechseln Sie zu **Start**, und öffnen Sie **services.msc**.  

    2. Wählen Sie den **Windows Update**-Dienst aus. Wechseln Sie zum Menü **Aktion**, und wählen Sie **Beenden** aus.

2. Benennen Sie das Verzeichnis **SoftwareDistribution** um.  

    1. Öffnen Sie eine Eingabeaufforderung als Administrator.  

    2. Geben Sie die folgenden Befehle ein:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Starten Sie den **Windows Update**-Dienst neu.

    1. Wechseln Sie zurück zum Fenster **Dienste**.  

    2. Wählen Sie den **Windows Update**-Dienst aus. Wechseln Sie zum Menü **Aktion**, und wählen Sie **Starten** aus.

    3. Schließen Sie das Fenster „Dienste“.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Schritt 4: Zurücksetzen der Antivirenaktualisierungs-Engine von Microsoft auf dem Computer  

1. Öffnen Sie eine Eingabeaufforderung als Administrator.

2. Geben Sie die folgenden Befehle ein:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Starten Sie den Computer neu.  

4. Versuchen Sie erneut, Windows Defender zu aktualisieren.

Wenn das Problem weiterhin besteht, fahren Sie mit dem nächsten Schritt fort.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Schritt 5: Manuelles Installieren der Definitionsupdates  

[Laden Sie manuell die neuesten Updates herunter](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>Schritt 6: Kontaktaufnahme mit dem Microsoft-Support  

Wenn diese Schritte das Problem nicht behoben haben, wenden Sie sich an den Microsoft-Support. Weitere Informationen finden Sie unter [Supportoptionen und Communityressourcen](../../core/understand/find-help.md#BKMK_SupportOptions).  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>Starten von Windows Defender oder des Endpoint Protection-Diensts

### <a name="symptom"></a>Symptom

Eine Meldung mit dem folgenden Hinweis wird angezeigt:  **Windows Defender or Endpoint Protection isn't monitoring your computer because the program's service stopped (Der Computer wird nicht von Windows Defender oder Endpoint Protection überwacht, da der Dienst des Programms angehalten wurde). Sie sollten ihn jetzt neu starten.**

### <a name="solution"></a>Lösung

#### <a name="step-1-restart-your-computer"></a>Schritt 1: Neustarten des Computers

Schließen Sie alle Anwendungen, und starten Sie den Computer neu.  

#### <a name="step-2-check-the-windows-service"></a>Schritt 2: Überprüfen des Windows-Diensts

1. Wechseln Sie zu **Start**, und öffnen Sie **services.msc**.  

2. Wählen Sie den **Windows Defender Antivirus-Dienst** aus.  

3. Stellen Sie sicher, dass der **Starttyp** auf **Automatisch** festgelegt ist.

4. Wechseln Sie zum Menü **Aktion**, und wählen Sie **Starten** aus.

    1. Wenn diese Aktion nicht verfügbar ist, wählen Sie **Beenden** aus. Warten Sie, bis der Dienst beendet ist, und wählen Sie dann die Aktion **Starten** aus, um den Dienst neu zu starten.  

Beachten Sie alle Fehler, die während dieses Prozesses auftreten können. [Wenden Sie sich an den Microsoft-Support](../../core/understand/find-help.md#BKMK_SupportOptions), und geben Sie die Fehlerinformationen an.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Schritt 3: Entfernen aller Sicherheitsprogramme von Drittanbietern  

> [!NOTE]  
> Einige Sicherheitsanwendungen lassen sich nicht vollständig deinstallieren. Sie müssen möglicherweise ein Bereinigungsprogramm für die frühere Sicherheitsanwendung herunterladen und ausführen, damit diese vollständig entfernt werden kann.  

1. Wechseln Sie zu **Starten**, und öffnen Sie **appwiz.cpl**.  

2. Deinstallieren Sie in der Liste der installierten Programme sämtliche Drittanbieter-Sicherheitsprogramme.

3. Starten Sie den Computer neu.  

> [!CAUTION]  
> Wenn Sie Ihre Sicherheitsprogramme entfernen, befindet sich der Computer möglicherweise in einem ungeschützten Zustand. Wenn nach dem Entfernen der vorhandenen Sicherheitsprogramme Probleme bei der Installation von Windows Defender auftreten, wenden Sie sich an den [Microsoft-Support](https://support.microsoft.com/supportforbusiness/productselection). Wählen Sie die Produktfamilie **Sicherheit** und dann das Produkt **Windows Defender** aus.

## <a name="internet-connection-issues"></a>Internetverbindungsprobleme

Damit Ihr Computer die neuesten Updates von Windows Update erhalten kann, verbinden Sie ihn mit dem Internet.  

1. Wechseln Sie zu **Starten**, und öffnen Sie **ncpa.cpl**.  

2. Öffnen Sie den Verbindungsnamen, um den **Status** der Verbindung anzuzeigen.  

3. Wenn Ihr Computer verbunden ist, entspricht **Internet** dem Status der **IPv4-Konnektivität** und/oder **IPv6-Konnektivität**.  

4. Wenn Ihr Computer scheinbar nicht verbunden ist, wählen Sie den Verbindungsnamen und anschließend **Verbindung untersuchen** aus.

Schließen Sie alle geöffneten Programme, und starten Sie den Computer neu.  

## <a name="detected-threat-cant-be-remediated"></a>Erkannte Bedrohung kann nicht beseitigt werden

Wenn Windows Defender oder Endpoint Protection eine potenzielle Bedrohung erkennt, versucht es, die Bedrohung durch Quarantäne oder Entfernen der Bedrohung einzudämmen. Diese Bedrohungen können sich in einem komprimierten Archiv (`.zip`) oder in einer Netzwerkfreigabe verbergen.

### <a name="remove-or-scan-the-file"></a>Entfernen oder scannen Sie die Datei.  

- Wenn sich die erkannte Bedrohung in einer komprimierten Archivdatei befand, navigieren Sie zu dieser Datei. Löschen Sie die Datei, oder überprüfen Sie sie manuell. Klicken Sie mit der rechten Maustaste auf die Datei, und wählen Sie **Mit Windows Defender scannen** aus. Wenn Windows Defender zusätzliche Bedrohungen in der Datei erkennt, werden Sie benachrichtigt. Anschließend können Sie eine geeignete Aktion auswählen.  

- Wenn sich die erkannte Bedrohung in einer Netzwerkfreigabe befand, öffnen Sie die Freigabe und scannen Sie sie manuell. Klicken Sie mit der rechten Maustaste auf die Datei, und wählen Sie **Mit Windows Defender scannen** aus. Wenn Windows Defender zusätzliche Bedrohungen in der Netzwerkfreigabe erkennt, werden Sie benachrichtigt. Anschließend können Sie eine geeignete Aktion auswählen.  

- Wenn Sie sich nicht sicher sind, woher die Datei stammt, führen Sie eine vollständige Überprüfung auf Ihrem Computer durch. Eine vollständige Überprüfung kann einige Zeit in Anspruch nehmen.  

## <a name="see-also"></a>Weitere Informationen:

[Endpoint Protection client frequently asked questions (Endpoint Protection-Client – Häufig gestellte Fragen)](endpoint-protection-client-faq.md)

[Hilfe zu Endpoint Protection-Client](endpoint-protection-client-help.md)
