---
title: Konfigurieren der Berichterstellung
titleSuffix: Configuration Manager
description: Vorgehensweise beim Einrichten der Berichterstellung in der Configuration Manager-Hierarchie, einschließlich Informationen zu SQL Server Reporting Services.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ba67fee260867494302e49b7c9d3a97480e236b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708378"
---
# <a name="configure-reporting-in-configuration-manager"></a>Konfigurieren der Berichterstattung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können in der Configuration Manager-Konsole nur dann Berichte erstellen, ändern und ausführen, nachdem Sie einige Konfigurationstasks erledigt haben. In diesem Artikel wird erläutert, wie Sie die Berichterstellung in der Configuration Manager-Hierarchie konfigurieren.  

Lesen Sie zunächst die folgenden Artikel zur Berichterstellung in Configuration Manager, bevor Sie SQL Server Reporting Services in der Hierarchie installieren und konfigurieren:  

- [Introduction to reporting (Einführung in die Berichterstellung)](introduction-to-reporting.md)  

- [Planen der Berichterstellung](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services ist eine serverbasierte Berichterstattungsplattform, von der umfassende Berichterstattungsfunktionen für verschiedene Arten von Datenquellen bereitgestellt werden. Der Reporting Services-Punkt in Configuration Manager kommuniziert mit SQL Server Reporting Services, um Folgendes durchzuführen:

- Kopieren von Configuration Manager-Berichten in einen bestimmten Berichtsordner
- Konfigurieren der Einstellungen der Reporting Services
- Konfigurieren der Sicherheitseinstellungen der Reporting Services

Wenn Sie einen Bericht ausführen, stellt die Reporting Services-Komponente eine Verbindung mit der Configuration Manager-Standortdatenbank her, um Daten abzurufen.  

Die Installation des Reporting Services-Punkts an einem Configuration Manager-Standort ist erst möglich, nachdem Sie SQL Server Reporting Services auf dem Zielstandortsystem installiert und konfiguriert haben. Weitere Informationen finden Sie unter [Installieren von SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).  

### <a name="verify-sql-server-reporting-services-installation"></a>Überprüfen einer Installation von SQL Server Reporting Services

Gehen Sie wie folgt vor, um zu überprüfen, ob SQL Server Reporting Services ordnungsgemäß installiert ist und ausgeführt wird.

1. Wechseln Sie auf dem Standortsystem zum **Startmenü**, und öffnen Sie **Konfigurations-Manager für Reporting Services**. Sie finden es möglicherweise im Abschnitt **Konfigurationstools** der **Microsoft SQL Server**-Gruppe.

2. Geben Sie im Fenster **Konfigurationsverbindung für Reporting Services** den Namen des Servers ein, der SQL Server Reporting Services hostet. Wählen Sie die Instanz von SQL Server aus, auf der Sie SQL Reporting Services installiert haben. Wählen Sie dann **Verbinden** aus, um den Konfigurations-Manager für Reporting Services zu öffnen.  

3. Überprüfen Sie auf der Seite **Berichtsserverstatus**, ob der **Berichtsdienststatus** den Wert **Gestartet** hat. Wenn dieser Status nicht vorliegt, wählen Sie **Starten** aus.  

4. Wählen Sie auf der Seite **Webdienst-URL** die URL in **URLs für Berichtsdienst-Webdienst** aus. Mit dieser Aktion wird die Verbindung mit dem Berichtsordner getestet. Der Browser könnte Sie zur Eingabe von Anmeldeinformationen auffordern. Überprüfen Sie, ob die Webseite erfolgreich geöffnet wird.

5. Überprüfen Sie auf der Seite **Datenbank**, ob für **Berichtsservermodus** die Einstellung **Nativ** festgelegt ist.  

6. Wählen Sie auf der Seite **Berichts-Manager-URL** die URL in **Identifikation der Berichts-Manager-Site** aus. Diese Aktion testet die Verbindung mit dem virtuellen Verzeichnis für den Berichts-Manager. Der Browser könnte Sie zur Eingabe von Anmeldeinformationen auffordern. Überprüfen Sie, ob die Webseite erfolgreich geöffnet wird.

    > [!NOTE]  
    > Für die Berichterstattung in Configuration Manager ist der Berichts-Manager für Reporting Services nicht erforderlich. Sie benötigen ihn nur, wenn Sie Berichte im Browser ausführen oder Berichte verwalten möchten, indem Sie den Berichts-Manager verwenden.  

7. Wählen Sie **Beenden** aus, um den Konfigurations-Manager für Reporting Services zu schließen.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Konfigurieren der Berichterstellung zur Verwendung von Report Builder 3.0

1. Öffnen Sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, den Windows-Registrierungs-Editor.  

2. Navigieren Sie zu `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Öffnen Sie den Schlüssel **ReportBuilderApplicationManifestName**, um den Wert zu bearbeiten.  

4. Ändern Sie den Wert in `ReportBuilder_3_0_0_0.application`, und wählen Sie dann zum Speichern **OK** aus.

5. Schließen Sie den Windows Registrierungs-Editor.  

## <a name="install-a-reporting-services-point"></a>Installieren eines Reporting Services-Punkts

Um Berichte am Standort zu verwalten, installieren Sie den Reporting Services-Punkt. Der Reporting Services-Punkt:

- Kopiert Berichts Ordner und Berichte in SQL Server Reporting Services
- Wendet die Sicherheitsrichtlinie für die Berichte und Ordner an
- Legt Konfigurationseinstellungen in Reporting Services fest

### <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

Bevor Sie Berichte in der Configuration Manager-Konsole anzeigen oder verwalten können, benötigen Sie einen Reporting Services-Punkt. Konfigurieren Sie diese Standortsystemrolle auf einem Server mit Microsoft SQL Server Reporting Services. Weitere Informationen finden Sie unter [Voraussetzungen für die Berichterstattung in System Center Configuration Manager](prerequisites-for-reporting.md).  

- Bedenken Sie bei der Auswahl eines Standorts zum Installieren des Reporting Services-Punkts, dass die Benutzer, die auf die Berichte zugreifen werden, sich im selben Sicherheitsbereich befinden müssen wie der Standort, an dem Sie die Rolle installieren.  

- Lassen Sie die URL des Berichtsservers unverändert, nachdem Sie einen Reporting Services-Punkt in einem Standortsystem installiert haben.

    Sie erstellen beispielsweise den Reporting Services-Punkt. Anschließend ändern Sie die URL für den Berichtsserver im Konfigurations-Manager für Reporting Services. Die Configuration Manager-Konsole verwendet weiterhin die alte URL. Sie können keine Berichte über die-Konsole ausführen, bearbeiten oder erstellen.

    Wenn Sie die Berichtsserver-URL ändern müssen, entfernen Sie zuerst den vorhandenen Reporting Services-Punkt. Ändern Sie die URL, und installieren Sie den Reporting Services-Punkt neu.  

- Wenn Sie einen Reporting Services-Punkt installieren, geben Sie ein [Konto eines Reporting Services-Punkts](../../plan-design/hierarchy/accounts.md#reporting-services-point-account) an. Erstellen Sie eine bidirektionale Vertrauensstellung zwischen Domänen, damit Benutzer aus einer anderen Domäne einen Bericht ausführen können. Andernfalls kann der Bericht nicht ausgeführt werden.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> Installieren des Reporting Services-Punkts in einem Standortsystem  

Weitere Informationen zum Konfigurieren von Standortsystemen finden Sie unter [Installieren von Standortsystemrollen](../deploy/configure/install-site-system-roles.md).  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie dann den Knoten **Server und Standortsystemrollen** aus.  

1. Fügen Sie den Reporting Services-Punkt einem neuen oder vorhandenen Standortsystem hinzu:  

    - *Neues Standortsystem:* Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Standortsystemserver erstellen** aus. Der **Assistent zum Erstellen von Standortsystemservern** wird geöffnet.  

    - *Vorhandenes Standortsystem:* Wählen Sie den Zielserver aus. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Server** die Option **Standortsystemrolle hinzufügen** aus. Der **Assistent zum Hinzufügen von Standortsystemrollen** wird geöffnet.  

1. Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an. Wenn Sie den Reporting Services-Punkt einem vorhandenen Server hinzufügen, überprüfen Sie die Werte, die Sie zuvor konfiguriert haben.  

1. Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen den Eintrag **Reporting Services-Punkt** aus. Wählen Sie dann **Weiter** aus.  

1. Konfigurieren Sie auf der Seite **Reporting Services-Punkt** die folgenden Einstellungen:  

    - **Name des Standortdatenbankservers:** Geben Sie den Namen des Servers an, auf dem die Configuration Manager-Standortdatenbank gehostet wird. Der vollqualifizierte Domänenname (Fully Qualified Domain Name, FQDN) für den Server wird vom Assistenten in der Regel automatisch abgerufen. Zur Angabe einer Datenbankinstanz verwenden Sie das Format &lt;*Servername*>\&lt;*Instanzname*>. Beispiel: `sqlserver\named1`.

    - **Datenbankname**: Geben Sie den Namen der Configuration Manager-Standortdatenbank an. Wählen Sie **Überprüfen** aus, um zu bestätigen, dass der Assistent auf die Standortdatenbank zugreifen kann.  

        > [!IMPORTANT]  
        > Das Benutzerkonto, das Sie zum Erstellen des Reporting Services-Punkt verwenden, muss die Berechtigung **Lesen** für die Standortdatenbank haben. Wenn beim Verbindungstest ein Fehler auftritt, wird ein rotes Warnsymbol angezeigt. Der kontextabhängige Hovertext auf dem Symbol weist die Details des Fehlers auf. Korrigieren Sie den Fehler, und wählen Sie dann erneut **Test** aus.  

    - **Ordnername:** Geben Sie den Namen des Ordners an, der erstellt und für Configuration Manager-Berichte in Reporting Services verwendet wird.  

    - **Reporting Services-Serverinstanz:** Wählen Sie die SQL Server-Instanz für Reporting Services aus. Wenn auf dieser Seite keine Instanzen aufgeführt sind, überprüfen Sie, ob SQL Server Reporting Services installiert, konfiguriert und gestartet ist.  

        > [!IMPORTANT]  
        > Configuration Manager stellt im Kontext des aktuellen Benutzers eine Verbindung mit WMI auf dem ausgewählten Standortsystem her. Diese Verbindung wird verwendet, um die Instanz von SQL Server für Reporting Services abzurufen. Der aktuelle Benutzer muss über die Berechtigung **Lesen** für WMI auf dem Standortsystem verfügen. Andernfalls kann der Assistent die Reporting Services-Instanzen nicht abrufen.  

    - **Konto des Reporting Services-Punkts**: Wählen Sie **Festlegen** und dann ein zu verwendendes Konto aus. SQL Server Reporting Services auf dem Reporting Services-Punkt stellt mit diesem Konto die Verbindung mit der Configuration Manager-Standortdatenbank her. Diese Verbindung dient zum Abrufen der Daten für einen Bericht. Wählen Sie **Vorhandenes Konto** aus, um ein Windows-Benutzerkonto anzugeben, das Sie zuvor als Configuration Manager-Konto konfiguriert haben. Wählen Sie **Neues Konto** aus, um ein Windows-Benutzerkonto anzugeben, das derzeit nicht für die Verwendung konfiguriert ist. Dem angegebenen Benutzer wird von Configuration Manager automatisch Zugriff auf die Standortdatenbank erteilt.  

        Das Konto, über das Reporting Services ausgeführt wird, muss zur lokalen Sicherheitsgruppe **Windows-Autorisierungszugriffsgruppe** der Domäne gehören. Außerdem muss die Berechtigung **tokenGroupsGlobalAndUniversal lesen** auf **Zulassen** festgelegt sein. Für Benutzer, die zu einer anderen Domäne als das Konto des Reporting Services-Punkts gehören, muss zur erfolgreichen Ausführung von Berichten eine bidirektionale Vertrauensstellung eingerichtet sein.

        Das angegebene Windows-Benutzerkonto und das zugehörige Kennwort werden verschlüsselt und in der Reporting Services-Datenbank gespeichert. Die Daten werden von Reporting Services über dieses Konto und Kennwort aus der Standortdatenbank abgerufen und für Berichte verwendet.  

        > [!IMPORTANT]  
        > Das angegebene Konto muss auf dem Server, auf dem die Reporting Services-Datenbank gehostet wird, über die Berechtigung **Lokal anmelden zulassen** verfügen.  

1. Schließen Sie den Assistenten ab.

Nachdem der Assistent abgeschlossen ist, erstellt Configuration Manager die Berichtsordner in Reporting Services. Anschließend werden die Berichte in die angegebenen Berichtsordner kopiert.  

> [!TIP]  
> Sollen nur die Standortsysteme aufgeführt werden, auf denen die Standortsystemrolle „Reporting Services-Punkt“ gehostet wird, klicken Sie mit der rechten Maustaste auf **Server und Standortsystemrollen**, und wählen Sie **Reporting Services-Punkt** aus.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" /> Sprachen für Berichte

<!-- SCCMDocs#1067 -->

Wenn Configuration Manager Berichtsordner erstellt und Berichte auf den Berichtsserver kopiert, ermittelt Configuration Manager die geeignete Sprache für die Objekte.

- Erstellen von Berichtsordnern, Kopieren von Berichten

  - Erstellen von Objekten mithilfe des Gebietsschemas des Betriebssystems des Standortservers

  - Wenn das spezifische Sprachpaket nicht verfügbar ist, wird standardmäßig Englisch (ENU) verwendet.

- Anzeigen von Berichten in einem Webbrowser

  - Ordner- und Berichtsnamen: das gleiche Gebietsschema wie der Standortserver
  
  - Berichtsinhalte: dynamisch basierend auf dem Browsergebietsschema

- Anzeigen von Berichten in der Configuration Manager-Konsole

  - Ordner- und Berichtsnamen: dynamisch basierend auf dem Gebietsschema der Konsole
  
  - Berichtsinhalte: dynamisch basierend auf dem Gebietsschema der Konsole

Die Berichte werden auch in Englisch installiert, wenn Sie einen Reporting Services-Punkt an einem Standort ohne Sprachpakete installieren. Wenn Sie ein Sprachpaket nach der Installation des Reporting Services-Punkts installieren, müssen Sie den Reporting Services-Punkt deinstallieren und neu installieren, damit die Berichte in der Sprache des gewünschten Sprachpakets verfügbar sind.  

Weitere Informationen finden Sie unter [Sprachpaketen](../deploy/install/language-packs.md).

### <a name="file-installation-and-report-folder-security-rights"></a>Dateiinstallation und Sicherheitsrechte für Berichtsordner

Zur Installation des Reporting Services-Punkts und zur Konfiguration von Reporting Services werden von Configuration Manager die folgenden Aktionen ausgeführt:  

> [!IMPORTANT]  
> Der Standort führt diese Aktionen im Kontext des Kontos aus, das für den SMS_Executive-Dienst konfiguriert ist. In der Regel handelt es sich bei diesem Konto um das lokale Systemkonto des Standortservers.  

- Installieren der Standortrolle „Reporting Services-Punkt“.  

- Erstellen der Datenquelle in Reporting Services mithilfe der gespeicherten Anmeldeinformationen, die Sie im Assistenten festgelegt haben. Bei diesem Konto handelt es sich um das Windows-Benutzerkonto und das dazugehörende Kennwort, über die von Reporting Services eine Verbindung mit der Standortdatenbank hergestellt wird, wenn Sie Berichte ausführen.  

- Erstellen des Configuration Manager-Stammordners in Reporting Services.  

- Hinzufügen der Sicherheitsrollen **ConfigMgr-Berichtsbenutzer** und **ConfigMgr-Berichtadministratoren** in Reporting Services.  

- Erstellen von Unterordnern und dann Bereitstellen von Configuration Manager-Berichten von `%ProgramFiles%\SMS_SRSRP` auf dem Standortserver für Reporting Services.  

- Hinzufügen der Rolle **ConfigMgr-Berichtsbenutzer** in Reporting Services zu den Stammordnern für alle Benutzerkonten in Configuration Manager, die über **Leseberechtigungen für den Standort** verfügen.  

- Hinzufügen der Rolle **ConfigMgr-Berichtadministratoren** in Reporting Services zu den Stammordnern für alle Benutzerkonten in Configuration Manager, die über **Berechtigungen zum Ändern des Standorts** verfügen.  

- Abrufen der Zuordnung zwischen Berichtsordnern und gesicherten Configuration Manager-Objekttypen. Configuration Manager verwaltet diese Zuordnung in der Standortdatenbank.  

- Konfigurieren der folgenden Rechte für bestimmte Berichtsordner in Reporting Services für Administratoren in Configuration Manager:  

  - Hinzufügen von Benutzern und Zuweisen der Rolle **ConfigMgr-Berichtsbenutzer** zum zugeordneten Berichtsordner für Administratoren, die über die Berechtigung **Bericht ausführen** für das Configuration Manager-Objekt verfügen.  

  - Hinzufügen von Benutzern und Zuweisen der Rolle **ConfigMgr-Berichtadministratoren** zum zugeordneten Berichtsordner für Administratoren, die über die Berechtigung **Bericht ändern** für das Configuration Manager-Objekt verfügen.  

Von Configuration Manager wird eine Verbindung mit Reporting Services hergestellt. Dann werden die Berechtigungen der Benutzer für die Configuration Manager- und Reporting Services-Stammordner sowie für bestimmte Berichtordner festgelegt. Nach der Erstinstallation des Reporting Services-Punkts wird von Configuration Manager alle 10 Minuten eine Verbindung mit Reporting Services hergestellt, um zu überprüfen, ob es sich bei den für die Berichtsordner konfigurierten Benutzerrechten um die entsprechenden Rechte handelt, die für Configuration Manager-Benutzer festgelegt wurden. Wenn mit dem Reporting Services Berichts-Manager Benutzer hinzugefügt bzw. Benutzerrechte für den Berichtordner geändert werden, werden diese Änderungen mithilfe der in der Standortdatenbank gespeicherten rollenbasierten Zuweisungen von Configuration Manager überschrieben. Configuration Manager entfernt auch Benutzer, die nicht zur Berichterstellung in Configuration Manager berechtigt sind.  

### <a name="reporting-services-security-roles"></a>Sicherheitsrollen in Reporting Services

Wenn von Configuration Manager der Reporting Services-Punkt installiert wird, werden in Reporting Services die folgenden Sicherheitsrollen hinzugefügt:  

- **ConfigMgr-Berichtbenutzer:** Benutzer, denen diese Sicherheitsrolle zugewiesen ist, können nur Configuration Manager-Berichte ausführen.  

- **ConfigMgr-Berichtadministratoren:** Benutzer, denen diese Sicherheitsrolle zugewiesen ist, können in Configuration Manager alle auf die Berichterstellung bezogenen Tasks ausführen.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a> Überprüfen der Installation

Überprüfen Sie die Installation des Reporting Services-Punkts anhand bestimmter Statusmeldungen und Protokolldateieinträge. Gehen Sie wie folgt vor, um zu überprüfen, ob der Reporting Services-Punkt erfolgreich installiert wurde.  

> [!Note]  
> Wenn im Arbeitsbereich **Überwachung** der Configuration Manager-Konsole im Unterordner **Berichte** des Knotens **Berichterstellung** Berichte angezeigt werden, können Sie dieses Verfahren überspringen.

### <a name="verify-installation-by-status-message"></a>Überprüfen der Installation anhand der Statusmeldung

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie den **Systemstatus**, und wählen Sie den Knoten **Komponentenstatus** aus.  

1. Wählen Sie die **SMS_SRS_REPORTING_POINT**-Komponente aus.  

1. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Komponente** die Option **Meldungen anzeigen** und dann **Alle** aus.  

1. Geben Sie ein Datum und eine Uhrzeit für einen Zeitraum vor der Installation des Reporting Services-Punkts an, und wählen Sie dann **OK** aus.  

1. Überprüfen Sie die Statusmeldungs-ID **1015**. Diese Statusmeldung weist darauf hin, dass der Reporting Services-Punkt erfolgreich installiert wurde.

### <a name="verify-installation-by-log-file"></a>Überprüfen der Installation anhand der Protokolldatei

Öffnen Sie die Datei **Srsrp.log**, die sich im Verzeichnis **Protokolle** des Configuration Manager-Installationspfads befindet. Suchen Sie nach der Zeichenfolge `Installation was successful`.

Sehen Sie die Protokolldatei ab dem Zeitpunkt der erfolgreichen Installation des Reporting Services-Punkts schrittweise durch. Überprüfen Sie, ob die Berichtsordner erstellt, die Berichte bereitgestellt und die Sicherheitsrichtlinie für jeden Ordner bestätigt wurden. Suchen Sie nach der letzten Zeile der Sicherheitsrichtlinienbestätigungen nach der Zeichenfolge `Successfully checked that the SRS web service is healthy on server`.  

## <a name="configure-a-certificate-to-author-reports"></a>Konfigurieren eines Zertifikats zum Verfassen von Berichten

Es gibt zahlreiche Möglichkeiten, Berichte in SQL Server Reporting Services zu erstellen. Beim Erstellen oder Bearbeiten von Berichten in der Configuration Manager-Konsole wird der Berichts-Generator von Configuration Manager als Erstellungsumgebung geöffnet. Unabhängig von der Erstellungsmethode für Configuration Manager-Berichte benötigen Sie ein selbstsigniertes Zertifikat für die Serverauthentifizierung beim Standortdatenbankserver.

> [!NOTE]  
> Weitere Informationen zum Erstellen von Berichten mit SQL Server Reporting Services finden Sie unter [Erstellungsumgebung des Berichts-Generators (SSRS)](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Von Configuration Manager wird das Zertifikat automatisch auf dem Standortserver und ggf. SMS-Anbieterrollen installiert. Sie können Berichte mithilfe der Configuration Manager-Konsole erstellen oder bearbeiten, wenn Sie sie auf einem dieser Server ausführen.

Wenn Sie Berichte in einer Configuration Manager-Konsole auf einem anderen Computer erstellen oder ändern, exportieren Sie das Zertifikat vom Standortserver. Der Anzeigename des jeweiligen Zertifikats ist der FQDN des Standortservers im **Vertrauenswürdige Personen**-Zertifikatspeicher für den lokalen Computer. Fügen Sie dieses Zertifikat dem Zertifikatspeicher **Vertrauenswürdige Personen** auf dem Computer hinzu, auf dem die Configuration Manager-Konsole ausgeführt wird.  

## <a name="modify-reporting-services-point-settings"></a>Ändern der Einstellungen des Reporting Services-Punkts

Nach der Installation dieser Rolle können Sie die Einstellungen für Standortdatenbankverbindung und Authentifizierung in den Eigenschaften des Reporting Services-Punkts konfigurieren.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie dann den Knoten **Server und Standortsystemrollen** aus.  

    > [!TIP]  
    > Sollen nur die Standortsysteme aufgeführt werden, auf denen der Reporting Services-Punkt gehostet wird, klicken Sie mit der rechten Maustaste auf den Knoten **Server und Standortsystemrollen**, und wählen Sie **Reporting Services-Punkt** aus.  

1. Wählen Sie das Standortsystem aus, das den Reporting Services-Punkt hostet. Wählen Sie dann im Detailbereich die **Reporting Services-Punkt**-Standortsystemrolle aus.

1. Wählen Sie auf dem Menüband auf der Registerkarte **Standortrolle** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

1. Sie können die folgenden Einstellungen im Dialogfeld **Eigenschaften des Reporting Services-Punkts** ändern:  

    - **Name des Standortdatenbankservers**

    - **Datenbankname**

    - **Benutzerkonto**

1. Wählen Sie **OK** aus, um die Änderungen zu speichern und die Eigenschaften zu schließen.  

Weitere Informationen zu diesen Einstellungen finden Sie in den Beschreibungen im Abschnitt [Installieren des Reporting Services-Punkts in einem Standortsystem](#bkmk_install).

## <a name="power-bi-report-server"></a>Power BI-Berichtsserver

Ab Version 2002 können Sie die Berichterstellung mit dem Power BI-Berichtsserver integrieren. Weitere Informationen zur Konfiguration finden Sie unter [Integrieren mit dem Power BI-Berichtsserver](powerbi-report-server.md).

## <a name="upgrade-sql-server"></a>Upgrade von SQL Server

Um SQL Server und SQL Server Reporting Services zu aktualisieren, entfernen Sie zuerst den Reporting Services-Punkt vom Standort. Nachdem Sie SQL Server aktualisiert haben, installieren Sie den Reporting Services-Punkt erneut in Configuration Manager.

Wenn Sie diesen Prozess nicht befolgen, werden Fehlermeldungen angezeigt, wenn Sie Berichte über die Configuration Manager Konsole ausführen oder bearbeiten. Sie können weiterhin erfolgreich Berichte mit einem Webbrowser ausführen und bearbeiten.  

## <a name="configure-report-options"></a>Konfigurieren von Berichtsoptionen

Sie können den standardmäßigen Reporting Services-Punkt auswählen, den Sie zum Verwalten von Berichten verwenden. Der Standort kann über mehrere Reporting Services-Punkte verfügen, er verwendet jedoch nur den Standardserver, um Berichte zu verwalten. Gehen Sie wie folgt vor, um Berichtoptionen für Ihren Standort zu konfigurieren.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus.  

1. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Einstellungen** die Option **Berichtsoptionen** aus.  

1. Wählen Sie in der Liste den Standardberichtsserver aus, und wählen Sie dann **OK** aus.

Wenn keine Server angezeigt werden, überprüfen Sie, ob Sie einen Reporting Services-Punkt auf dem Standort installiert und konfiguriert haben. Weitere Informationen finden Sie unter [Überprüfen der Installation](#bkmk_verify).

Stellen Sie sicher, dass auf Ihrem Computer eine Version von SQL Server Report Builder ausgeführt wird, die mit der Version von SQL Server übereinstimmt, die Sie für den Berichtsserver verwenden. Andernfalls wird eine Fehlermeldung angezeigt, dass der Standardberichtsserver nicht speichern wird, und Sie können keine Berichte erstellen oder bearbeiten.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Nächste Schritte

[Vorgänge und Wartungstasks für die Berichterstellung](operations-and-maintenance-for-reporting.md)
