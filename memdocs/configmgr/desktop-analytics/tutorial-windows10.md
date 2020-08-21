---
title: Tutorial – Bereitstellen von Windows 10
titleSuffix: Configuration Manager
description: In diesem Tutorial wird das Bereitstellen von Windows 10 mithilfe von Desktop Analytics und Configuration Manager in einer Pilotgruppe behandelt.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: fc4309d3d09cd35c17b23bc46dcb1a28d210aa8e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125745"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutorial: Bereitstellen von Windows 10 für den Pilotversuch

In diesem Tutorial wird Windows 10 mithilfe von Desktop Analytics und Configuration Manager in einer Pilotgruppe bereitgestellt. Dabei wird die Integration des Clouddiensts veranschaulicht, um Erkenntnisse zum Bereitstellen von Windows mit dem lokalen Produkt zu vermitteln. Bestimmen Sie mit Desktop Analytics die Geräte, die sich am besten für die Einbindung in eine Pilotgruppe eignen. Verwenden Sie dann Configuration Manager, um auf den aktuellen Stand in Bezug auf Windows zu gelangen.

In diesem Tutorial wird Folgendes vermittelt:  

> [!div class="checklist"]  
> * Einrichten von Desktop Analytics im Azure-Portal  
> * Herstellen der Verbindung mit Configuration Manager und Konfigurieren von Geräteeinstellungen  
> * Erstellen eines Bereitstellungsplans in Desktop Analytics für Windows 10  
> * Bereitstellen von Windows 10 in der Pilotgruppe mit Configuration Manager  

