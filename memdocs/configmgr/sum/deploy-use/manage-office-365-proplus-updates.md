---
title: Verwalten von Office 365 ProPlus-Updates
titleSuffix: Configuration Manager
description: Configuration Manager synchronisiert Office 365-Clientupdates aus dem WSUS-Katalog auf den Standortserver, um Updates zur Bereitstellung für den Client zur Verfügung zu stellen.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 4967b8b289d54a6355cb0a1e6454d5fac469a733
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110405"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Verwalten von Office 365 ProPlus mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Note]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

Mit dem Configuration Manager können Sie Office 365 ProPlus-Apps auf folgende Weise verwalten:

- [Bereitstellen von Office 365-Apps:](#deploy-office-365-apps) Sie können den Office 365-Installer aus dem [Office 365-Clientverwaltungsdashboard](office-365-dashboard.md) starten, um die Erstinstallation der Office 365-App zu vereinfachen. Mit dem Assistenten können Sie die Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen, und eine Skriptanwendung mit dem Inhalt erstellen und bereitstellen.

- [Bereitstellen von Updates für Office 365:](#deploy-office-365-updates) Sie können Updates von Office 365-Clients mithilfe des Workflows zum Verwalten von Softwareupdates verwalten. Wenn Microsoft ein neues Update für Office 365-Clients im Office Content Delivery Network (CDN) veröffentlicht, veröffentlicht Microsoft auch ein Updatepaket in Windows Server Update Services (WSUS). Nachdem Configuration Manager das Office 365-Clientupdate aus dem WSUS-Katalog auf den Standortserver übertragen hat, kann das Update für Clients bereitgestellt werden.

   > [!NOTE]
   > Ab Configuration Manager, Version 2002, können Sie Office 365-Updates in getrennte Umgebungen importieren. Weitere Informationen finden Sie unter [Synchronisieren von Office 365-Updates bei einem getrennten Softwareupdatepunkt](../get-started/synchronize-office-updates-disconnected.md).   

- [Hinzufügen von Sprachen für Downloads des Office 365-Updates:](#bkmk_o365_lang) Sie können Configuration Manager so einrichten, dass das Herunterladen von Updates für alle von Office 365 unterstützen Sprachen unterstützt wird. Das heißt, Configuration Manager muss die Sprache nicht unterstützen, wenn sie bereits von Office 365 unterstützt wird. Vor der Configuration Manager-Version 1610 müssen Sie Updates in der gleichen Sprache herunterladen und bereitstellen, in der die Office 365-Clients konfiguriert sind.

- [Ändern des Updatekanals:](#bkmk_channel) Sie können Sie mit einer Gruppenrichtlinie die Änderung eines Registrierungsschlüsselwerts an Office 365-Clients verteilen, um den Updatekanal zu ändern.

Über das [Office 365-Clientverwaltungsdashboard](office-365-dashboard.md) können Sie Office 365-Clientinformationen überprüfen und einige dieser Office 365-Verwaltungsaktionen starten.

## <a name="deploy-office-365-apps"></a>Bereitstellen von Office 365-Apps  
Starten Sie den Office 365-Installer für die erste Office 365-App-Installation über das Office 365-Clientverwaltungsdashboard. Mit dem Assistenten können Sie die Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen, und eine Skriptanwendung für die Dateien erstellen und bereitstellen. Bis Office 365 auf Clients installiert und das [automatische Office-Update](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) ausgeführt wurde, sind Office 365-Updates nicht anwendbar. Zu Testzwecken können Sie das Update manuell ausführen.

Bei früheren Versionen von Configuration Manager müssen Sie beim ersten Installieren von Office 365-Apps auf Clients folgende Schritte ausführen:
- Herunterladen des Office 365-Bereitstellungstools (ODT)
- Herunterladen der Office 365-Installationsquelldateien einschließlich aller Sprachpakete, die Sie benötigen.
- Generieren der Datei „Configuration.xml“, die die richtige Version von Office und Kanal angibt.
- Erstellen und Bereitstellen entweder eines Legacypakets oder einer Skriptanwendung für Clients zur Installation der Office 365-Apps.

### <a name="requirements"></a>Anforderungen
- Der Computer, der den Office 365-Installer ausführt, muss über Internetzugriff verfügen.  
- Der Benutzer, der den Office 365-Installer ausführt, muss über die Zugriffe **Lesen** und **Schreiben** auf der Freigabe für die im Assistenten bereitgestellten Inhaltsorte verfügen.
- Wenn Sie einen 404-Downloadfehler erhalten, kopieren Sie die folgenden Dateien in den Benutzerorder %temp%:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Bereitstellen von Office 365-Apps mithilfe von Configuration Manager Version 1806 oder höher: 
Ab Configuration Manager 1806 wird das Office-Anpassungstool in den Office 365-Installer in der Configuration Manager-Konsole integriert. Beim Erstellen einer Bereitstellung für Office 365 können Sie die neuesten Verwaltungseinstellungen von Office dynamisch konfigurieren. <!--1358149-->

1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung**.
2. Klicken Sie im oberen rechten Bereich auf **Office 365-Installer**. Der Office 365-Installations-Assistent wird geöffnet.
3. Geben Sie auf der Seite **Anwendungseinstellungen** einen Namen und eine Beschreibung für die App an, geben Sie den Downloadpfad für die Dateien ein, und klicken Sie anschließend auf **Weiter**. Der Speicherort muss in Form von &#92;&#92;*Server*&#92;*Freigabe* angegeben werden.
4. Klicken Sie auf der Seite **Office-Einstellungen** auf **Zum Office-Anpassungstool wechseln**. Dies öffnet das [Office-Anpassungstool für Klick-und-Los](https://config.office.com).
5. Konfigurieren Sie die gewünschten Einstellungen für Ihre Office 365-Installation. Klicken Sie oben rechts auf der Seite auf **Senden**, wenn Sie mit der Konfiguration fertig sind. 
6. Auf der Seite **Bereitstellung** müssen Sie sich entscheiden, ob Sie die Bereitstellung jetzt oder zu einem späteren Zeitpunkt durchführen möchten. Wenn Sie die Bereitstellung später durchführen möchten, finden Sie die Anwendung unter **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  
7. Bestätigen Sie die Einstellungen auf der Seite **Zusammenfassung**. 
8. Klicken Sie auf **Weiter**, und klicken Sie anschließend auf **Schließen**, sobald der Office 365-Installations-Assistent abgeschlossen wurde. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Bereitstellen von Office 365-Apps mithilfe von Configuration Manager Version 1802 oder früher:

1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung**.
2. Klicken Sie im oberen rechten Bereich auf **Office 365-Installer**. Der Office 365-Installations-Assistent wird geöffnet.
3. Geben Sie auf der Seite **Anwendungseinstellungen** einen Namen und eine Beschreibung für die App an, geben Sie den Downloadpfad für die Dateien ein, und klicken Sie anschließend auf **Weiter**. Der Speicherort muss in Form von &#92;&#92;*Server*&#92;*Freigabe* angegeben werden.
4. Legen Sie auf der Seite **Clienteinstellungen importieren** fest, ob Sie die Office 365-Clienteinstellungen aus einer vorhandenen XML-Konfigurationsdatei importieren oder die Einstellungen manuell angeben möchten. Klicken Sie auf **Weiter**, wenn Sie fertig sind.  

    Wenn Sie über eine vorhandene Konfigurationsdatei verfügen, geben Sie den Speicherort für die Datei an, und fahren Sie mit Schritt 7 fort. Der Speicherort muss im folgenden Format angegeben werden: &#92;&#92;*Server*&#92;*Freigabe*&#92;*Dateiname*.XML.
    > [!IMPORTANT]    
    > Die XML-Konfigurationsdatei darf nur [vom Office 365 ProPlus-Client unterstützte Sprachen](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016) enthalten.

5. Wählen Sie auf der Seite **Client Products** (Clientprodukte) die von Ihnen verwendete Office 365-Suite aus. Wählen Sie die Anwendungen aus, die Sie hinzufügen möchten. Wählen Sie sämtliche zusätzlichen Office-Produkte aus, die hinzugefügt werden sollen, und klicken Sie dann auf **Weiter**.
6. Wählen Sie auf der Seite **Clienteinstellungen** die einzuschließenden Einstellungen aus, und klicken Sie anschließend auf **Weiter**.
7. Wählen Sie auf der Seite **Bereitstellung** aus, ob die Anwendung bereitgestellt werden soll, und klicken Sie anschließend auf **Weiter**. <br/>Wenn Sie auswählen, das Paket nicht im Assistenten bereitzustellen, fahren Sie mit Schritt 9 fort.
8. Konfigurieren Sie die restlichen Seiten des Assistenten, wie Sie dies bei einer normalen Anwendungsbereitstellung tun würden. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen einer Anwendung](../../apps/get-started/create-and-deploy-an-application.md).
9. Schließen Sie den Assistenten ab.
10. Sie können die Anwendung von **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Anwendungen** aus bereitstellen oder bearbeiten.    

Nachdem Sie Office 365-Anwendungen mithilfe des Office 365-Installers erstellt und bereitgestellt haben, werden die Office-Updates von Configuration Manager nicht standardmäßig verwaltet. Damit Office 365-Clients Updates von Configuration Manager erhalten können, lesen Sie [Bereitstellen von Office 365-Updates mit Configuration Manager](#deploy-office-365-updates).

Nach der Bereitstellung von Office 365-Apps können Sie Regeln zur automatischen Bereitstellung erstellen, um die Apps zu verwalten. Um eine Regel zur automatischen Bereitstellung (Automatic Deployment Rule, ADR) für Office 365-Apps zu erstellen, klicken Sie im [Office 365-Clientverwaltungsdashboard](office-365-dashboard.md) auf **ADR erstellen**. Wählen Sie bei der Produktauswahl **Office 365 Client** aus. Weitere Informationen finden Sie unter [Automatically deploy software updates (Automatisches Bereitstellen von Softwareupdates)](automatically-deploy-software-updates.md).


## <a name="drill-through-required-office-365-updates"></a>Ausführen eines Drillthrough durch erforderliche Office 365-Updates
<!--4224414-->
*(Eingeführt in Version 1906)*

Sie können einen Drillthrough durch die Konformitätsstatistiken durchführen, um herauszufinden, auf welchen Geräten ein bestimmtes Softwareupdate für Office 365 erforderlich ist. Sie benötigen zum Abrufen der Geräteliste die Berechtigung, Updates und die jeweiligen Sammlungen abzurufen, zu denen die Geräte gehören. Gehen Sie wie folgt vor, um einen Drilldown in der Geräteliste auszuführen:

1. Wechseln Sie zu **Softwarebibliothek** > **Office 365-Clientverwaltung** > **Office 365-Updates**.
1. Wählen Sie ein beliebiges Update aus, das für mindestens ein Gerät erforderlich ist.
1. Öffnen Sie die Registerkarte **Zusammenfassung**, und sehen Sie sich das Kreisdiagramm unter **Statistiken** an.
1. Klicken Sie auf der rechten Seite neben dem Kreisdiagramm auf den Link **Erforderliche anzeigen**, um einen Drilldown für die Geräteliste auszuführen.
1. Über diese Aktion gelangen Sie unter **Geräte** zu einem temporären Knoten, unter dem die Geräte angezeigt werden, für die das Update erforderlich ist. Außerdem können Sie Aktionen für den Knoten ausführen, z. B. können Sie eine neue Sammlung aus der Liste erstellen.


## <a name="deploy-office-365-updates"></a>Bereitstellen von Updates für Office 365

Befolgen Sie die folgenden Schritte, um Office 365-Updates mit Configuration Manager bereitzustellen:

1. [Überprüfen Sie die Anforderungen](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) für die Verwendung von Configuration Manager zum Verwalten von Office 365-Client-Updates im Abschnitt **Anforderungen für die Verwendung von Configuration Manager zum Verwalten von Office 365-Clientupdates** des verlinkten Artikels.  

2. [Konfigurieren Sie Softwareupdatepunkte](../get-started/configure-classifications-and-products.md), um die Office 365-Clientupdates zu synchronisieren. Legen Sie als Klassifizierung **Updates** fest, und wählen Sie **Office 365-Client** als Produkt aus. Synchronisieren Sie Softwareupdates nach dem Konfigurieren von Softwareupdatepunkten, um die Klassifizierung **Updates** zu verwenden.
3. Aktivieren Sie die Office 365-Clients, damit sie Updates von Configuration Manager erhalten können. Sie können den Client mithilfe von Configuration Manager-Clienteinstellungen oder Gruppenrichtlinien aktivieren.

    **Methode 1:** Ab der Version 1606 von Configuration Manager können Sie die Configuration Manager-Clienteinstellung zum Verwalten des Office 365-Client-Agents nutzen. Nachdem Sie diese Einstellung konfiguriert und Updates für Office 365 bereitgestellt haben, kommuniziert der Configuration Manager-Client-Agent mit dem Office 365-Client-Agent, um die Updates von einem Verteilungspunkt herunterzuladen und zu installieren. Configuration Manager macht eine Bestandsaufnahme der Office 365 ProPlus-Clienteinstellungen.    

      1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Übersicht** > **Clienteinstellungen**.  

      2. Öffnen Sie die entsprechenden Geräteeinstellungen zum Aktivieren des Client-Agents. Weitere Informationen zum Konfigurieren von Standard- und benutzerdefinierten Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).  

      3. Klicken Sie auf **Softwareupdates** und wählen Sie **Ja** für die Einstellung **Verwaltung des Office 365-Client-Agents aktivieren** aus.  

    **Methode 2:**  [Aktivieren Sie die Office 365-Clients, um Updates von Configuration Manager zu erhalten](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient), indem Sie das Office-Bereitstellungstool oder die Gruppenrichtlinie verwenden.  

4. [Stellen Sie für Clients Office 365-Updates bereit](deploy-software-updates.md).

> [!Important]
> - Ab Configuration Manager-Version 1706 wurden Office 365-Clientupdates auf den Knoten **Office 365-Clientverwaltung** >**Office 365-Updates** verschoben. Diese Aktion hat keine Auswirkungen auf die aktuelle ADR-Konfiguration. 
> - Vor der Configuration Manager-Version 1610 müssen Sie Updates in der gleichen Sprache herunterladen und bereitstellen, in der die Office 365-Clients konfiguriert sind. Nehmen wir z.B. an, Sie haben einen Office 365-Client, der mit den Sprachen en-US und de-DE konfiguriert ist. Auf dem Standortserver laden Sie nur den en-US-Inhalt für ein zutreffendes Office 365-Update herunter und stellen ihn bereit. Wenn der Benutzer die Installation für dieses Updates aus dem Softwarecenter startet, hängt das Update beim Herunterladen des Inhalts für „de-de“. 

> [!NOTE]  
>
> Wenn Office 365 ProPlus vor kurzem installiert wurde, ist es je nach Installationsmethode möglich, dass der Updatekanal noch nicht festgelegt wurde. In diesem Fall werden die bereitgestellten Updates als nicht anwendbar erkannt. Bei der Installation von Office 365 ProPlus wird ein [Task für geplante, automatische Updates](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) erstellt. In diesem Fall muss der Task mindestens einmal ausgeführt werden, damit der Updatekanal festgelegt wird und die Updates als anwendbar ermittelt werden.
>
> Wenn Office 365 ProPlus vor kurzem installiert wurde und Updates nicht erkannt werden, können Sie den Task für automatische Office-Updates für Testzwecke manuell starten, und starten Sie dann den [Auswertungszyklus für Softwareupdatebereitstellung](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) auf dem Client. Anweisungen dazu, wie Sie dies in einer Tasksequenz durchführen, finden Sie unter [Aktualisieren von Office 365 ProPlus in einer Tasksequenz](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence).

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Verhalten bei Neustart und Client-Benachrichtigungen für Office 365-Updates
Wenn Sie ein Update für einen Office 365-Client bereitstellen, unterscheiden sich das Verhalten beim Neustart und die Clientbenachrichtigungen je nach verwendeter Version von Configuration Manager. In der folgenden Tabelle finden Sie Informationen dazu, welche Aktionen beim Endnutzer erfolgen, wenn der Client ein Update für Office 365 empfängt:

|Configuration Manager-Version |Ablauf für Endbenutzer|  
|----------------|---------------------|
|1706, 1710|Der Client empfängt Popup- und In-App-Benachrichtigungen. Vor der Installation des Updates wird außerdem ein Countdown-Dialog angezeigt.|
|1802| Der Client empfängt Popup- und In-App-Benachrichtigungen. Vor der Installation des Updates wird außerdem ein Countdown-Dialog angezeigt. </br>Wenn Office 365-Anwendungen während eines erzwungenen Updates von Office 365-Clients ausgeführt werden, werden Office-Anwendungen nicht zum Schließen gezwungen. Stattdessen wird zu einem späteren Zeitpunkt angezeigt, dass für die Updateinstallation ein Systemneustart erforderlich ist. <!--510006-->|


> [!Important]
>
>Beachten Sie in der Configuration Manager-Version 1706 die folgenden Details:
>
>- Ein Benachrichtigungssymbol wird im Infobereich in der Taskleiste für erforderliche Anwendungen angezeigt, wenn die Frist innerhalb von 48 Stunden in der Zukunft liegt und der Inhalt des Updates heruntergeladen wurde. 
>- Ein Countdown-Dialogfeld wird für benötigte Apps angezeigt, bei denen die Frist innerhalb von 7,5 Stunden in der Zukunft liegt und das Update heruntergeladen wurde. Der Benutzer kann den Countdown-Dialog vor Ablauf der Frist maximal dreimal zurückstellen. Bei einer Zurückstellung wird der Countdown nach zwei Stunden wieder angezeigt. Wenn keine Zurückstellung erfolgt, gibt es einen 30-minütigen Countdown, und das Update wird installiert, wenn der Countdown abläuft.
>- Eine Popupbenachrichtigung wird möglicherweise erst angezeigt, nachdem der Benutzer auf das Symbol im Infobereich geklickt hat. Wenn darüber hinaus im Infobereich nur wenig Platz zur Verfügung steht, ist das Benachrichtigungssymbol möglicherweise nicht sichtbar, es sei denn, der Benutzer öffnet oder erweitert den Infobereich. 
>- Das Dialogfeld für die Benachrichtigung und den Countdown wird möglicherweise geöffnet, während der Benutzer nicht aktiv sein Gerät bedient. Wenn das Gerät beispielsweise über Nacht gesperrt ist, wird die Schließung ausgeführter Office-Apps möglicherweise erzwungen, damit das Update installiert werden kann. Vor dem Schließen der App speichert Office App-Daten, um Datenverlust zu vermeiden. 
>- Wenn die Frist in der Vergangenheit liegt oder so konfiguriert ist, dass sie so schnell wie möglich beginnt, können ausgeführte Office-Anwendungen gezwungen sein, ohne Benachrichtigung geschlossen zu werden. 
>- Wenn der Benutzer ein Office-Update vor Ablauf der Frist installiert, überprüft Configuration Manager, ob das Update nach Ablauf der Frist installiert wird. Wenn das Update nicht auf dem Gerät erkannt wird, wird das Update installiert. 
>- Die In-App-Benachrichtigungsleiste wird in einer Office-Anwendung, die vor dem Herunterladen des Updates ausgeführt wird, nicht angezeigt. Nach dem Herunterladen des Updates wird die In-App-Benachrichtigung nur für neu geöffnete Anwendungen angezeigt.
>- Bei Office-Updates, die im Rahmen eines Wartungsfensters oder außerhalb der Geschäftszeiten ausgelöst werden, kann es vorkommen, dass ausgeführte Office-Anwendungen zum Schließen gezwungen werden, um das Update ohne Benachrichtigungen zu installieren. 
>- Weitere Informationen finden Sie unter [End-user update notifications for Office 365 (Updatebenachrichtigungen für Office 365-Endbenutzer)](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus).


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a> Hinzufügen von Sprachen für Downloads des Office 365-Updates
Sie können Configuration Manager so einrichten, dass das Herunterladen von Updates für alle von Office 365 unterstützen Sprachen unterstützt wird.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Herunterladen von Updates für zusätzliche Sprachen in Version 1902
<!--3555955-->

Ab der Configuration Manager-Version 1902 trennt der Updateworkflow die 38 Sprachen für **Windows Update** von den zahlreichen zusätzlichen Sprachen für das **Office 365-Clientupdate**.

Um die benötigten Sprachen auszuwählen, verwenden Sie die Seite **Sprachauswahl** an den folgenden Stellen:
- Assistent zum Erstellen automatischer Bereitstellungsregeln
- Assistent zum Bereitstellen von Softwareupdates
- Assistent zum Herunterladen von Softwareupdates
- Eigenschaften der automatischen Bereitstellungsregel

Wählen Sie auf der Seite **Sprachauswahl** die Option **Office 365-Clientupdate** aus, und klicken Sie auf **Bearbeiten**. Fügen Sie die benötigten Sprachen für Office 365 hinzu, und klicken Sie auf **OK**.

![Screenshot zum Hinzufügen von zusätzlichen Sprachen für Office 365](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>So fügen Sie Unterstützung für das Herunterladen von Updates für zusätzliche Sprachen in Version 1810 und früher hinzu

Gehen Sie am Softwareupdatepunkt des Standorts der zentralen Verwaltung oder an einem eigenständigen primären Standort folgendermaßen vor.

> [!IMPORTANT]  
> Das Konfigurieren zusätzlicher Sprachen für das Office 365-Update ist eine standortweite Einstellung. Nachdem Sie die Sprachen mithilfe des folgenden Verfahrens hinzugefügt haben, werden alle Office 365-Updates in diesen Sprachen sowie in den Sprachen heruntergeladen, die Sie auf der Seite **Sprachauswahl** in den Assistenten „Softwareupdates herunterladen“ oder „Softwareupdates bereitstellen“ auswählen.

1. Geben Sie an der Eingabeaufforderung als Administrator den Befehl *wbemtest* ein, um das Testprogramm für die Windows-Verwaltungsinstrumentation zu öffnen.
2. Klicken Sie auf **Verbinden**, und geben Sie dann *root\sms\site_&lt;siteCode&gt;* ein.
3. Klicken Sie auf **Abfrage**, und führen Sie dann die folgende Abfrage aus: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI-Abfrage](../media/1-wmiquery.png)
4. Doppelklicken Sie im Ergebnisbereich auf das Objekt mit dem Standortcode für den Standort der zentralen Verwaltung oder für den eigenständigen primären Standort.
5. Wählen Sie die **Props**-Eigenschaft, klicken Sie auf **Eigenschaft bearbeiten**, und klicken Sie dann auf **Eingebettet**.
   ![Eigenschaften-Editor](../media/2-propeditor.png)
6. Beginnen Sie beim ersten Abfrageergebnis, und öffnen Sie jedes Objekt, bis Sie das Objekt finden, dessen **PropertyName**-Eigenschaft **AdditionalUpdateLanguagesForO365** lautet.
7. Wählen Sie **Value2**, und klicken Sie auf **Eigenschaft bearbeiten**.  
   ![Value2-Eigenschaft bearbeiten](../media/3-queryresult.png)
8. Fügen Sie **Value2**-Eigenschaft zusätzliche Sprachen hinzu, und klicken Sie auf **Eigenschaft speichern**. <br/> Beispiel: pt-pt (Portugiesisch – Portugal) af-za (für Afrikaans – Südafrika), nn-no (für Norwegisch [Nynorsk] – Norwegen) usw. Für die Beispielsprachen geben Sie `pt-pt,af-za,nn-no` ein. Verwenden Sie keine Leerzeichen zwischen den Sprachen.
 
   ![Sprachen im Eigenschaften-Editor hinzufügen](../media/4-props.png)  
9. Klicken Sie auf **Schließen** > **Schließen** > **Eigenschaft speichern** > **Objekt speichern** (wenn Sie hier auf **Schließen** klicken, werden die Werte verworfen). Klicken Sie zuerst auf **Schließen** und anschließend auf **Beenden**, um das Testprogramm für die Windows-Verwaltungsinstrumentation zu beenden.
10. Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung** > **Office 365-Updates**.
11. Beim Herunterladen von Updates für Office 365 werden die Updates jetzt in der Sprache heruntergeladen, die Sie im Assistenten auswählen und in diesem Verfahren konfiguriert haben. Um zu überprüfen, ob die Updates in den richtigen Sprachen heruntergeladen wurden, wechseln Sie zur Paketquelle für das Update, und suchen Sie nach Dateien mit dem Sprachcode im Dateinamen.  
    ![Dateinamen mit zusätzlichen Sprachen](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>Aktualisieren von Office 365 ProPlus in einer Tasksequenz
Bei der Verwendung des Tasksequenzschritts [Softwareupdates installieren](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) zum Installieren von Office 365-Updates, ist es möglich, dass bereitgestellte Updates als nicht anwendbar erkannt werden.  Dies kann auftreten, wenn der Task für geplante, automatische Updates nicht mindestens einmal ausgeführt wurde (siehe Hinweis unter [Bereitstellen von Updates für Office 365](manage-office-365-proplus-updates.md#deploy-office-365-updates)). Dies kann beispielsweise vorkommen, wenn Office 365 ProPlus unmittelbar vor der Ausführung dieses Schritts installiert wurde.

Verwenden Sie eine der folgenden Methoden, um sicherzustellen, dass der Updatekanal so festgelegt ist, dass bereitgestellte Updates ordnungsgemäß erkannt werden:

**Methode 1:**
1. Öffnen Sie den Taskplaner (taskschd.msc) auf einem Computer mit der gleichen Version von Office 365 ProPlus, und identifizieren Sie den Task für das automatische Office 365-Update. In der Regel befindet sie sich unter **Aufgabenplanungsbibliothek** >**Microsoft**>**Office**.
2. Klicken Sie mit der rechten Maustaste auf die automatischen Updates, und wählen Sie **Eigenschaften** aus.
3. Wechseln Sie zur Registerkarte **Aktionen**, und klicken Sie auf **Bearbeiten**. Kopieren Sie den Befehl und alle Argumente. 
4. Bearbeiten Sie Ihre Tasksequenzen in der Configuration Manager-Konsole.
5. Fügen Sie einen neuen Schritt **Befehlszeile ausführen** vor dem Schritt **Softwareupdates installieren** in der Tasksequenz hinzu. Wenn Office 365 ProPlus als Teil derselben Tasksequenz installiert wird, stellen Sie sicher, dass dieser Schritt nach der Installation ausgeführt wird.
6. Kopieren Sie den Befehl und die Argumente, die Sie aus der geplanten Aufgabe für automatische Office-Updates gesammelt haben. 
7. Klicken Sie auf **OK**. 

**Methode 2:**
1. Öffnen Sie den Taskplaner (taskschd.msc) auf einem Computer mit der gleichen Version von Office 365 ProPlus, und identifizieren Sie den Task für das automatische Office 365-Update. In der Regel befindet sie sich unter **Aufgabenplanungsbibliothek** >**Microsoft**>**Office**.
2. Bearbeiten Sie Ihre Tasksequenzen in der Configuration Manager-Konsole.
3. Fügen Sie einen neuen Schritt **Befehlszeile ausführen** vor dem Schritt **Softwareupdates installieren** in der Tasksequenz hinzu. Wenn Office 365 ProPlus als Teil derselben Tasksequenz installiert wird, stellen Sie sicher, dass dieser Schritt nach der Installation ausgeführt wird.
4. Geben Sie die Befehlszeile in das Befehlszeilenfeld ein, mit dem der geplante Task ausgeführt wird. Stellen Sie sicher, dass die Zeichenfolge in Anführungszeichen wie im folgenden Beispiel dem in Schritt 1 identifizierten Pfad und Namen entspricht.  

    Beispiel: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Klicken Sie auf **OK**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a><a name="bkmk_channel"></a> Ändern des Updatekanals nach dem Aktivieren des Erhalts von Updates für Office 365-Clients über Configuration Manager

Nach der Bereitstellung von Office 365 ProPlus können Sie den Updatekanal per Gruppenrichtlinie oder mit dem Office-Bereitstellungstool (ODT) ändern. Beispielsweise können Sie ein Gerät aus „Halbjährlicher Kanal“ in „Halbjährlicher Kanal (gezielt)“ verschieben. Beim Wechseln des Kanals wird Office automatisch aktualisiert, ohne dass die Vollversion neu installiert oder heruntergeladen werden muss. Weitere Informationen finden Sie unter [Ändern des Office 365 ProPlus-Updatekanals für Geräte in Ihrer Organisation](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Nächste Schritte

Über das Office 365-Clientverwaltungsdashboard in Configuration Manager können Sie Office 365-Clientinformationen überprüfen und Office 365-Apps bereitstellen. Weitere Informationen finden Sie unter [Office 365-Clientverwaltungsdashboard](office-365-dashboard.md).
