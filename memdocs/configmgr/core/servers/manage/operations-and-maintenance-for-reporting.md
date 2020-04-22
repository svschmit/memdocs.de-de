---
title: Vorgänge und Wartungstasks für die Berichterstellung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Verwalten von Berichten und Berichtsabonnements in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694418"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Vorgänge und Wartungstasks für die Berichterstattung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sobald die für die Berichterstellung in Configuration Manager erforderliche Infrastruktur vorhanden ist, werden üblicherweise einige Schritte zur Verwaltung von Berichten und Berichtsabonnements ausgeführt.

> [!NOTE]
> In diesem Artikel geht es um Berichte in den SQL Server Reporting Services. Ab Version 2002 können Sie die Berichterstellung mit dem Power BI-Berichtsserver integrieren. Weitere Informationen hierzu finden Sie unter [Integration mit dem Power BI-Berichtsserver](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Ausführen eines Berichts in den Reporting Services

Configuration Manager speichert die Berichte in den SQL Server Reporting Services. Der Bericht ruft Daten aus der Configuration Manager-Standortdatenbank ab. Sie können in der Configuration Manager-Konsole oder mithilfe des Berichts-Managers in einem Webbrowser auf die Berichte zugreifen. Berichte können in einem Webbrowser auf jedem Computer geöffnet werden, der auf den Reporting Services-Punkt zugreifen kann, wenn der entsprechende Benutzer über die erforderlichen Berechtigungen zum Anzeigen der Berichte verfügt. Zum Ausführen von Berichten benötigen Sie das Recht **Lesen** für die Berechtigung **Standort** sowie die Berechtigung **Bericht ausführen** für bestimmte Objekte.

Wenn Sie einen Bericht ausführen, werden Titel, Beschreibung und Kategorie des Berichts in der Sprache des lokalen Betriebssystems angezeigt. Weitere Informationen finden Sie unter [Sprachen für Berichte](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> Der Berichts-Manager ist ein webbasiertes Zugriffs- und Verwaltungstool für Berichte. Sie können damit eine einzelne Berichtsserverinstanz über eine HTTPS-Verbindung verwalten. Verwenden Sie den Berichts-Manager für operative Aufgaben: Zeigen Sie Berichte an, ändern Sie Berichtseigenschaften, und verwalten Sie zugeordnete Berichtsabonnements. In diesem Artikel werden die Schritte zum Anzeigen von Berichten und Ändern von Berichtseigenschaften im Berichts-Manager beschrieben. Unter [Was ist der Berichts-Manager?](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode) finden Sie weitere Informationen zu anderen Optionen im Berichts-Manager.

Verwenden Sie die folgenden Verfahren, um Configuration Manager-Berichten auszuführen.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Ausführen eines Berichts in der Configuration Manager-Konsole

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Berichterstellung**, und klicken Sie dann auf **Berichte**. Unter diesem Knoten sind die verfügbaren Berichte aufgeführt.

    > [!TIP]
    > Wenn dort keine Berichte aufgelistet sind, vergewissern Sie sich, dass der Reporting Services-Punkt installiert und konfiguriert ist. Weitere Informationen finden Sie unter [Konfigurieren der Berichterstellung](configuring-reporting.md).

1. Klicken Sie auf den Bericht, den Sie ausführen möchten. Klicken Sie im Menüband auf der Registerkarte **Home** (Start) im Bereich **Berichtsgruppe** auf **Ausführen**, um den Bericht zu öffnen.

1. Wenn Parameter erforderlich sind, geben Sie diese Parameter an, und klicken Sie dann auf **Bericht anzeigen**.

### <a name="run-a-report-in-a-web-browser"></a>Ausführen eines Berichts in einem Webbrowser

1. Navigieren Sie in Ihrem Webbrowser zur URL des Berichts-Managers, beispielsweise `https://Server1/Reports`. Diese Adresse finden Sie auf der Seite **Berichts-Manager-URL** im Konfigurations-Manager für Reporting Services.

1. Klicken Sie im Berichts-Manager auf den Berichtsordner für Configuration Manager, z. B. **ConfigMgr_CAS**.

    > [!TIP]
    > Wenn im Berichts-Manager keine Berichte aufgelistet sind, vergewissern Sie sich, dass der Reporting Services-Punkt installiert und konfiguriert ist. Weitere Informationen finden Sie unter [Konfigurieren der Berichterstellung](configuring-reporting.md).

1. Klicken Sie auf die Berichtskategorie des Berichts, den Sie ausführen möchten, und dann auf den gewünschten Bericht. Der Bericht wird im Berichts-Manager geöffnet.

1. Wenn Parameter erforderlich sind, geben Sie diese Parameter an, und klicken Sie dann auf **Bericht anzeigen**.

## <a name="modify-the-properties-of-a-report"></a>Ändern der Eigenschaften eines Berichts

Zu den Berichtseigenschaften gehören Name und Beschreibung des Berichts. Die Eigenschaften eines Berichts können in der Configuration Manager-Konsole angezeigt werden.

Gehen Sie wie folgt vor, um diese Eigenschaften im Berichts-Manager zu ändern:

1. Navigieren Sie in Ihrem Webbrowser zur URL des Berichts-Managers, beispielsweise `https://Server1/Reports`.

1. Klicken Sie im Berichts-Manager auf den Berichtsordner für Configuration Manager, z. B. **ConfigMgr_CAS**.

1. Klicken Sie auf die entsprechende Berichtskategorie und dann auf den gewünschten Bericht. Der Bericht wird im Berichts-Manager geöffnet.

1. Klicken Sie auf die Registerkarte **Eigenschaften**. Ändern Sie Name und Beschreibung des Berichts, und klicken Sie anschließend auf **Übernehmen**.

Der Berichts-Manager speichert die Berichtseigenschaften auf dem Berichtsserver. Die aktualisierten Berichtseigenschaften werden in der Configuration Manager-Konsole angezeigt.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a> Bearbeiten eines Berichts

Wenn ein bereits vorhandener Configuration Manager-Bericht nicht die gewünschten Informationen abruft, bearbeiten Sie ihn im Berichts-Generator. Mit dem Berichts-Generator können Sie auch Layout und Design des Berichts ändern. Sie können zwar einen Standardbericht direkt anpassen, die beste Variante ist jedoch, den Bericht zu klonen. Öffnen Sie den Bericht, um ihn zu bearbeiten, und klicken Sie dann auf **Speichern unter**.

Wenn Sie einen Bericht bearbeiten möchten, müssen Sie über die Berechtigung **Site Modify** (Standort ändern) sowie die Berechtigung **Bericht ändern** für die konkreten Objekte im Bericht verfügen.

> [!IMPORTANT]
> Bei Standortupdates werden integrierte Berichte beibehalten. Wenn Sie einen Standardbericht ändern, wird dem Namen des Berichts beim Aktualisieren des Standorts ein Unterstrich (`_`) als Präfix vorangestellt. Durch dieses Verhalten wird sichergestellt, dass der geänderte Bericht beim Aktualisieren des Standorts nicht durch den Standardbericht überschrieben wird.
>
> Wenn Sie vordefinierte Berichte ändern, sichern Sie Ihre benutzerdefinierten Berichte, bevor Sie ein Standortupdate installieren. Stellen Sie nach dem Update den Bericht in den Reporting Services wieder her. Wenn Sie an einem vordefinierten Bericht erhebliche Änderungen vornehmen möchten, erstellen Sie stattdessen einen neuen Bericht. Neue Berichte, die Sie erstellt haben, werden bei einem Upgrade des Standorts nicht überschrieben.

Wenden Sie das folgende Verfahren an, um die Eigenschaften eines Configuration Manager-Berichts zu ändern.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Berichterstellung**, und klicken Sie dann auf den Knoten **Berichte**.

1. Klicken Sie auf den Bericht, den Sie ändern möchten. Klicken Sie im Menüband auf der Registerkarte **Home** (Start) im Bereich **Berichtsgruppe** auf **Bearbeiten**. Sie werden möglicherweise dazu aufgefordert, Anmeldeinformationen einzugeben. Wenn der Berichts-Generator nicht auf dem Computer installiert ist, fordert Configuration Manager Sie dazu auf, ihn zu installieren. Der Berichts-Generator ist erforderlich, um Berichte ändern und erstellen zu können.

1. Ändern Sie die relevanten Berichtseinstellungen im Berichts-Generator. Klicken Sie auf **Speichern**, um den Bericht auf dem Berichtsserver zu speichern.

## <a name="create-reports"></a>Erstellen von Berichten

Sie können zwei Arten von Berichten erstellen:

- Bei einem **modellbasierten Bericht** können Sie die Elemente, die Sie in den Bericht aufnehmen möchten, interaktiv auswählen. Weitere Informationen zum Erstellen von benutzerdefinierten Berichtsmodellen finden Sie unter [Erstellen benutzerdefinierter Berichtsmodelle für Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

- Bei einem **SQL-basierten Bericht** können Sie auf einer SQL-Anweisung für Berichte basierende Daten abrufen.

> [!IMPORTANT]
> Damit ein neuer Bericht erstellt werden kann, muss Ihr Konto über die Berechtigung **Site Modify**(Standort ändern) verfügen. Sie können Berichte nur in Ordnern erstellen, für die Sie über die Berechtigung **Bericht ändern** verfügen.

### <a name="create-a-model-based-report"></a>Erstellen eines modellbasierten Berichts

Gehen Sie wie folgt vor, um einen modellbasierten Configuration Manager-Bericht zu erstellen.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus.

1. Klicken Sie im Menüband auf der Registerkarte **Home** (Start) im Bereich **Erstellen** auf **Bericht erstellen**. Durch diese Aktion wird der **Assistent zum Erstellen von Berichten** geöffnet.

1. Konfigurieren Sie auf der Seite **Informationen** die folgenden Einstellungen:

    - **Typ:** Klicken Sie auf **modellbasierter Bericht**.

    - **Name:** Geben Sie einen Namen für den Bericht an.

    - **Beschreibung:** Geben Sie eine Beschreibung für den Bericht an.

    - **Server:** Zeigt den Namen des Berichtsservers an, auf dem Sie diesen Bericht erstellen

    - **Pfad:** Klicken Sie auf **Durchsuchen**, um einen Ordner anzugeben, in dem der Bericht gespeichert werden soll.

1. Wählen Sie auf der Seite **Modellauswahl** ein verfügbares Modell zum Erstellen des Berichts aus der Liste aus. Im Bereich **Vorschau** werden die SQL Server-Ansichten und -Entitäten angezeigt, die in dem entsprechenden Berichtsmodell verfügbar sind.

1. Schließen Sie den Assistenten zum Erstellen von Berichten ab.

1. Öffnen Sie den Berichts-Generator, um die Berichtseinstellungen zu konfigurieren. Weitere Informationen finden Sie unter [Bearbeiten eines Configuration Manager-Berichts](#bkmk_edit).

1. Erstellen Sie im Berichts-Generator das Berichtslayout, wählen Sie Daten in den verfügbaren SQL Server-Ansichten aus, und fügen Sie Parameter zum Bericht hinzu.

1. Klicken Sie auf **Ausführen**, um Ihren Bericht auszuführen. Überprüfen Sie, ob die erwarteten Informationen im Bericht enthalten sind. Klicken Sie auf **Design**, um den Bericht, falls nötig, weiter zu ändern.

1. Klicken Sie auf **Speichern**, um den Bericht auf dem Berichtsserver zu speichern.

### <a name="create-a-sql-based-report"></a>Erstellen eines SQL-basierten Berichts

Wenn Sie eine SQL-Anweisung für einen benutzerdefinierten Bericht erstellen, verweisen Sie nicht direkt auf SQL Server-Tabellen. Verweisen Sie immer auf unterstützte SQL Server-Ansichten für die Berichterstellung aus der Standortdatenbank. Die Namen dieser Ansichten beginnen mit `v_`. Weitere Informationen finden Sie unter [Erstellen von benutzerdefinierten Berichten in Configuration Manager mithilfe von SQL Server-Ansichten](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

Sie können auch auf öffentliche gespeicherte Prozeduren aus der Standortdatenbank verweisen. Die Namen dieser gespeicherten Prozeduren beginnen mit `sp_`.

Gehen Sie wie folgt vor, um einen SQL-basierten Configuration Manager-Bericht zu erstellen.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus.

1. Klicken Sie im Menüband auf der Registerkarte **Home** (Start) im Bereich **Erstellen** auf **Bericht erstellen**. Durch diese Aktion wird der **Assistent zum Erstellen von Berichten** geöffnet.

1. Konfigurieren Sie auf der Seite **Informationen** die folgenden Einstellungen:

    - **Typ:** Klicken Sie auf **SQL-basierter Bericht**.

    - **Name:** Geben Sie einen Namen für den Bericht an.

    - **Beschreibung:** Geben Sie eine Beschreibung für den Bericht an.

    - **Server:** Zeigt den Namen des Berichtsservers an, auf dem Sie diesen Bericht erstellen

    - **Pfad:** Klicken Sie auf **Durchsuchen**, um einen Ordner anzugeben, in dem der Bericht gespeichert werden soll.

1. Schließen Sie den Assistenten zum Erstellen von Berichten ab.

1. Öffnen Sie den Berichts-Generator, um die Berichtseinstellungen zu konfigurieren. Weitere Informationen finden Sie unter [Bearbeiten eines Configuration Manager-Berichts](#bkmk_edit).

1. Geben Sie im Berichts-Generator die SQL-Anweisung für den Bericht an. Sie können die SQL-Anweisung auch mithilfe von Spalten in verfügbaren Ansichten erstellen. Fügen Sie Parameter zum Bericht hinzu, wenn dies erforderlich ist.

1. Klicken Sie auf **Ausführen**, um Ihren Bericht auszuführen. Überprüfen Sie, ob die erwarteten Informationen im Bericht enthalten sind. Klicken Sie auf **Design**, um den Bericht, falls nötig, weiter zu ändern.

1. Klicken Sie auf **Speichern**, um den Bericht auf dem Berichtsserver zu speichern.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a> Verwalten von Berichtsabonnements

Mithilfe von Berichtsabonnements in SQL Server Reporting Services können Sie die automatische Übermittlung von angegebenen Berichten per E-Mail oder an eine Dateifreigabe in geplanten Zeitintervallen konfigurieren. Verwenden Sie den **Assistenten zum Erstellen von Abonnements** in Configuration Manager, um Berichtsabonnements zu konfigurieren.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Erstellen eines Berichtsabonnements zum Übermitteln eines Berichts an eine Dateifreigabe

Wenn Sie ein Berichtsabonnement zum Übermitteln eines Berichts an eine Dateifreigabe erstellen, kopieren die Reporting Services den Bericht im angegebenen Format in die angegebene Dateifreigabe. Sie können die Übermittlung von nur einem Bericht auf einmal abonnieren bzw. anfordern.

Wenn Sie ein Abonnement erstellen, das eine Dateifreigabe verwendet, geben Sie einen vorhandenen freigegebenen Ordner als Ziel an. Der Berichtsserver erstellt den Ordner oder die Netzwerkfreigabe nicht. Wenn Sie den Zielordner in einem Abonnement angeben, verwenden Sie einen UNC-Pfad. Verwenden Sie dabei keinen umgekehrten Schrägstrich (`\`) am Ende des Ordnerpfads. Ein gültiger UNC-Pfad für den Zielordner könnte beispielsweise folgendermaßen aussehen: `\\server\reportfiles\operations\2001`.

> [!NOTE]
> Beim Erstellen des Abonnements geben Sie einen Benutzernamen und ein Kennwort an. Dieses Konto muss mit **Schreibberechtigung** für den Zielordner auf die Freigabe zugreifen können.

Die Reporting Services können Berichte in verschiedenen Dateiformaten rendern. Beispiele hierfür sind MTHML und Excel. Das Format wird beim Erstellen des Abonnements ausgewählt. Sie können zwar jedes unterstützte Renderformat auswählen, doch einige Formate sind zum Rendern besser geeignet als andere.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Beschränkungen bei Berichtsabonnements für Dateifreigaben

Im Folgenden sind die Beschränkungen bei Berichtsabonnements für Dateifreigaben aufgeführt:

- Im Gegensatz zu Berichten, die Sie auf einem Berichtsserver hosten und verwalten, übermitteln die Reporting Services Berichte an freigegebene Ordner als statische Dateien.

- Interaktive Features des Berichts funktionieren bei als Dateien gespeicherten Berichten nicht. Der Bericht stellt interaktive Features als statische Elemente dar.

- Wenn im Bericht Diagramme enthalten sind, wird die Standarddarstellung verwendet.

- Wenn im Bericht ein anderer Bericht verlinkt ist, wird der Link als statischer Text gerendert.

Wenn interaktive Features in einem übermittelten Bericht erhalten bleiben sollen, übermitteln Sie den Bericht per E-Mail. Weitere Informationen finden Sie im Abschnitt [Erstellen eines Berichtsabonnements zum Übermitteln eines Berichts per E-Mail](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Vorgehen beim Erstellen eines Berichtsabonnements für eine Dateifreigabe

Gehen Sie wie folgt vor, um ein Berichtsabonnement zur Übermittlung eines Berichts an eine Dateifreigabe zu erstellen.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus.

1. Klicken Sie auf einen Berichtsordner und dann auf den Bericht, den Sie abonnieren möchten. Klicken Sie im Menüband auf der Registerkarte **Home** (Start) im Bereich **Berichtsgruppe** auf **Abonnement erstellen**. Durch diese Aktion wird der **Assistent zum Erstellen von Abonnements** geöffnet.

1. Konfigurieren Sie auf der Seite **Abonnementübermittlung** die folgenden Einstellungen:  

    - **Bericht übermittelt von:** Wählen Sie **Windows-Dateifreigabe** aus.

    - **Dateiname:** Geben Sie den Dateinamen des Berichts an. Standardmäßig verfügt die Berichtsdatei über kein Suffix. Klicken Sie auf **Dateierweiterung beim Erstellen hinzufügen**, um basierend auf dem Format automatisch ein Suffix hinzuzufügen.

    - **Pfad:** Geben Sie einen UNC-Pfad zu einem vorhandenen Ordner an, an den Sie den Bericht übermitteln möchten. Beispiel: `\\server\reportfiles\operations`.

    - **Renderformat:** Wählen Sie eines der folgenden Formate für die Berichtsdatei:

      - **XML-Datei mit Berichtsdaten**
      - **CSV (Komma-getrennt)**
      - **TIFF-Datei**
      - **Acrobat-Datei (PDF)**
      - **HTML 4.0**
        > [!NOTE]
        > Wenn Ihr Bericht Bilder enthält, sind diese im Format HTML 4.0 nicht enthalten.
      - **MHTML (Webarchiv)**
      - **RPL-Renderer** (Report Page Layout, Berichtsseitenlayout)
      - **Excel**
      - **Word**

    - **Benutzername:** Geben Sie ein Windows-Benutzerkonto mit *Schreibberechtigung* für den angegebenen **Pfad** an.

    - **Kennwort:** Geben Sie das Kennwort für das obige Windows-Benutzerkonto an.

    - **Überschreibungsoption:** Wählen Sie eine der folgenden Optionen aus, um zu konfigurieren, wie vorgegangen werden soll, wenn eine Datei mit dem gleichen Namen bereits im Zielordner vorhanden ist.

      - **Vorhandene Datei mit einer neueren Version überschreiben**
      - **Vorhandene Datei nicht überschreiben**
      - **Dateinamen inkrementieren, wenn neuere Versionen hinzugefügt werden:** Bei dieser Option wird im Dateinamen des neuen Berichts eine Zahl angehängt, um diesen von früheren Versionen zu unterscheiden.

    - **Beschreibung:** Optional können Sie hier weitere Informationen zu diesem Berichtsabonnement angeben.

1. Wählen Sie auf der Seite **Abonnementzeitplan** eine der folgenden Optionen für den Übermittlungszeitplan des Berichtsabonnements aus:

    - **Freigegebenen Zeitplan verwenden:** Ein freigegebener Zeitplan ist ein zuvor festgelegter Zeitplan, der von anderen Berichtsabonnements verwendet werden kann. Wählen Sie auch einen freigegebenen Zeitplan aus, wenn Sie diese Option auswählen. Wenn keine freigegebenen Zeitpläne vorhanden sind, klicken Sie auf die Option zum Erstellen eines neuen Zeitplans.

    - **Neuen Zeitplan erstellen:** Konfigurieren Sie den Zeitplan für das Ausführen des Berichts. Dieser Zeitplan enthält das Intervall, die Startzeit und das Startdatum sowie das Enddatum für das Abonnement. Standardmäßig wird bei einem neuen Abonnement ein neuer Zeitplan erstellt mit Ausführung jede Stunde ab dem aktuellen Datum und der aktuellen Uhrzeit.

1. Geben Sie auf der Seite **Abonnementparameter** die Parameter an, die für das unbeaufsichtigte Ausführen des Berichts erforderlich sind. Wenn der Bericht über keine Parameter verfügt, wird diese Seite im Assistenten nicht angezeigt.

1. Schließen Sie den Assistenten ab.

1. Überprüfen Sie, ob Configuration Manager das Berichtsabonnement erfolgreich erstellt hat. Klicken Sie auf den Knoten **Abonnements**, um Berichtsabonnements anzuzeigen und zu ändern.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a> Erstellen eines Berichtsabonnements zum Übermitteln eines Berichts per E-Mail

Wenn Sie ein Berichtsabonnement zum Übermitteln eines Berichts per E-Mail erstellen, senden die Reporting Services eine E-Mail an die von Ihnen konfigurierten Empfänger. In dieser E-Mail ist der Bericht als Anlage enthalten. Der Berichtsserver überprüft E-Mail-Adressen nicht und ruft auch keine E-Mail-Adressen von einem E-Mail-Server ab. Sie können Berichte per E-Mail an alle gültigen E-Mail-Konten innerhalb oder außerhalb Ihrer Organisation senden.

> [!NOTE]
> Wenn Sie die **E-Mail**-Abonnementoption aktivieren möchten, müssen Sie die E-Mail-Einstellungen in den Reporting Services konfigurieren. Weitere Informationen finden Sie unter [E-Mail-Übermittlung in Reporting Services](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

Sie können eine oder beide der folgenden E-Mail-Übermittlungsoptionen auswählen:

- Senden Sie eine Benachrichtigung mit einem Link zum generierten Bericht.

- Senden Sie einen eingebetteten oder angehängten Bericht. Ob der Bericht eingebettet oder angehängt wird, hängt vom Renderformat und vom Browser ab.

  - Wenn Ihr Browser HTML 4.0 und MHTML unterstützt, und Sie das Format **MHTML (Webarchiv)** auswählen, wird der Bericht in die Nachricht eingebettet.
  - Bei allen anderen Formaten wird der Bericht als Anlage übermittelt.
  - Die Größe der Anlage oder der Nachricht wird von den Reporting Services vor dem Senden des Berichts nicht überprüft. Wenn der Grenzwert des E-Mail-Servers für die maximal zulässige Größe durch die Anlage oder die Nachricht überschritten wird, wird der Bericht nicht übermittelt.

Gehen Sie wie folgt vor, um ein Berichtsabonnement zur Übermittlung eines Berichts per E-Mail zu erstellen.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus.

1. Klicken Sie auf einen Berichtsordner und dann auf den Bericht, den Sie abonnieren möchten. Klicken Sie im Menüband auf der Registerkarte **Home** (Start) im Bereich **Berichtsgruppe** auf **Abonnement erstellen**. Durch diese Aktion wird der **Assistent zum Erstellen von Abonnements** geöffnet.

1. Konfigurieren Sie auf der Seite **Abonnementübermittlung** die folgenden Einstellungen:  

    - **Bericht übermittelt von:** Wählen Sie **E-Mail** aus.

    - **Nach:** Geben Sie eine gültige E-Mail-Adresse als Empfänger an.

        > [!NOTE]
        > Sie können mehrere Empfänger eingeben, indem Sie die E-Mail-Adressen durch Semikolons (`;`) trennen.

    - **Cc:** Optional können Sie hier eine E-Mail-Adresse angeben, an die der Bericht per Kopie gesendet werden soll.

    - **Bcc:** Optional können Sie hier eine E-Mail-Adresse angeben, an die der Bericht per Blindkopie gesendet werden soll.

    - **Antwort an:** Geben Sie die Antwortadresse an. Wenn der Empfänger auf die E-Mail antwortet, wird die Antwort an diese Adresse gesendet.

    - **Betreff**: Geben Sie eine Betreffzeile für die Abonnement-E-Mail an.

    - **Priorität:** Wählen Sie die Prioritätskennzeichnung für die E-Mail aus: **Niedrig**, **Normal** oder **Hoch**. Microsoft Exchange verwendet diese Kennzeichnung, um die Wichtigkeit der E-Mail anzugeben.

    - **Kommentar**: Geben Sie Text für den Nachrichtentext der Abonnement-E-Mail an.

    - **Beschreibung:** Optional können Sie hier weitere Informationen zu diesem Berichtsabonnement angeben.

    - **Link einschließen:** Nehmen Sie die URL zu diesem Bericht in den Nachrichtentext der E-Mail auf.

    - **Bericht einschließen:** Hängen Sie den Bericht an die E-Mail an. Verwenden Sie die Option **Renderformat**, um das Format des Berichts, der angehängt werden soll, anzugeben.

    - **Renderformat:** Wählen Sie eines der folgenden Formate für die angehängte Berichtsdatei aus:

      - **XML-Datei mit Berichtsdaten**
      - **CSV (Komma-getrennt)**
      - **TIFF-Datei**
      - **Acrobat-Datei (PDF)**
      - **MHTML (Webarchiv)**
      - **Excel**
      - **Word**

1. Wählen Sie auf der Seite **Abonnementzeitplan** eine der folgenden Optionen für den Übermittlungszeitplan des Berichtsabonnements aus:

    - **Freigegebenen Zeitplan verwenden:** Ein freigegebener Zeitplan ist ein zuvor festgelegter Zeitplan, der von anderen Berichtsabonnements verwendet werden kann. Wählen Sie auch einen freigegebenen Zeitplan aus, wenn Sie diese Option auswählen. Wenn keine freigegebenen Zeitpläne vorhanden sind, klicken Sie auf die Option zum Erstellen eines neuen Zeitplans.

    - **Neuen Zeitplan erstellen:** Konfigurieren Sie den Zeitplan für das Ausführen des Berichts. Dieser Zeitplan enthält das Intervall, die Startzeit und das Startdatum sowie das Enddatum für das Abonnement. Standardmäßig wird bei einem neuen Abonnement ein neuer Zeitplan erstellt mit Ausführung jede Stunde ab dem aktuellen Datum und der aktuellen Uhrzeit.

1. Geben Sie auf der Seite **Abonnementparameter** die Parameter an, die für das unbeaufsichtigte Ausführen des Berichts erforderlich sind. Wenn der Bericht über keine Parameter verfügt, wird diese Seite im Assistenten nicht angezeigt.

1. Schließen Sie den Assistenten ab.

1. Überprüfen Sie, ob Configuration Manager das Berichtsabonnement erfolgreich erstellt hat. Klicken Sie auf den Knoten **Abonnements**, um Berichtsabonnements anzuzeigen und zu ändern.