Wenn Sie über kein Azure-Abonnement verfügen, erstellen Sie zuerst ein [kostenloses Konto](https://azure.microsoft.com/free). Bei ordnungsgemäßer Konfiguration entstehen bei der Verwendung von Desktop Analytics keinerlei auf Azure bezogene Kosten.

Desktop Analytics verwendet einen *Log Analytics-Arbeitsbereich* in Ihrem Azure-Abonnement. Ein Arbeitsbereich ist im Wesentlichen ein Container, der Kontoinformationen und einfache Konfigurationsinformationen für das Konto enthält. Weitere Informationen finden Sie unter [Verwalten von Arbeitsbereichen](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie dieses Tutorial durcharbeiten, vergewissern Sie sich, dass die folgenden Voraussetzungen erfüllt sind:  

- Ein aktives Azure-Abonnement mit Berechtigungen eines [**globalen Administrators**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)  

    Weitere Informationen finden Sie unter [Desktop Analytics – Voraussetzungen](overview.md#prerequisites).

- Configuration Manager, Version 1902 mit Updaterollup (4500571) oder höher, mit der Rolle **Hauptadministrator**  

- Installationsmedium für die aktuelle Version von Windows 10

- Mindestens ein Windows 10-Gerät mit den folgenden Konfigurationen:  

    - Windows 10, Version 1709 oder höher, jedoch älter als die Version des verwendeten Installationsmediums

    - Das aktuelle kumulative Windows 10-Qualitätsupdate  

    - Konfigurations-Manager-Client, Version 1902 mit Updaterollup (4500571) oder höher  

- Unternehmensgenehmigung, die Windows-Diagnosedatenebene auf den Pilotgeräten auf **Optional (begrenzt)** festzulegen  

    Weitere Informationen finden Sie unter [Desktop Analytics – Datenschutz](privacy.md).

- Netzwerkkonnektivität zwischen dem Gerät und den folgenden Internetendpunkten:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (nur für die Configuration Manager-Serverrolle)
    - `https://*.manage.microsoft.com` (nur für die Configuration Manager-Serverrolle)

    Weitere Informationen finden Sie unter [Aktivieren der Datenfreigabe für Desktop Analytics](enable-data-sharing.md#endpoints).  

> [!Important]  
> Diese Voraussetzungen müssen für die Zwecke dieses Tutorials erfüllt sein. Weitere Informationen zu den allgemeinen Voraussetzungen für Desktop Analytics mit Configuration Manager finden Sie unter [Voraussetzungen](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Einrichten von Desktop Analytics

Melden Sie sich mit diesem Verfahren bei Desktop Analytics an, und konfigurieren Sie den Dienst in Ihrem Abonnement. Dieses Verfahren muss einmalig ausgeführt werden, um Desktop Analytics für Ihre Organisation einzurichten.  

1. Öffnen Sie das [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) in der Microsoft 365-Geräteverwaltung als Benutzer mit **globalen Administratorberechtigungen**. Wählen Sie **Starten** aus.  

2. Lesen Sie auf der Seite **Servicevertrag annehmen** den Servicevertrag durch, und wählen Sie **Annehmen** aus.  

3. Auf der Seite **Ihr Abonnement bestätigen** bezieht sich die Liste der qualifizierenden Lizenzen auf Windows-Geräteintegritätsfeatures von Desktop Analytics. Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.  

4. Auf der Seite **Benutzern Zugriff erteilen**:

    - **Desktop Analytics das Verwalten von Verzeichnisrollen in Ihrem Auftrag gestatten**: Desktop Analytics weist **Workspace-Besitzern** automatisch die Rolle **Desktop Analytics-Administrator** zu. Wenn diese Gruppen bereits über **globale Administratorberechtigungen** verfügen, wird keine Änderung vorgenommen.  

        Wenn Sie diese Option nicht auswählen, fügt Desktop Analytics dennoch Benutzer als Mitglieder der Sicherheitsgruppe hinzu. Ein **globaler Administrator** muss für die Benutzer die Rolle **Desktop Analytics-Administrator** manuell zuweisen.  

        Weitere Informationen zum Zuweisen von Berechtigungen der Administratorrolle in Azure Active Directory und den **Desktop Analytics-Administratoren** zugewiesenen Berechtigungen finden Sie unter [Berechtigungen der Administratorrolle in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics konfiguriert die Sicherheitsgruppe **Arbeitsbereichsbesitzer** in Azure Active Directory vorab für das Erstellen und Verwalten von Arbeitsbereichen und Bereitstellungsplänen. 

        Wenn Sie der Gruppe einen Benutzer hinzufügen möchten, geben Sie seinen Namen oder seine E-Mail-Adresse im Bereich **Namen oder E-Mail-Adresse eingeben** ein. Wählen Sie anschließend **Weiter** aus.

5. Auf der Seite **Ihren Arbeitsbereich einrichten**:  

    > [!Note]  
    > Zum Abschließen dieses Schritts benötigt der Benutzer Berechtigungen des **Arbeitsbereichsbesitzers** und zusätzlichen Zugriff auf das Azure-Abonnement und die Ressourcengruppe. Weitere Informationen finden Sie unter [Voraussetzungen](overview.md#prerequisites).  

    - Wählen Sie Ihr Azure-Abonnement aus.  

    - Wenn Sie einen vorhandenen Arbeitsbereich für Desktop Analytics verwenden möchten, wählen Sie ihn aus, und fahren Sie mit dem nächsten Schritt fort.  

    - Wählen Sie zum Erstellen eines Arbeitsbereichs für Desktop Analytics die Option **Arbeitsbereich hinzufügen** aus.  

        1. Geben Sie einen **Arbeitsbereichsnamen** ein.  

        2. Wählen Sie die Dropdownliste **Das Azure-Abonnement für diesen Arbeitsbereich auswählen** aus, und wählen Sie das Azure-Abonnement für den Arbeitsbereich aus.  

        3. Wählen Sie für die Ressourcengruppe **Neu erstellen** oder **Vorhandene verwenden** aus.  

        4. Wählen Sie in der Liste die **Region** aus, und wählen Sie anschließend **Hinzufügen** aus.  

6. Wählen Sie einen neuen oder vorhandenen Arbeitsbereich aus, und wählen Sie dann die Option **Als Desktop Analytics-Arbeitsbereich einrichten** aus.  Wählen Sie im Dialogfeld **Zugriff bestätigen und erteilen** die Option **Weiter** aus.  

7. Wählen Sie auf der neuen Browserregisterkarte ein Konto für die Anmeldung aus. Wählen Sie die Option **Zustimmung im Namen Ihrer Organisation** und anschließend **Zustimmen** aus.  


    > [!Note]  
    > Mit dieser Zustimmung wird der Anwendung MALogAnalyticsReader die Rolle „Log Analytics-Leser“ für den Arbeitsbereich zugewiesen. Diese Anwendungsrolle ist für Desktop Analytics erforderlich. Weitere Informationen erhalten Sie unter [Anwendungsrolle MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Wählen Sie auf der Seite **Ihren Arbeitsbereich einrichten** die Option **Weiter** aus.  

9. Wählen Sie auf der Seite **Letzte Schritte** die Option **Zu Desktop Analytics wechseln** aus. Im Azure-Portal wird die **Startseite** von Desktop Analytics angezeigt.  



## <a name="connect-configuration-manager"></a>Herstellen einer Verbindung mit Configuration Manager

Führen Sie dieses Verfahren aus, um Configuration Manager zu aktualisieren, eine Verbindung mit Desktop Analytics herzustellen und Geräteeinstellungen zu konfigurieren. Dieses Verfahren ist ein einmaliger Prozess, in dem Ihre Hierarchie an den Clouddienst angefügt wird.  

### <a name="update-configuration-manager"></a>Configuration Manager aktualisieren

Installieren Sie das Updaterollup (4500571) von Configuration Manager, Version 1902, um die Integration mit Desktop Analytics zu unterstützen. Weitere Informationen zu diesem Update finden Sie unter [Updaterollup für den aktuellen Branch von Configuration Manager, Version 1902](https://support.microsoft.com/help/4500571).

1. Aktualisieren Sie den Standort mit dem Updaterollup für Version 1902. Weitere Informationen finden Sie unter [Installieren konsoleninterner Updates](../core/servers/manage/install-in-console-updates.md).  

2. Aktualisieren der Clients Um diesen Prozess zu vereinfachen, sollten Sie automatische Clientupgrades in Betracht ziehen. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Herstellen einer Verbindung mit dem Dienst

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus. Wählen Sie im Menüband **Azure-Dienste konfigurieren** aus.  

2. Konfigurieren Sie auf der Seite **Azure-Dienste** des Assistenten für Azure-Dienste die folgenden Einstellungen:  

    - Geben Sie einen **Namen** für das Objekt in Configuration Manager an.  

    - Geben Sie eine optionale **Beschreibung** an, anhand derer Sie den Dienst identifizieren können.  

    - Wählen Sie in der Liste der verfügbaren Dienste **Desktop Analytics** aus.  
  
   Wählen Sie **Weiter** aus.  

3. Wählen Sie auf der Seite **App** die geeignete **Azure-Umgebung** aus. Wählen Sie anschließend für die Web-App **Durchsuchen** aus.

4. Wählen Sie **Erstellen** aus, um auf einfache Weise eine Azure AD-App für die Desktop Analytics-Verbindung hinzuzufügen.

5. Konfigurieren Sie im Fenster **Serveranwendung erstellen** die folgenden Einstellungen:  

    - **Anwendungsname**: Ein Anzeigename für die App in Azure AD.

    - **URL für Startseite**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Der Standardwert beträgt `https://ConfigMgrService`.  

    - **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, mit dem der Konfigurations-Manager-Client Zugriff auf den Dienst anfordert. Der Standardwert beträgt `https://ConfigMgrService`.  

    - **Gültigkeitsdauer des geheimen Schlüssels:** Wählen Sie entweder **1 Jahr** oder **2 Jahre** aus der Dropdownliste aus. Ein Jahr ist der Standardwert.  

    Wählen Sie **Anmelden** aus. Nach einer erfolgreichen Authentifizierung in Azure, wird zu Referenzzwecken der **Name des Azure AD-Mandanten** auf der Seite angezeigt.

    > [!Note]  
    > Führen Sie diesen Schritt als **globaler Administrator** aus. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird.  

    Klicken Sie auf **OK**, um die Web-App in Azure AD zu erstellen und das Dialogfeld „Serveranwendung erstellen“ zu schließen. Wählen Sie im Dialogfeld „Server-App“ **OK** aus. Wählen Sie anschließend auf der Seite „App“ des Assistenten für Azure-Dienste **Weiter** aus.  

6. Konfigurieren Sie auf der Seite **Diagnosedaten** die folgenden Einstellungen:  

    - **Kommerzielle ID**: Dieser Wert wird automatisch mit der ID Ihrer Organisation aufgefüllt.  

    - **Windows 10-Diagnosedatenebene**: Wählen Sie mindestens **Optional (begrenzt)** aus.  

    - **Gerätenamen in Diagnosedaten zulassen**: Wählen Sie **Aktivieren** aus.  
  
   Wählen Sie **Weiter** aus. Auf der Seite **Verfügbare Funktionalität** werden die Desktop Analytics-Funktionen angezeigt, die mit den Einstellungen für Diagnosedaten von der vorherigen Seite verfügbar sind. Wählen Sie **Weiter** aus.  

7. Konfigurieren Sie auf der Seite **Sammlungen** die folgenden Einstellungen:  

    - **Anzeigename:** Im Desktop Analytics-Portal wird die Configuration Manager-Verbindung mit diesem Namen angezeigt. Anhand dieses Namens können Sie zwischen verschiedenen Hierarchien unterscheiden. Beispiele sind *Testlabor* oder *Produktion*.  

    - **Zielsammlung**: Diese Sammlung enthält alle Geräte, die von Configuration Manager mit den Einstellungen für kommerzielle ID und Diagnosedaten konfiguriert werden. Dabei handelt es sich um sämtliche Geräte, die Configuration Manager mit dem Desktop Analytics-Dienst verbindet.  

    - **Geräte in der Zielsammlung verwenden einen vom Benutzer authentifizierten Proxy für die ausgehende Kommunikation**: In der Standardeinstellung ist dieser Wert **Nein**. Sollte Ihre Umgebung etwas anderes erfordern, legen Sie ihn auf **Ja** fest.  

    - **Wählen Sie bestimmte Sammlungen zur Synchronisierung mit Desktop Analytics aus**: Wählen Sie **Hinzufügen** aus, um zusätzliche Sammlungen einzuschließen. Diese Sammlungen können im Desktop Analytics-Portal mit Bereitstellungsplänen gruppiert werden. Sie müssen Pilotsammlungen und Pilotausschlusssammlungen einschließen.  

        Diese Sammlungen werden auch nach Ändern ihrer Mitgliedschaft weiterhin synchronisiert. Ihr Bereitstellungsplan verwendet beispielsweise eine Sammlung mit einer Windows 7-Mitgliedschaftsregel. Wird ein Upgrade dieser Geräte auf Windows 10 durchgeführt und Configuration Manager wertet die Sammlungsmitgliedschaft aus, werden diese Geräte aus der Sammlung und dem Bereitstellungsplan entfernt.  

8. Schließen Sie den Assistenten ab.  

Configuration Manager erstellt eine Richtlinie für Einstellungen, um Geräte in der Zielsammlung zu konfigurieren. Diese Richtlinie enthält die Einstellungen für Diagnosedaten, um Geräten das Senden von Daten an Microsoft zu ermöglichen. In der Standardeinstellung wird die Richtlinie von den Clients stündlich aktualisiert. Nach dem Empfang der neuen Einstellungen kann es einige Stunden dauern, bis die Daten in Desktop Analytics verfügbar sind.

> [!Note]  
> Weitere Informationen zu diesen Einstellungen finden Sie unter [Windows-Einstellungen](enroll-devices.md#windows-settings).  

Überwachen Sie die Konfiguration Ihrer Geräte für Desktop Analytics. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie den Knoten **Desktop Analytics-Wartung**, und wählen Sie das Dashboard **Verbindungsintegrität** aus.  

Configuration Manager synchronisiert Ihre Sammlungen innerhalb von 60 Minuten nach dem Erstellen der Verbindung. Navigieren Sie im Desktop Analytics-Portal zu **Weltweiter Pilot**, und zeigen Sie Ihre Configuration Manager-Gerätesammlungen an. Es kann zwei bis drei Tage dauern, bis der Rest des Portals die gesamten Daten anzeigt. Weitere Informationen finden Sie unter [Datenlatenz](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Erstellen eines Desktop Analytics-Bereitstellungsplans

Erstellen Sie anhand dieses Verfahrens einen Bereitstellungsplan in Desktop Analytics.

1. Öffnen Sie das [Desktop Analytics-Portal](https://aka.ms/desktopanalytics). Geben Sie Anmeldeinformationen ein, die mindestens über die Berechtigungen **Arbeitsbereichsmitwirkende** verfügen.  

2. Wählen Sie in der Gruppe „Verwalten“ die Option **Bereitstellungspläne** aus.  

3. Wählen Sie im Bereich **Bereitstellungspläne** die Option **Erstellen** aus.  

4. Konfigurieren Sie im Bereich **Bereitstellungsplan erstellen** die folgenden Einstellungen:  

    - **Name:** Ein eindeutiger Namen für den Bereitstellungsplan, z. B. `Windows 10 pilot`.  

    - **Produkte und Versionen**: Wählen Sie die bereitzustellende Windows 10-Version aus. Microsoft empfiehlt, Bereitstellungspläne zu erstellen, die die neueste Version verwenden.

    - **Gerätegruppen**: Wählen Sie auf der Registerkarte „Configuration Manager“ eine oder mehrere Gruppen aus, und wählen Sie anschließend **Als Zielgruppe festlegen** aus. Bei diesen Gruppen handelt es sich um Sammlungen, die von Configuration Manager synchronisiert werden.  

    - **Bereitschaftsregeln**: Anhand dieser Regeln können Sie bestimmen, welche Geräte sich für ein Upgrade qualifizieren. Klicken Sie auf **Windows-Betriebssystem**, und konfigurieren Sie die folgenden Einstellungen:  

        - **Meine Computer rufen Treiber automatisch von Windows Update ab**: Der Standardwert für diese Einstellung ist **Aus**; dieser Wert wird für das Bereitstellen mit Configuration Manager empfohlen.  

        - **Definieren Sie einen Schwellenwert für niedrige Anzahl von Installationen für Ihre Apps**: Der Standardwert für diese Einstellung ist `2%`. Apps unterhalb dieses Schwellenwerts werden automatisch auf *Niedrige Anzahl von Installationen* festgelegt. Diese Add-Ins werden von Desktop Analytics während des Pilotversuchs nicht überprüft.  

            Wenn eine App auf einem Prozentsatz der Computer installiert ist, der diesen Schwellenwert überschreitet, wird diese App vom Bereitstellungsplan als *Beachtenswert* markiert. Nun können Sie entscheiden, wie wichtig ihre Prüfung während der Pilotphase ist.  

    - **Abschlussdatum**: Wählen Sie das Datum aus, an dem Windows vollständig auf sämtlichen Zielgeräten bereitgestellt sein soll.  

5. Wählen Sie **Erstellen** aus. Der neue Plan wird während seiner Verarbeitung in der Liste der Bereitstellungspläne angezeigt. Fordern Sie die bedarfsgesteuerte Datenaktualisierung an, um die Verarbeitung zu beschleunigen. Weitere Informationen finden Sie unter [Desktop Analytics – Häufig gestellte Fragen](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Öffnen Sie den Bereitstellungsplan, indem Sie seinen Namen auswählen.  

7. Wählen Sie im Menü des Bereitstellungsplans in der Gruppe **Vorbereiten** die Option **Wichtigkeit angeben** aus.  

    1. Wählen Sie auf der Registerkarte **Apps** aus, dass nur Objekte vom Typ **Nicht überprüft** angezeigt werden sollen.  

    2. Wählen Sie die einzelnen Apps aus, und wählen Sie anschließend **Bearbeiten** aus. Sie können mehrere Apps gleichzeitig für die Bearbeitung auswählen.  

    3. Wählen Sie in der Liste **Wichtigkeit** eine Wichtigkeitsstufe aus. Wenn Desktop Analytics die App während des Pilotversuchs überprüfen soll, wählen Sie **Kritisch** oder **Wichtig** aus. Apps, die als **Nicht wichtig** markiert sind, werden nicht überprüft. Bewerten Sie beim Zuweisen von Wichtigkeitsstufen ihre [Kompatibilität](compat-assessment.md) und andere Planerkenntnisse.  

        Beim Zuweisen von Wichtigkeitsstufen können Sie auch die Upgradeentscheidung auswählen.  

    4. Klicken Sie abschließend auf **Speichern**.  

8. Wählen Sie im Menü des Bereitstellungsplans in der Gruppe **Vorbereiten** die Option **Piloten identifizieren** aus.  

    1. Überprüfen Sie die empfohlenen Geräte für den Pilotversuch.  

    2. Wählen Sie die einzelnen Geräte aus, und wählen Sie **Zu Pilot hinzufügen** aus. Wenn Sie mit der Empfehlung nicht einverstanden sind, wählen Sie **Ersetzen** aus.  

        Wenn Sie Informationen dazu wünschen, wie Desktop Analytics diese Empfehlungen abgibt, wählen Sie oben rechts im Bereich **Piloten identifizieren** das Informationssymbol aus.



## <a name="deploy-windows-10-in-configuration-manager"></a>Bereitstellen von Windows 10 in Configuration Manager

Stellen Sie anhand dieses Verfahrens Windows 10 in Configuration Manager in der Pilotgruppe bereit.

- [Erstellen Sie zunächst ein Betriebssystem-Upgradepaket für Windows 10](#bkmk_create-package) (sofern nicht bereits vorhanden)  

- [Erstellen Sie zunächst eine Betriebssystem-Upgrade-Tasksequenz für Windows 10](#bkmk_create-ts) (sofern nicht bereits vorhanden)  

- [Stellen Sie die Tasksequenz bereit](#bkmk_deploy-ts), wobei Sie den Desktop Analytics-Bereitstellungsplan verwenden  

- [Installieren Sie die Tasksequenz](#bkmk_install-ts) über das Softwarecenter auf einem Zielgerät  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> Erstellen eines Betriebssystem-Upgradepakets für Windows 10

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Betriebssystemaktualisierungspakete** aus.  

2. Klicken Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** auf **Aktualisierungspaket für Betriebssysteme hinzufügen**. Dadurch wird der Assistent zum Hinzufügen des Upgrades für Betriebssysteme gestartet.  

3. Geben Sie auf der Seite **Datenquelle** den **Netzwerkpfad** zu den Installationsquelldateien des Betriebssystem-Upgradepakets an. Beispiel: `\\server\share\path`.  

    > [!NOTE]  
    > Zu den Installationsquelldateien gehören „Setup.exe“ sowie andere Dateien und Ordner zum Installieren des Betriebssystems.  

4. Geben Sie auf der Seite **Allgemein** einen eindeutigen **Namen** für das Betriebssystem-Upgradepaket an.  

5. Führen Sie den Assistenten zum Hinzufügen des Upgradepakets für Betriebssysteme aus.  

#### <a name="distribute-content"></a>Verteilen von Inhalt

Verteilen Sie das Betriebssystemupgradepaket als Nächstes an die Verteilungspunkte.  

1. Wählen Sie das Betriebssystem-Upgradepaket in der Liste aus. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Bereitstellung** die Option **Inhalt verteilen** aus. Der Assistent für die Verteilung von Inhalt wird geöffnet.  

2. Überprüfen Sie auf der Seite **Allgemein**, ob es sich bei dem aufgeführten Inhalt um den Inhalt handelt, den Sie verteilen möchten. Wählen Sie dann **Weiter** aus.  

3. Wählen Sie auf der Seite **Inhaltsziel** die Option **Hinzufügen** und anschließend **Verteilungspunkt** aus. Wählen Sie einen vorhandenen Verteilungspunkt aus, und wählen Sie dann **OK** aus. Nachdem Sie alle gewünschten Inhaltsziele hinzugefügt haben, wählen Sie **Weiter** aus.  

4. Führen Sie den Assistenten für die Verteilung von Inhalt aus.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a> Erstellen einer Betriebssystem-Upgradetasksequenz für Windows 10

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz erstellen** aus.  

3. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** des Tasksequenzerstellungs-Assistenten **Ein Betriebssystem mithilfe eines Aktualisierungspakets aktualisieren** und dann **Weiter** aus.  

4. Geben Sie auf der Seite **Informationen zur Tasksequenz** einen **Namen der Tasksequenz** an, anhand dessen Sie die Tasksequenz identifizieren können.  

5. Geben Sie auf der Seite zum **Windows-Betriebssystem aktualisieren** die folgenden Einstellungen an, und wählen Sie dann **Weiter** aus:  

    - **Upgradepaket:** Geben Sie das Upgradepaket an, das die Quelldateien für das Upgrade des Betriebssystems enthält.  

    - **Editionsindex:** Wenn mehrere Editionsindizes für das Betriebssystem im Paket verfügbar sind, wählen Sie den gewünschten Editionsindex aus. Der Assistent wählt standardmäßig den ersten Index aus.  

    - **Product Key:** Geben Sie den Windows-Product Key für das zu installierende Betriebssystem an. Geben Sie codierte Volumenlizenzschlüssel oder Standard-Product Keys an. Wenn Sie einen Standard-Product Key verwenden, trennen Sie jede Gruppe von fünf Zeichen durch einen Bindestrich („-“). Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Wenn das Upgrade für eine Volumenlizenzedition vorgesehen ist, ist der Product Key möglicherweise nicht erforderlich.  

        > [!Note]  
        > Dieser Product Key kann ein Mehrfachaktivierungsschüssel oder ein generischer Volumenlizenzschlüssel sein. Ein generischer Volumenlizenzschlüssel wird auch als Clientsetupschlüssel für den Schlüsselverwaltungsdienst (KMS) bezeichnet. Weitere Informationen finden Sie unter [Planen der Volumenaktivierung](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Eine Liste der KMS-Clientsetupschlüssel finden Sie im Windows Server-Aktivierungshandbuch in [Anhang A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).

6. Wählen Sie auf der Seite **Updates einschließen** die Option **Weiter** aus, sodass keine Softwareupdates installiert werden.  

7. Wählen Sie auf der Seite **Anwendungen installieren** die Option **Weiter** aus, sodass keine Anwendungen installiert werden.

8. Führen Sie den Tasksequenzerstellungs-Assistenten aus.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> Bereitstellen der Tasksequenz mit dem Desktop Analytics-Bereitstellungsplan

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie den Knoten **Desktop Analytics-Wartung**, und wählen Sie den Knoten **Bereitstellungspläne** aus.  

2. Wählen Sie Ihren Bereitstellungsplan für den Windows 10-Pilotversuch aus, und wählen Sie anschließend im Menüband **Bereitstellungsplandetails** aus.  

3. Wählen Sie in der Kachel **Pilotstatus** in der Dropdownliste **Tasksequenz** aus, und wählen Sie anschließend **Bereitstellen** aus.  

4. Wählen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Allgemein** neben dem Feld **Software** die Option **Durchsuchen** aus. Wählen Sie die Tasksequenz für ein direktes Windows 10-Upgrade aus, und wählen Sie **Weiter** aus.  

    > [!Note]  
    > Bei Integration mit Desktop Analytics erstellt Configuration Manager automatisch Pilot- und Produktionssammlungen für den Bereitstellungsplan. Bevor Sie diese verwenden können, kann es eine Weile dauern, bis die Sammlungen synchronisiert wurden. Weitere Informationen finden Sie unter [Problembehandlung – Datenlatenz](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Diese Sammlung ist für Geräte im Desktop Analytics-Bereitstellungsplan reserviert. Diese Sammlung kann nicht manuell geändert werden.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Wählen Sie auf der Seite **Inhalt** die Option **Hinzufügen** und anschließend **Verteilungspunkt** aus. Wählen Sie einen verfügbaren Verteilungspunkt zum Hosten des Installationsinhalts aus, und wählen Sie **OK** aus. Klicken Sie dann auf **Weiter**.  

6. Wählen Sie auf der Seite **Bereitstellungseinstellungen** die Option **Weiter** aus, um die Standardeinstellungen zu übernehmen. (Eine verfügbare Installation.)  

7. Wählen Sie auf der Seite **Zeitplanung** die Option **Weiter** aus, um die Standardeinstellungen zu übernehmen. (Baldmöglichst verfügbar.)  

8. Wählen Sie auf der Seite **Benutzerfreundlichkeit** die Option **Weiter** aus, um die Standardeinstellungen zu übernehmen. (Anzeige im Softwarecenter, und es werden nur Benachrichtigungen zu Computerneustarts angezeigt.)  

9. Wählen Sie auf der Seite **Benachrichtigungen** die Option **Weiter** aus, um die Standardeinstellungen zu übernehmen.  

10. Schließen Sie den Assistenten ab.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> Installieren der Tasksequenz aus dem Softwarecenter

1. Melden Sie sich bei einem Gerät an, das Mitglied des Bereitstellungsplans für den Pilotversuch ist.  

2. Öffnen Sie das **Softwarecenter**, und installieren Sie das verfügbare Betriebssystem für Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit dem nächsten Artikel fort, um mehr über Desktop Analytics-Bereitstellungspläne zu erfahren.
> [!div class="nextstepaction"]  
> [Bereitstellungspläne](about-deployment-plans.md)
