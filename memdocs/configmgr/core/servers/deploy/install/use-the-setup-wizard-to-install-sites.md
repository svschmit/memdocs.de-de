---
title: Setup-Assistent
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 22a70d2d1c779163d18e89e3ddb9b2371907ef56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700368"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Verwenden des Setup-Assistenten zum Installieren von Configuration Manager-Standorten

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie zum Installieren eines neuen Configuration Manager-Standorts mit einer Benutzeroberfläche den Configuration Manager-Setup-Assistenten (setup.exe). Der Assistent unterstützt die Installation eines primären Standorts oder eines Standorts der zentralen Verwaltung. Verwenden Sie auch den Assistenten zum [Ausführen eines Upgrades für eine Evaluierungsinstallation](upgrade-an-evaluation-install-to-a-full-install.md) von Configuration Manager auf eine vollständig lizenzierte Installation. Wenn Sie den Assistenten nicht verwenden möchten, können Sie stattdessen ein [Installationsskript](use-a-command-line-to-install-sites.md) verwenden und eine unbeaufsichtigte Befehlszeileninstallation ausführen.

Installieren Sie einen sekundären Standort aus der Configuration Manager-Konsole heraus. Sekundäre Standorte unterstützen keine Installation per Skript über die Befehlszeile.

> [!Note]  
> Ab Version 1906 ist die Datei **splash.hta** nicht mehr im Stammverzeichnis des Installationsmediums vorhanden. Sie enthielt die folgenden Informationen:<!--SCCMDocs-pr#3545-->
>
> - **Installieren des Standorts**: `smssetup\bin\x64\setup.exe`. Weitere Informationen finden Sie unter [Installieren einer zentralen Verwaltung oder eines primären Standorts](#bkmk_primary).
> - **Vorbereitung**: [Entwerfen einer Hierarchie von Standorten](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Bewerten der Serverbereitschaft**: [Voraussetzungsprüfung](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Für den Download erforderliche Dateien**: `smssetup\bin\x64\setupdl.exe`. Weitere Informationen finden Sie unter [Setup Downloader (Setup-Downloadprogramm)](setup-downloader.md).
> - **Installieren einer Configuration Manager-Konsole**: `smssetup\bin\i386\consolesetup.exe`. Weitere Informationen finden Sie unter [Installieren von Konsolen](install-consoles.md).
> - [**System Center Updates Publisher herunterladen**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Clients für weitere Betriebssysteme herunterladen**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft Endpoint Configuration Manager – macOS-Client (64-Bit)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Clients für UNIX und Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Versionshinweise**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Dokumentation lesen**](https://docs.microsoft.com/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Unterstützung bei der Installation anfordern**: [TechNet-Foren: Configuration Manager (Current Branch) – Bereitstellung von Standorten und Clients](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Configuration Manager-Community**: [System Center-Community: Teilnahme](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Configuration Manager-Startseite**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> Installieren einer zentralen Verwaltung oder eines primären Standorts

Wenden Sie das folgende Verfahren an, um einen Standort der zentralen Verwaltung oder einen primären Standort zu installieren. Wenden Sie es auch an, um einen Evaluierungsstandort auf einen voll lizenzierten Configuration Manager-Standort upzugraden.

Machen Sie sich vor der Installation des Standorts mit den Details in den folgenden Artikeln vertraut:

- [Vorbereitung zur Installation von Standorten ](prepare-to-install-sites.md)
- [Voraussetzungen für die Installation von Standorten](prerequisites-for-installing-sites.md)

Wenn Sie einen Standort der zentralen Verwaltung als Teil eines Standorterweiterungsszenarios installieren, lesen Sie den Abschnitt [Erweitern eines eigenständigen primären Standorts](use-the-setup-wizard-to-install-sites.md#bkmk_expand), bevor Sie das folgende Verfahren anwenden.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Vorgang zum Installieren eines primären Standorts oder eines Standorts der zentralen Verwaltung

1. Führen Sie auf dem Computer, auf dem der Standort installiert werden soll, `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` aus, um den **Setup-Assistenten von Configuration Manager** zu starten.  

    > [!NOTE]  
    > Wenn Sie einen Standort der zentralen Verwaltung installieren, um auf einem eigenständigen primären Standort zu erweitern, oder einen neuen untergeordneten primären Standort in einer vorhandenen Hierarchie installieren, verwenden Sie Installationsmedien (Quelldateien), die mit der Version des oder der vorhandenen Standorte übereinstimmen. Wenn Sie konsoleninterne Aktualisierungen installiert haben, die die Versionen der zuvor installierten Standorte geändert haben, verwenden Sie nicht die Originalinstallationsmedien. Verwenden Sie stattdessen Quelldateien aus dem [Ordner CD.Latest](../../manage/the-cd.latest-folder.md) eines aktualisierten Standorts. Configuration Manager erfordert die Verwendung von Quelldateien, die mit der Version des bestehenden Standorts übereinstimmen, mit dem der neue Standort eine Verbindung herstellt.  

2. Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter** aus.  

3. Wählen Sie auf der Seite **Erste Schritte** den Typ des Standorts aus, den Sie installieren möchten:  

    - **Standort der zentralen Verwaltung** als ersten Standort einer neuen Hierarchie oder beim Erweitern eines eigenständigen primären Standorts:  

        Wählen Sie **Standort der zentralen Verwaltung für Configuration Manager installieren** aus.  

        Bei einem späteren Schritt dieses Verfahrens haben Sie die Möglichkeit, einen Standort der zentralen Verwaltung als ersten Standort einer neuen Hierarchie oder zum Erweitern eines eigenständigen primären Standorts zu installieren.  

    - **Primärer Standort** als eigenständiger primärer Standort, der der erste Standort einer neuen Hierarchie ist, oder als untergeordneter primärer Standort:  

        Wählen Sie **Primären Configuration Manager-Standort installieren** aus.  

        > [!TIP]  
        > Normalerweise wählen Sie nur die Option **Typische Installationsoptionen für einen eigenständigen primären Standort verwenden** aus, wenn Sie einen eigenständigen primären Standort in einer Testumgebung installieren möchten. Wenn Sie diese Option auswählen, führt Setup die folgenden Aktionen aus:  
        >
        > - konfiguriert Setup den Standort automatisch als eigenständigen primären Standort.  
        > - wird ein Standardinstallationspfad verwendet.  
        > - wird eine lokale Installation der Standardinstanz von SQL Server für die Standortdatenbank verwendet.  
        > - werden ein Verwaltungspunkt und ein Verteilungspunkt auf dem Standortservercomputer installiert.  
        > - Konfiguriert den Standort mit Englisch und der Anzeigesprache des BS auf dem primären Standortserver, wenn diese einer der Sprachen entspricht, die Configuration Manager unterstützt.  

4. Auf der Seite **Product Key**:  

    - Wählen Sie, ob Configuration Manager als Evaluierungsversion oder als lizenzierte Version installiert werden soll.  

        - Wenn Sie eine lizenzierte Version auswählen, geben Sie den Product Key ein und klicken Sie auf **Weiter**.  

        - Wenn Sie eine Evaluierungsversion auswählen, klicken Sie auf **Weiter**. (Sie können später ein Upgrade einer Evaluierungsversion auf eine Vollversion durchführen.)  

    - Sie können auch das **Ablaufdatum der Software Assurance** Ihres Lizenzvertrags angeben. Es ist eine bequeme Erinnerung an dieses Datum. Wenn Sie das Datum nicht während des Setups eingeben, können Sie es später in der Configuration Manager-Konsole angeben.  

        > [!NOTE]  
        > Microsoft überprüft das angegebene Ablaufdatum nicht und verwendet es auch nicht, um die Lizenz zu überprüfen. Sie können es als Erinnerung an das Ablaufdatum verwenden. Dieses Datum ist hilfreich, da Configuration Manager regelmäßig online überprüft, ob neue Softwareupdates angeboten werden. Ihr Software Assurance-Lizenzstatus sollte aktuell sein, sodass Sie berechtigt sind, diese zusätzlichen Updates zu verwenden.  

    Weitere Informationen finden Sie unter [Lizenzierung und Branches](../../../understand/learn-more-editions.md).  

5. Lesen und akzeptieren Sie auf der Seite **Microsoft-Software-Lizenzbedingungen** die Lizenzbedingungen.  

6. Lesen und akzeptieren Sie auf der Seite **Lizenzen für erforderliche Komponenten** die Lizenzbedingungen für die erforderliche Software. Die Software wird gegebenenfalls heruntergeladen und automatisch auf Standortsystemen oder Clients installiert. Übernehmen Sie alle Begriffe, bevor Sie mit der nächsten Seite fortfahren.  

7. Geben Sie auf der Seite **Download der Voraussetzungskomponenten** an, ob Setup die neuesten vorausgesetzten verteilbaren Dateien aus dem Internet herunterladen oder zuvor heruntergeladene Dateien verwenden muss:  

    - Wenn Setup die Dateien zu diesem Zeitpunkt herunterladen soll, wählen Sie **Erforderliche Dateien herunterladen** aus. Geben Sie dann einen Speicherort zum Speichern der Dateien an.  

    - Falls Sie die Dateien bereits mit dem [Setup-Downloadprogramm](setup-downloader.md) heruntergeladen haben, wählen Sie **Bereits heruntergeladene Dateien verwenden** aus. Geben Sie dann den Downloadordner an.  

        > [!TIP]  
        > Wenn Sie bereits heruntergeladene Dateien verwenden, überprüfen Sie, ob der Downloadordner die neuesten Dateiversionen enthält.  

8. Wählen Sie auf der Seite **Serversprachauswahl** die Sprachen aus, die für die Configuration Manager-Konsole sowie für Berichte verfügbar sind. (Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.) Weitere Informationen finden Sie unter [Sprachpaketen](language-packs.md).  

9. Wählen Sie auf der Seite **Clientsprachauswahl** die Sprachen aus, die Clientcomputern zur Verfügung stehen. Geben Sie auch an, ob alle Clientsprachen für mobile Geräteclients aktiviert werden sollen. (Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.)  

    > [!IMPORTANT]  
    > Wenn Sie einen Standort der zentralen Verwaltung verwenden, stellen Sie sicher, dass die Clientsprachen, die Sie am Standort der zentralen Verwaltung konfigurieren, alle Clientsprachen umfassen, die Sie an den einzelnen untergeordneten primären Standorten konfigurieren. Clients, die über einen Verteilungspunkt installieren, haben Zugriff auf die Clientsprachen am Standort der obersten Ebene, während Clients, die über einen Verwaltungspunkt installieren, von ihrem zugewiesenen primären Standort aus Zugriff auf die Clientsprachen haben.  

10. Geben Sie auf der Seite **Standort- und Installationseinstellungen** Einstellungen für den neuen Standort an, den Sie installieren:  

    - **Standortcode:** [Jeder Standortcode in einer Hierarchie muss eindeutig sein](prepare-to-install-sites.md#bkmk_sitecodes). Verwenden Sie drei alphanumerische Zeichen: A bis Z und 0 bis 9. Da der Standortcode in Ordnernamen verwendet wird, dürfen keine für Windows reservierten Namen wie die folgenden verwendet werden:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > Setup überprüft nicht, ob der angegebene Standortcode bereits verwendet wird oder ein reservierter Name ist.  

    - **Standortname:** Jeder Standort benötigt diesen Anzeigenamen, mit dem Sie den Standort bestimmen können.  

    - **Installationsordner:** Dieser Ordner ist der Pfad zur Configuration Manager-Installation. Sie können den Speicherort nach der Installation des Standorts nicht mehr ändern. Der Pfad darf keine Unicode-Zeichen oder Leerzeichen enthalten.  

        > [!NOTE]  
        > Überlegen Sie sich, ob Sie den Standardinstallationsordner verwenden möchten. Wenn Sie die Standardbetriebssystempartition in einer Produktionsumgebung verwenden, können folgende Probleme in der Zukunft auftreten:  
        >
        > - Wenn Configuration Manager den zusätzlichen freien Speicherplatz auf der Betriebssystempartition verwendet, werden weder Windows noch Configuration Manager ordnungsgemäß funktionieren. Wenn Sie Configuration Manager auf einer separaten Partition installieren, wird sich dessen Datenträgernutzung nicht auf das Betriebssystem auswirken.
        > - Die Leistung von Configuration Manager ist bei Verwendung eines schnellen Datenträgers besser. Eine Serverentwürfe optimieren die Geschwindigkeit des Betriebssystemdatenträgers nicht.
        > - Sie können das Betriebssystem warten, wiederherstellen oder neuinstallieren, ohne Ihre Configuration Manager-Installation zu beeinträchtigen.  

11. Verwenden Sie auf der Seite **Standortinstallation** die folgende Option entsprechend Ihrem Szenario:  

    - **Ich installiere einen Standort der zentralen Verwaltung:**  

        Wählen Sie auf der Seite **Installation des Standorts der zentralen Verwaltung** die Option **Als ersten Standort in einer neuen Hierarchie installieren** aus, und klicken Sie auf **Weiter**, um fortzufahren.  

    - **Ich erweitere einen eigenständigen primären Standort in eine Hierarchie mit einem Standort der zentralen Verwaltung:**  

        Wählen Sie auf der Seite **Installation des Standorts der zentralen Verwaltung** die Option **Vorhandenen eigenständigen primären Standort in eine Hierarchie erweitern**aus. Geben Sie dann den FQDN des eigenständigen primären Standortservers an, und wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.  

        Die Medien, die Sie verwenden, um den neuen Standort der zentralen Verwaltung zu installieren, müssen mit der Version des primären Standorts übereinstimmen.  

    - **Ich installiere einen eigenständigen primären Standort:**  

        Wählen Sie auf der Seite **Installation am primären Standort** die Option **Den primären Standort als eigenständigen Standort installieren** aus. Klicken Sie dann auf **Weiter**.  

    - **Ich installiere einen untergeordneten primären Standort:**  

        Wählen Sie auf der Seite **Installation am primären Standort** die Option **Primären Standort einer vorhandenen Hierarchie hinzufügen** aus. Geben Sie dann den FQDN für den Standort der zentralen Verwaltung ein, und wählen Sie **Weiter** aus.  

12. Geben Sie auf der Seite **Datenbankinformationen** die folgenden Informationen an:  

    - **SQL Server-Name (FQDN):** Dieser Wert wird standardmäßig auf den Standortservercomputer festgelegt.  

        Wenn Sie einen benutzerdefinierten Port verwenden, fügen Sie diesen Port zum FQDN des SQL Servers hinzu. Stellen Sie hierzu dem FQDN der SQL Server-Instanz ein Komma gefolgt von der Portnummer hinzu. Beispiel: Verwenden Sie für den Server *SQLServer1.fabrikam.com* Folgendes, um den Port *1551* anzugeben: `SQLServer1.fabrikam.com,1551`  

    - **Instanzname:** Standardmäßig ist dieser Wert leer. Verwendet die Standardinstanz von SQL auf dem Standortservercomputer.  

    - **Datenbankname**: Standardmäßig ist diese Option auf `CM_<Sitecode>` festgelegt. Sie können diesen Wert anpassen.  

    - **Service Broker-Port**: In der Standardeinstellung ist dieser Wert auf die Verwendung des standardmäßigen SQL Server Service Broker-Ports (SSB) 4022 festgelegt. SQL kommuniziert damit direkt mit der Standortdatenbank an anderen Standorten.  

13. Auf der zweiten Seite **Datenbankinformationen** können Sie benutzerdefinierte Speicherorte für die SQL Server-Datendatei und die SQL Server-Protokolldatei für die Standortdatenbank angeben:  

    - Standardmäßig werden die Standard-Dateispeicherorte für SQL Server verwendet.  

    - Wenn Sie einen SQL Server-Cluster verwenden, ist die Option zur Angabe der benutzerdefinierten Dateispeicherorte nicht verfügbar.  

    - Von der Voraussetzungsprüfung wird nicht überprüft, ob für die benutzerdefinierten Dateispeicherorte genügend Speicherplatz vorhanden ist.  

14. Geben Sie auf der Seite **SMS-Anbietereinstellungen** den vollqualifizierten Domänennamen (FQDN) des Servers an, auf dem der SMS-Anbieter installiert werden soll.  

    - Standardmäßig wird der Standortserver angegeben.  

    - Nach der Standortinstallation können Sie zusätzliche SMS-Anbieter konfigurieren. Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

15. Geben Sie auf der Seite **Kommunikationseinstellungen für Clientcomputer** an, ob von allen Standortsystemen ausschließlich die HTTPS-Kommunikation mit Clients zugelassen werden soll oder ob die Kommunikationsmethode für jede Standortsystemrolle konfiguriert werden muss.  

    Wenn Sie die Option **Alle Standortsystemrollen lassen ausschließlich die HTTPS-Kommunikation mit Clients zu** auswählen, ist für den Clientcomputer ein gültiges PKI-Zertifikat zur Clientauthentifizierung erforderlich. Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Dieser Schritt ist nur nötig, wenn Sie einen primären Standort installieren. Wenn sie einen Standort der zentralen Verwaltung installieren, überspringen Sie diesen Schritt.  

16. Geben Sie auf der Seite **Standortsystemrollen** an, ob ein Verwaltungspunkt oder ein Verteilungspunkt installiert werden soll. Für jede gewählte Rolle, die von Setup installiert werden soll, gelten diese Voraussetzungen:  

    - Geben Sie den **FQDN** des Servers ein, der die Rolle hostet. Wählen Sie dann die Clientverbindungsmethode aus, die vom Server unterstützt wird: HTTP oder HTTPS.  

    - Falls Sie auf der vorherigen Seite die Option **Alle Standortsystemrollen lassen ausschließlich die HTTPS-Kommunikation mit Clients zu** ausgewählt haben, werden die Clientverbindungseinstellungen automatisch für HTTPS konfiguriert. Sie können diese Einstellung nur ändern, wenn Sie zur vorherigen Seite zurückkehren.  

    > [!NOTE]  
    > Dieser Schritt ist nur nötig, wenn Sie einen primären Standort installieren. Wenn sie einen Standort der zentralen Verwaltung installieren, überspringen Sie diesen Schritt.  

    > [!NOTE]  
    > Zum Installieren der Standortsystemrollen wird von Setup das **Standortsystem-Installationskonto**verwendet. Standardmäßig wird das Computerkonto des primären Standorts verwendet. Dieses Konto muss einem lokalen Administrator auf einem Remotecomputer gehören, um die Standortsystemrolle zu installieren. Wenn dieses Konto nicht über die erforderlichen Berechtigungen verfügt, deaktivieren Sie die Standortsystemrollen, und installieren Sie sie später über die Configuration Manager-Konsole, nachdem weitere Konten für die Verwendung als Standortsystem-Installationskonten konfiguriert wurden. Weitere Informationen finden Sie unter [Konten](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. Überprüfen Sie auf der Seite **Nutzungsdaten** die Informationen zu Daten, die von Microsoft gesammelt werden, und klicken Sie dann auf **Weiter**. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. Die Seite **Dienstverbindungspunkt einrichten** ist nur in den folgenden Szenarien verfügbar:  

    - Wenn Sie einen eigenständigen primären Standort installieren.  

    - Wenn Sie einen Standort der zentralen Verwaltung installieren.  

    > [!NOTE]  
    > Wenn Sie einen untergeordneten primären Standort installieren, überspringen Sie diesen Schritt.  

     Wenn Sie einen Standort der zentralen Verwaltung als Teil eines Standorterweiterungsszenarios installieren und diese Rolle bereits an dem eigenständigen primären Standort installiert ist, deinstallieren Sie zuerst diese Rolle am eigenständigen primären Standort. In einer Hierarchie ist nur eine Instanz dieser Rolle zulässig, und sie wird nur für den obersten Standort der Hierarchie unterstützt.  

     Nach Auswahl einer Konfiguration für den **Dienstverbindungspunkt** klicken Sie auf **Weiter**. Nach Abschluss des Setups können Sie diese Konfiguration in der Configuration Manager-Konsole ändern. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../configure/about-the-service-connection-point.md).  

19. Überprüfen Sie auf der Seite **Zusammenfassung der Einstellungen** die Einstellung, die Sie ausgewählt haben. Wenn Sie bereit sind, wählen Sie **Weiter** aus, um die Voraussetzungsprüfung zu starten.  

20. Auf der Seite **Voraussetzungsprüfung** werden etwaige Probleme aufgelistet, die die Prüfung identifizieren kann.  

    - Wenn bei der Voraussetzungsprüfung ein Problem festgestellt wird, klicken Sie in der Liste auf einen Eintrag, um Details zur Behebung des Problems anzuzeigen.  

    - Bevor Sie die Installation des Standorts fortsetzen können, lösen Sie die**Fehler**-Elemente auf. Korrigieren Sie nach Möglichkeit auch Elemente mit dem Status **Warnung**, welche die Installation des Standorts nicht blockieren.  

    - Nach dem Beheben von Problemen klicken Sie auf **Prüfung ausführen**, um die Voraussetzungsprüfung erneut auszuführen.  

        Wenn die Voraussetzungsprüfung ausgeführt wird und nicht der Status **Fehler** gemeldet wird, können Sie auf **Installation starten** klicken, um die Installation des Standorts zu starten.  

    > [!TIP]  
    > Zusätzlich zu dem Feedback des Assistenten finden Sie weitere Informationen zu Problemen mit den Voraussetzungen in der **ConfigMgrPrereq.log**-Datei. Sie befindet sich im Stammverzeichnis des Systemlaufwerks des Computers, auf dem Sie den Standort installieren. Weitere Informationen finden Sie unter [Liste der Voraussetzungsprüfungen](list-of-prerequisite-checks.md).  

21. Auf der Seite **Installation** wird der Installationsstatus von Setup angezeigt. Nach Abschluss der Installation des Hauptstandortservers können Sie den Installationsassistenten mit der Option **Schließen** beenden. Nachdem Sie den Assistenten geschlossen haben, werden die Installation und Erstkonfiguration des Standorts im Hintergrund fortgesetzt.  

    - Bevor das Setup abgeschlossen ist, können Sie eine Configuration Manager-Konsole mit dem Standort verbinden. Diese Konsole stellt eine schreibgeschützte Verbindung her und ermöglicht Ihnen das Anzeigen, jedoch nicht das Bearbeiten von Objekten und Einstellungen.  

    - Nach dem Abschluss des Setups können Sie eine Verbindung mit einer Konsole herstellen, über die Sie Objekte und Einstellungen bearbeiten können.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Erweitern eines eigenständigen primären Standorts

Wenn Sie einen eigenständigen primären Standort als ersten Standort installiert haben, können Sie diesen Standort zu einem späteren Zeitpunkt in eine größere Hierarchie erweitern, indem Sie einen Standort der zentralen Verwaltung installieren.

Wenn Sie einen eigenständigen primären Standort erweitern, installieren Sie einen neuen Standort der zentralen Verwaltung, der die Datenbank des vorhandenen eigenständigen primären Standorts als Referenz verwendet. Nach Installation des neuen Standorts der zentralen Verwaltung fungiert der eigenständige primäre Standort als untergeordneter primärer Standort.

- Sie können nur einen eigenständigen primären Standort in einer neuen Hierarchie erweitern.  

- Sie können nur einen eigenständigen primären Standort in einer bestimmten Hierarchie erweitern. Sie können über diese Option nicht zusätzliche eigenständige primäre Standorte derselben Hierarchie hinzufügen. Verwenden Sie stattdessen den Migrations-Assistenten, um Daten aus einer Hierarchie in eine andere zu migrieren. Weitere Informationen finden Sie unter [Migrieren von Daten zwischen Hierarchien](../../../migration/migrate-data-between-hierarchies.md).  

- Nachdem Sie einen eigenständigen Standort in eine Hierarchie mit einem Standort der zentralen Verwaltung erweitert haben, können Sie weitere untergeordnete primäre Standorte hinzufügen.  

- Zum Entfernen eines primären Standorts aus einer Hierarchie mit einem Standort der zentralen Verwaltung deinstallieren Sie zuerst den primären Standort.  

Um den Standort zu erweitern, verwenden Sie den Setup-Assistenten für Configuration Manager, um einen neuen Standort der zentralen Verwaltung mit folgenden Einschränkungen zu installieren:  

- Installieren Sie den Standort der zentralen Verwaltung mit derselben Version von Configuration Manager, mit der der eigenständige primäre Standort installiert wird.  

- Wählen Sie auf der Seite **Erste Schritte** des Setup-Assistenten die Option zum Installieren eines Standorts der zentralen Verwaltung aus. In einer späteren Phase von Setup wählen Sie eine Option zum Erweitern eines vorhandenen eigenständigen primären Standorts aus.  

- Wenn Sie die Seite **Clientsprachauswahl** für den neuen Standort der zentralen Verwaltung konfigurieren, wählen Sie dieselben Clientsprachen aus, die für den eigenständigen primären Standort konfiguriert werden, den Sie erweitern.  

- Auf der Seite **Standortinstallation** wählen Sie die Option zum Erweitern des eigenständigen primären Standorts aus.  

Bevor Sie einen eigenständigen primären Standort erweitern, informieren Sie sich über die [Voraussetzungen für die Erweiterung eines eigenständigen primären Standorts](prerequisites-for-installing-sites.md#bkmk_expand). Wenden Sie dann das weiter oben in diesem Artikel beschriebene Verfahren [So installieren Sie einen primären Standort oder einen Standort der zentralen Verwaltung](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) an.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> Installieren eines sekundären Standorts

Installieren Sie mithilfe der Configuration Manager-Konsole einen sekundären Standort.  

- Wenn die verwendete Konsole nicht mit dem primären Standort verbunden ist, welcher der übergeordnete Standort des neuen sekundären Standorts sein wird, wird der Befehl zum Installieren des Standorts an den ordnungsgemäßen primären Standort repliziert.  

- Stellen Sie vor der Installation des Standorts sicher, dass Ihr Benutzerkonto über die erforderlichen Berechtigungen verfügt. Stellen Sie außerdem sicher, dass der Server, der den neuen sekundären Standort hostet, alle Voraussetzungen für die Verwendung als sekundärer Standortserver erfüllt.  

- Wenn Sie den sekundären Standort installieren, konfiguriert Configuration Manager den neuen Standort für das Verwenden der Clientkommunikationsports, die am übergeordneten primären Standort konfiguriert sind.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Vorgang zum Installieren eines sekundären Standorts  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie den Standort aus, der der übergeordnete primäre Standort des neuen sekundären Standorts sein wird.  

2. Wählen Sie zum Starten des **Assistenten zum Erstellen sekundärer Standorte** die Option **Sekundären Standort erstellen** im Menüband aus.  

3. Überprüfen Sie auf der Seite **Bevor Sie beginnen**, ob der aufgeführte primäre Standort der Standort ist, der dem neuen sekundären Standort übergeordnet sein soll. Wählen Sie anschließend **Weiter** aus.  

4. Geben Sie auf der Seite **Allgemein** die folgenden Einstellungen an:  

    - **Standortcode:** Jeder Standortcode in einer Hierarchie muss eindeutig sein. Verwenden Sie drei alphanumerische Zeichen: A bis Z und 0 bis 9. Da der Standortcode in Ordnernamen verwendet wird, dürfen keine für Windows reservierten Namen wie die folgenden verwendet werden:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > Setup überprüft nicht, ob der angegebene Standortcode bereits verwendet wird oder ein reservierter Name ist.  

    - **Standortservername:** Dieser Wert ist der FQDN des Servers, auf dem der neue sekundäre Standort installiert wird.  

    - **Standortname:** Jeder Standort benötigt diesen Anzeigenamen, mit dem Sie den Standort bestimmen können.  

    - **Installationsordner:** Dieser Ordner ist der Pfad zur Configuration Manager-Installation. Sie können den Speicherort nach der Installation des Standorts nicht mehr ändern. Der Pfad darf keine Unicode-Zeichen oder Leerzeichen enthalten.  

    > [!IMPORTANT]  
    > Nachdem Sie die Details auf dieser Seite angeben haben, können Sie **Zusammenfassung** auswählen, um direkt zur Seite **Zusammenfassung** des Assistenten zu gelangen. Diese Aktion verwendet die Standardeinstellungen für die restlichen Optionen für den sekundären Standort.  
    > 
    > - Verwenden Sie diese Option nur, wenn Sie mit den Standardeinstellungen des Assistenten vertraut und dies die Einstellungen sind, die Sie verwenden möchten.  
    > - Wenn Sie die Standardeinstellungen verwenden, werden Begrenzungsgruppen nicht dem Verteilungspunkt zugeordnet. Bis Sie Begrenzungsgruppen konfigurieren, die den sekundären Standortserver enthalten, werden Clients nicht den Verteilungspunkt, der auf diesem sekundären Standort installiert ist, als Quellspeicherort für Inhalt verwenden.  

5. Wählen Sie auf der Seite **Installationsquelldateien** aus, wie der Computer des sekundären Standorts Quelldateien für die Installation des Standorts erhält.  

    Wenn Sie CD.Latest-Quelldateien verwenden, die im Netzwerk freigegeben oder lokal auf den gewünschten sekundären Standortserver kopiert werden:  

    - **Version 1802 und früher**

        - Der Speicherort der CD.Latest-Quelldatei enthält einen Ordner namens **Redist**. Verschieben Sie diesen **Redist**-Ordner als Unterordner unter den **SMSSETUP**-Ordner.  

            > [!Note]  
            > Wenn Hashkonfliktfehler während des Setups auftreten, aktualisieren Sie den **Redist**-Ordner. Verwenden Sie das [Setup-Downloadprogramm](setup-downloader.md) zum Abrufen der neuesten Dateien. Kopieren Sie alle Dateien, die einen Hashkonfliktfehler auslösen, außerdem aus dem aktualisierten **Redist**-Ordner in den **SMSSETUP\BIN\X64**-Ordner.

    - **Version 1806 und höher**<!-- SCCMDocs-pr issue 3164 -->

        - Der Speicherort der CD.Latest-Quelldatei enthält einen Ordner namens **Redist**. Verschieben Sie diesen **Redist**-Ordner als Unterordner unter den **SMSSETUP**-Ordner.  

        - Kopieren Sie die folgenden Dateien aus dem **Redist**-Ordner in den **SMSSETUP\BIN\X64**-Ordner:  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Wenn Dateien aus **Redist** nicht verfügbar sind, kann Setup den sekundären Standort nicht installieren.  

    - Das Computerkonto des Servers des sekundären Standorts muss über die Berechtigung **Lesen** für den Quelldateiordner und die Freigabe verfügen.  

6. Geben Sie auf der Seite **SQL Server-Einstellungen** die zu verwendende Version von SQL Server an, und konfigurieren Sie dann die entsprechenden Einstellungen.  

    > [!NOTE]  
    > Die von Ihnen auf dieser Seite eingegebenen Informationen werden von Setup erst zu Beginn der Installation überprüft. Überprüfen Sie diese Einstellungen, und setzen Sie dann den Vorgang fort.  

    - **Lokale Kopie von SQL Server Express auf dem Computer des sekundären Standorts installieren und konfigurieren**  

        - **SQL Server-Dienstport**: Geben Sie den SQL Server-Dienstport an, der von SQL Server Express verwendet werden soll. Der Dienstport ist in der Regel zur Verwendung von TCP-Port 1433 konfiguriert, aber Sie können auch einen anderen Port konfigurieren.  

        - **SQL Server Broker-Port**: Geben Sie den SSB-Port (SQL Server Service Broker) an, der von SQL Server Express verwendet werden soll. Der Service Broker ist in der Regel zur Verwendung von TCP-Port 4022 konfiguriert, aber Sie können auch einen anderen Port konfigurieren. Geben Sie einen gültigen Port an, der von keinem anderen Standort oder Dienst verwendet wird und nicht durch Firewalleinschränkungen blockiert ist.  

    - **Vorhandene SQL Server-Instanz verwenden**  

        - **SQL Server-Name (FQDN):** Prüfen Sie den FQDN des Computers, der SQL Server ausführt. Zum Hosten der sekundären Standortdatenbank müssen Sie einen lokalen Server verwenden, der SQL Server ausführt. Diese Einstellung kann nicht geändert werden.  

        - **SQL Server-Instanz**: Geben Sie die SQL Server-Instanz an, die als Datenbank des sekundären Standorts verwendet werden soll. Lassen Sie diese Option leer, wenn Sie die Standardinstanz verwenden möchten.  

        - **Name der ConfigMgr-Standortdatenbank**: Geben Sie den Namen der Datenbank des sekundären Standorts an.  

        - **SQL Server Broker-Port**: Geben Sie den SSB-Port (SQL Server Service Broker) an, der von SQL Server verwendet werden soll. Geben Sie einen gültigen Port an, der von keinem anderen Standort oder Dienst verwendet wird und nicht durch Firewalleinschränkungen blockiert ist.  

    > [!TIP]  
    > Eine Liste der SQL Server-Versionen, die von Configuration Manager unterstützt werden, finden Sie unter [Unterstützte Versionen von SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md).  

7. Auf der Seite **Verteilungspunkt** konfigurieren Sie Einstellungen für den Verteilungspunkt, der auf dem sekundären Standortserver installiert wird.  

    - **Erforderliche Einstellungen:**  

        - **Specify how client devices communicate with the distribution point** (Angeben, wie Clientgeräte mit dem Verteilungspunkt kommunizieren): Wählen Sie zwischen HTTP und HTTPS.  

        - **Erstellen Sie ein selbstsigniertes Zertifikat, oder importieren Sie ein PKI-Clientzertifikat:** Wählen Sie zwischen der Verwendung eines selbstsignierten Zertifikats und dem Importieren eines Zertifikats von Ihrer PKI. Mit einem selbstsignierten Zertifikat können Sie auch anonyme Verbindungen von Configuration Manager-Clients mit der Inhaltsbibliothek zulassen. Das Zertifikat wird zum Authentifizieren des Verteilungspunkts bei einem Verwaltungspunkt verwendet, bevor Statusmeldungen vom Verteilungspunkt gesendet werden. Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

    - **Optionale Einstellungen:**  

        - **IIS installieren und konfigurieren, sofern dies für Configuration Manager erforderlich ist:** Wählen Sie diese Einstellung aus, damit Internetinformationsdienste (IIS) gegebenenfalls von Configuration Manager auf dem Server installiert und konfiguriert werden. IIS ist auf allen Verteilungspunkten erforderlich.  

            > [!NOTE]  
            > Wenngleich diese Einstellung optional ist, muss IIS auf dem Server installiert sein, bevor ein Verteilungspunkt erfolgreich installiert werden kann.  

        - **Aktivieren und Konfigurieren von BranchCache für diesen Verteilungspunkt**  

        - **Beschreibung:** Dieser Wert ist eine benutzerfreundliche Beschreibung des Verteilungspunkts, um ihn leichter zu erkennen.  

        - **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren**  

8. Legen Sie auf der Seite **Laufwerkseinstellungen** die Laufwerkseinstellungen für den Verteilungspunkt des sekundären Standorts fest.  

    Sie können bis zu zwei Laufwerke für die Inhaltsbibliothek und zwei Laufwerke für die Paketfreigabe konfigurieren. Configuration Manager kann jedoch zusätzliche Laufwerke verwenden, wenn die ersten beiden die konfigurierte Laufwerksspeicherreserve erreichen. Auf der Seite **Laufwerkseinstellungen** werden die Priorität der Laufwerke und der freie Speicherplatz, der auf jedem Laufwerk verbleiben muss, festgelegt.  

    - **Laufwerksspeicherreserve (MB):** Hiermit geben Sie an, wie viel freier Speicher auf einem Laufwerk verbleiben muss. Wird der Wert erreicht, wählt Configuration Manager ein anderes Laufwerk aus, auf dem der Kopiervorgang fortgesetzt wird. Inhaltsdateien können sich über mehrere Laufwerke erstrecken.  

    - **Inhaltsorte**: Geben Sie die Inhaltsorte für die Inhaltsbibliothek und die Paketfreigabe an. Configuration Manager kopiert solange Inhalte zum primären Inhaltsort, bis die Menge des freien Speicherplatzes den unter **Laufwerksspeicherreserve (MB)** angegebenen Wert erreicht.  

    Die Inhaltsorte sind standardmäßig auf **Automatisch**festgelegt. Der primäre Inhaltsort wird auf das Laufwerk festgelegt, das bei der Installation über den meisten Speicherplatz verfügt. Der sekundäre Inhaltsort wird auf das Laufwerk festgelegt, das nach dem primären Laufwerk über den meisten freien Speicherplatz verfügt. Wenn vom primären und sekundären Laufwerk die Laufwerksspeicherreserve erreicht wird, wählt Configuration Manager ein anderes verfügbares Laufwerk mit dem meisten freien Speicherplatz aus und setzt den Kopiervorgang dort fort.  

9. Geben Sie auf der Seite **Inhaltsprüfung** an, ob die Integrität der Inhaltsdateien am Verteilungspunkt geprüft werden soll.  

    - Wenn Sie die Inhaltsprüfung nach einem Zeitplan aktivieren, startet Configuration Manager den Vorgang zum festgesetzten Zeitpunkt. Alle Inhalte auf dem Verteilungspunkt werden überprüft.  

    - Sie können auch die **Priorität der Inhaltsprüfung**konfigurieren.  

    - Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Verteilungsstatus**, und wählen Sie dann den Knoten **Inhaltsstatus** aus. Der Inhalt jedes Pakettyps wird angezeigt. Diese Typen sind z.B. Anwendungen, Softwareupdatepakete, und Startimages.  

10. Auf der Seite **Begrenzungsgruppen** können Sie die Begrenzungsgruppen verwalten, denen dieser Verteilungspunkt zugewiesen ist:  

    - Bei der Inhaltsbereitstellung müssen sich die Clients in einer dem Verteilungspunkt zugeordneten Begrenzungsgruppe befinden, damit der Verteilungspunkt als Quellort für Inhalt verwendet werden kann.  

    - Sie können das Kontrollkästchen **Fallbackquellpfad für Inhalt zulassen** aktivieren, um Clients außerhalb solcher Begrenzungsgruppen ein Ausweichen auf den Verteilungspunkt als Quellort für den Inhalt zu ermöglichen, wenn keine bevorzugten Verteilungspunkte verfügbar sind.  

        Weitere Informationen finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung in Configuration Manager](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen. Klicken Sie dann auf **Weiter**, um den sekundären Standort zu installieren. Wenn der Assistent die Seite **Abschluss** anzeigt, können Sie den Assistenten schließen. Die Installation des sekundären Standorts wird im Hintergrund fortgesetzt.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> So überprüfen Sie den Installationsstatus des sekundären Standorts  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Wählen Sie den sekundären Standort aus, den Sie installieren, und dann **Installationsstatus anzeigen** im Menüband.  

    > [!TIP]  
    > Wenn Sie mehrere sekundäre Standorte gleichzeitig installieren, wird die Voraussetzungsprüfung immer nur für jeweils einen Standort ausgeführt. Die Prüfung eines Standorts muss abgeschlossen sein, damit der nächste geprüft werden kann.  
