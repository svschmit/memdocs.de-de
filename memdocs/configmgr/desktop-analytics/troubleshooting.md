---
title: Problembehandlung bei Desktop Analytics
titleSuffix: Configuration Manager
description: Dieser Artikel enthält technische Details zur Problembehandlung bei Desktop Analytics.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: cfd329b7edb695c1e7316323555bfc18a2fd479e
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428585"
---
# <a name="troubleshoot-desktop-analytics"></a>Problembehandlung bei Desktop Analytics

Anhand der Details in diesem Artikel können Sie Probleme mit der Desktop Analytics-Integration mit Configuration Manager beheben.

## <a name="confirm-prerequisites"></a>Voraussetzungen bestätigen

Viele gängige Probleme sind darauf zurückzuführen, dass Voraussetzungen nicht erfüllt sind. Bestätigen Sie zunächst die folgenden Konfigurationen:

- [Voraussetzungen](overview.md#prerequisites)  

- [Updates für Windows-Komponenten](enroll-devices.md#update-devices)  

- [Aktivieren der Datenfreigabe](enable-data-sharing.md); in diesem Artikel werden die folgenden Themen behandelt:  

  - Internetendpunkte, mit denen Clients eine Verbindung herstellen müssen  

  - Proxyserverauthentifizierung  

  - Diagnosedatenebenen  

## <a name="monitor-connection-health"></a>Überwachen der Verbindungsintegrität

Verwenden Sie das Dashboard **Verbindungsintegrität** in Configuration Manager, um die Geräteintegrität nach Kategorien aufzuschlüsseln. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie den Knoten **Desktop Analytics-Wartung**, und wählen Sie das Dashboard **Verbindungsintegrität** aus.  

Weitere Informationen finden Sie unter [Überwachen der Verbindungsintegrität](monitor-connection-health.md).

> [!NOTE]
> Die Configuration Manager-Verbindung mit Desktop Analytics basiert auf dem Dienstverbindungspunkt. Wenn Änderungen an dieser Standortsystemrolle vorgenommen werden, kann dies Auswirkungen auf die Synchronisierung mit dem Clouddienst haben. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

Seit Version 2002 gilt Folgendes: Wenn die Verbindung des Configuration Manager-Standorts mit den erforderlichen Endpunkten für einen Clouddienst nicht hergestellt werden kann, wird eine kritische Statusmeldung mit der ID 11488 ausgegeben. Wenn keine Verbindung mit dem Dienst hergestellt werden kann, wird der Status der Komponente „SMS_SERVICE_CONNECTOR“ in „kritisch“ geändert. Zeigen Sie detaillierte Statusinformationen im Knoten [Komponentenstatus](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) in der Configuration Manager-Konsole an.<!-- 5566763 -->

## <a name="log-files"></a>Protokolldateien

Weitere Informationen finden Sie unter [Protokolldateien für Desktop Analytics](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

Ab Configuration Manager, Version 1906, können Sie das Tool **DesktopAnalyticsLogsCollector.ps1** aus dem Installationsverzeichnis von Configuration Manager zum Behandeln von Problemen in Desktop Analytics verwenden. Es führt einige grundlegende Schritte zur Problembehandlung aus und sammelt die relevanten Protokolle in einem einzelnen Arbeitsverzeichnis. Weitere Informationen finden Sie unter [Protokollsammler](log-collector.md).

### <a name="enable-verbose-logging"></a>Ausführliche Protokollierung aktivieren

1. Wechseln Sie auf dem Dienstverbindungspunkt zum folgenden Registrierungsschlüssel: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Legen Sie den Wert für **LoggingLevel** auf `0` fest.  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a> Azure AD-Anwendungen

Desktop Analytics fügt Ihrer Azure AD-Instanz die folgenden Anwendungen hinzu:

- **Configuration Manager-Microservice**: Stellt eine Verbindung von Configuration Manager mit Desktop Analytics her. Für diese App gelten keine Zugriffsanforderungen.  

- **MALogAnalyticsReader**: Diese Anwendung überwacht Ihren Azure Log Analytics-Arbeitsbereich, um sicherzustellen, dass die tägliche Momentaufnahme erfolgreich kopiert wurde. Weitere Informationen erhalten Sie unter [Anwendungsrolle MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- **Desktop Analytics**: Diese Anwendung ermöglicht Configuration Manager das Abrufen der Bereitstellungsplaninformationen und des Status der Gerätebereitschaft von Desktop Analytics.

Wenn Sie diese Apps nach Abschluss des Setups bereitstellen müssen, wechseln Sie zum Bereich **Verbundene Dienste**. Wählen Sie **Benutzer- und Apps-Zugriff konfigurieren** aus, und stellen Sie die Apps bereit.  

- **Azure AD-App für Configuration Manager**. Wenn Sie nach Abschluss des Setups Apps bereitstellen oder Verbindungsprobleme beheben müssen, sehen Sie den Abschnitt [Erstellen und Importieren von Apps für Configuration Manager](#create-and-import-app-for-configuration-manager) ein. Diese App erfordert die Berechtigungen **Write CM Collection Data** (CM-Sammlungsdaten schreiben) und **Read CM Collection Data** (CM-Sammlungsdaten lesen) für die **Configuration Manager-Dienst**-API.  

### <a name="create-and-import-app-for-configuration-manager"></a>Erstellen und Importieren von Apps für Configuration Manager

Wenn Sie die Azure AD-App für Configuration Manager nicht im Assistenten zum Konfigurieren von Azure-Diensten erstellen können oder eine vorhandene App wiederverwenden möchten, müssen Sie sie manuell erstellen und importieren. Führen Sie nach Abschluss des [anfänglichen Onboardings](set-up.md#initial-onboarding) im Desktop Analytics-Portal die folgenden Schritte aus:

#### <a name="create-app-in-azure-ad"></a>Erstellen einer App in Azure AD

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com) als Benutzer mit *globalen Administratorberechtigungen*, navigieren Sie zu **Azure Active Directory**, und wählen Sie **App-Registrierungen** aus. Wählen Sie anschließend **Neue Registrierung** aus.  

2. Konfigurieren Sie im Bereich **Erstellen** die folgenden Einstellungen:  

    - **Name**: Ein eindeutiger Name, der die App identifiziert, z. B. `Desktop-Analytics-Connection`  

    - **Unterstützte Kontotypen**: **Nur Konten in diesem Organisationsverzeichnis (Contoso)**

    - **Umleitungs-URI (optional)** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Wählen Sie **Registrieren** aus.  

3. Wählen Sie die App aus, und notieren Sie die **Anwendungs-ID (Client)** und die **Verzeichnis-ID (Mandant)** . Bei den Werten handelt es sich um GUIDs, mit denen die Configuration Manager-Verbindung konfiguriert wird.  

4. Wählen Sie im Menü **Verwalten** die Option **Certificates & secrets** (Zertifikate und geheime Schlüssel) aus. Wählen Sie **Neuer geheimer Clientschlüssel** aus. Geben Sie eine **Beschreibung** ein, geben Sie eine Ablauffrist an, und wählen Sie anschließend **Hinzufügen** aus. Kopieren Sie den **Wert** des Schlüssels, mit dem die Configuration Manager-Verbindung konfiguriert wird.

    > [!Important]  
    > Dies ist die einzige Möglichkeit, den Wert des Schlüssels zu kopieren. Wenn Sie ihn jetzt nicht kopieren, müssen Sie später einen weiteren Schlüssel erstellen.  
    >
    > Speichern Sie den Wert des Schlüssels an einem sicheren Speicherort.  

5. Wählen Sie im Menü **Verwalten** die Option **API-Berechtigungen** aus.  

    1. Wählen Sie im Bereich **API-Berechtigungen** die Option **Berechtigung hinzufügen** aus.  

    2. Wechseln Sie im Bereich **API-Berechtigungen anfordern** zu **Von meiner Organisation verwendete APIs**.  

    3. Suchen Sie nach der **Configuration Manager-Microservice**-API.  

    4. Wählen Sie die Gruppe **Anwendungsberechtigungen** aus. Erweitern Sie **CmCollectionData**, und wählen Sie die beiden folgenden Berechtigungen aus: **Write CM Collection Data** (CM-Sammlungsdaten schreiben) und **Read CM Collection Data** (CM-Sammlungsdaten lesen).  

    5. Wählen Sie **Berechtigungen hinzufügen** aus.  

6. Wählen Sie im Bereich **API-Berechtigungen** die Option **Administratoreinwilligung erteilen** aus. Wählen Sie **Ja** aus.  

#### <a name="import-app-in-configuration-manager"></a>Importieren von Apps in Configuration Manager

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus. Wählen Sie im Menüband **Azure-Dienste konfigurieren** aus.  

2. Konfigurieren Sie auf der Seite **Azure-Dienste** des Assistenten für Azure-Dienste die folgenden Einstellungen:  

    - Geben Sie einen **Namen** für das Objekt in Configuration Manager an.  

    - Geben Sie eine optionale **Beschreibung** an, mit der Sie den Dienst identifizieren können.  

    - Wählen Sie in der Liste der verfügbaren Dienste **Desktop Analytics** aus.  
  
   Wählen Sie **Weiter** aus.  

3. Wählen Sie auf der Seite **App** die geeignete **Azure-Umgebung** aus. Wählen Sie anschließend für die Web-App **Importieren** aus. Konfigurieren Sie im Fenster **Apps importieren** die folgenden Einstellungen:  

    - **Name des Azure AD-Mandanten**: Mit diesem Namen wird der Mandant in Configuration Manager bezeichnet.  

    - **ID des Azure AD-Mandanten**: Dies ist die **Verzeichnis-ID**, die Sie aus Azure AD kopiert haben.  

    - **Client-ID:** Dies ist die **Anwendungs-ID**, die Sie aus der Azure AD-App kopiert haben.  

    - **Geheimer Schlüssel**: Dies ist der **Wert** des Schlüssels, den Sie aus der Azure AD-App kopiert haben.  

    - **Ablauf des geheimen Schlüssels**: Das Ablaufdatum des Schlüssels.  

    - **App-ID-URI**: Diese Einstellung sollte automatisch mit dem folgenden Wert aufgefüllt werden: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Wählen Sie **Überprüfen** und anschließend **OK** aus, um das Fenster „Apps importieren“ zu schließen. Wählen Sie auf der Seite „App“ des Assistenten für Azure-Dienste **Weiter** aus.  

Weitere Informationen zum weiteren Bearbeiten des Assistenten auf der Seite **Diagnosedaten** finden Sie unter [Herstellen einer Verbindung mit dem Dienst](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Problembehandlung für Apps in Configuration Manager

Wenn beim Erstellen oder Importieren der App Probleme auftreten, durchsuchen Sie das Protokoll **SMSAdminUI.log** nach dem jeweiligen Fehler. Überprüfen Sie anschließend die folgenden Konfigurationen:

- Sie haben den Mandanten erfolgreich beim Desktop Analytics-Dienst registriert. Weitere Informationen finden Sie unter [Einrichten von Desktop Analytics](set-up.md).

- Auf alle erforderlichen Endpunkte kann zugegriffen werden. Weitere Informationen finden Sie unter [Endpunkte](enable-data-sharing.md#endpoints).

- Stellen Sie sicher, dass der sich anmeldende Benutzer über die richtigen Berechtigungen verfügt. Weitere Informationen finden Sie unter [Voraussetzungen](overview.md#prerequisites).

- Stellen Sie sicher, dass sich der Benutzer generell bei Azure anmelden kann. Durch diese Aktion wird bestimmt, ob allgemeine Azure AD-Authentifizierungsprobleme vorliegen.

- Überprüfen Sie Statusmeldungen für die Komponente **SMS_SERVICE_CONNECTOR** in Bezug auf den *Desktop Analytics-Worker*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a> Anwendungsrolle MALogAnalyticsReader

Beim Einrichten von Desktop Analytics erteilen Sie die Zustimmung im Namen Ihrer Organisation. Mit dieser Zustimmung wird der Anwendung MALogAnalyticsReader die Rolle „Log Analytics-Leser“ für den Arbeitsbereich zugewiesen. Diese Anwendungsrolle ist für Desktop Analytics erforderlich.

Wenn während des Setups ein Problem mit diesem Vorgang auftritt, führen Sie die folgenden Schritte aus, um diese Berechtigung manuell hinzuzufügen:

1. Wechseln Sie zum [Azure-Portal](https://portal.azure.com), und wählen Sie **Alle Ressourcen**aus. Wählen Sie den Arbeitsbereich vom Typ **Log Analytics** aus.  

2. Wählen Sie im Menü des Arbeitsbereichs **Zugriffssteuerung (IAM)** und anschließend **Hinzufügen** aus.  

3. Konfigurieren Sie im Bereich **Berechtigungen hinzufügen** die folgenden Einstellungen:  

    - **Rolle**: **Leser**  

    - **Zugriff zuweisen zu**: **Azure AD-Benutzer, -Gruppe oder -Anwendung**  

    - **Auswählen**: **MALogAnalyticsReader**  

4. Wählen Sie **Speichern** aus.

Im Portal wird eine Benachrichtigung ausgegeben, dass die Rollenzuweisung hinzugefügt wurde.

## <a name="data-latency"></a>Datenlatenz

<!-- 3846531 -->
Wenn Sie beim erstmaligen Einrichten von Desktop Analytics neue Clients registrieren oder neue Bereitstellungspläne konfigurieren, zeigen die Berichte in Configuration Manager und im Desktop Analytics-Portal möglicherweise nicht sofort die kompletten Daten an. Es kann zwei bis drei Tage dauern, bis die folgenden Schritte ausgeführt werden:

- Aktive Geräte senden Diagnosedaten an den Desktop Analytics-Dienst.
- Die Daten werden vom Dienst verarbeitet.
- Der Dienst wird mit Ihrem Configuration Manager-Standort synchronisiert.

Beim Synchronisieren von Gerätesammlungen aus Ihrer Configuration Manager-Hierarchie mit Desktop Analytics kann es bis zu einer Stunde dauern, bis die betreffenden Sammlungen im Desktop Analytics-Portal angezeigt werden. Ebenso kann es beim Erstellen eines Bereitstellungsplans in Desktop Analytics bis zu einer Stunde dauern, bis die neuen Sammlungen für den Bereitstellungsplan in der Configuration Manager-Hierarchie angezeigt werden. Die Sammlungen werden von den primären Standorten erstellt, und der Standort der zentralen Verwaltung wird mit Desktop Analytics synchronisiert. Es kann bis zu 24 Stunden dauern, bis Configuration Manager die Sammlungsmitgliedschaft bewertet und aktualisiert. Sie können diesen Vorgang beschleunigen, indem Sie die Sammlungsmitgliedschaft manuell aktualisieren.<!-- 4984639 -->

> [!Note]
> Damit bei manuellen Aktualisierungen von Sammlungen die Änderungen widergespiegelt werden, muss zuerst die Komponente SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker synchronisiert werden. Die Ausführung dieses Vorgangs kann bis zu einer Stunde dauern. Weitere Informationen finden Sie in der Datei **M365ADeploymentPlanWorker.log**.

Es gibt zwei Arten von Daten im Desktop Analytics-Portal: **Administratordaten** und **Diagnosedaten**:

- **Administratordaten** beziehen sich auf alle Änderungen, die Sie an der Arbeitsbereichskonfiguration vornehmen. Wenn Sie beispielsweise die **Upgradeentscheidung** oder die **Wichtigkeit** eines Objekts ändern, ändern Sie Administratordaten. Diese Änderungen wirken sich häufig kumulativ aus, da sie den Bereitschaftsstatus eines Geräts bei Installation des betreffenden Objekts ändern können.

- **Diagnosedaten** beziehen sich auf die Systemmetadaten, die von Clientgeräten zu Microsoft hochgeladen werden. Diese Daten bilden die Grundlage der Analysen von Desktop Analytics. Hierzu zählen Merkmale wie Gerätebestand, Sicherheitsstatus und Featureupdatestatus.

Standardmäßig werden alle Daten im Desktop Analytics-Portal automatisch täglich aktualisiert. Diese Aktualisierung umfasst Änderungen der Diagnosedaten sowie alle Änderungen, die Sie an der Konfiguration vornehmen (Administratordaten). Sie werden täglich um 08:00 Uhr UTC in Ihrem Desktop Analytics-Portal angezeigt.

Wenn Sie Administratordaten ändern, können Sie eine bedarfsgesteuerte Aktualisierung der Administratordaten in Ihrem Arbeitsbereich auslösen. Öffnen Sie auf einer beliebigen Seite im Desktop Analytics-Portal das Flyout zur Datenaktualität:

![Screenshot der Registerkarte des Flyouts zur Datenaktualität im Desktop Analytics-Portal](media/data-currency-flyout.png)

Wählen Sie dann **Änderungen übernehmen** aus:

![Screenshot des erweiterten Flyouts zur Datenaktualität im Desktop Analytics-Portal](media/data-currency-flyout-expand.png)

Dieser Vorgang dauert in der Regel 15 bis 60 Minuten. Die Dauer hängt von der Größe Ihres Arbeitsbereichs und vom Umfang der zu verarbeitenden Änderungen ab. Wenn Sie eine bedarfsgesteuerte Datenaktualisierung anfordern, bewirkt dies keine Änderung der Diagnosedaten.  Weitere Informationen finden Sie unter [Desktop Analytics – Häufig gestellte Fragen](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Wenn innerhalb des obigen Zeitfensters keine Aktualisierung von Änderungen erfolgt, warten Sie weitere 24 Stunden auf die nächste tägliche Aktualisierung. Sehen Sie bei längeren Verzögerungen das Dashboard zur Dienstintegrität ein. Wenn der Dienst als fehlerfrei gemeldet wird, wenden Sie sich an den Microsoft-Support.<!-- 3896921 -->

> [!IMPORTANT]
> Die Desktop Analytics-Option **Aktuelle Daten anzeigen** ist veraltet. Diese Aktion wird in einer zukünftigen Version des Desktop Analytics-Diensts entfernt. Weitere Informationen finden Sie unter [Veraltete Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  
