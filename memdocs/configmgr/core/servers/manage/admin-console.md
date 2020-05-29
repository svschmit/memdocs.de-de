---
title: Configuration Manager-Konsole
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zur Navigation durch die Configuration Manager-Konsole.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ac5b3ca8e8e2231bb421838fa56b20253ddfcb74
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878373"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Verwenden der Configuration Manager-Konsole

*Gilt für: Configuration Manager (Current Branch)*

Administratoren verwenden die Configuration Manager-Konsole zum Verwalten der Configuration Manager-Umgebung. Dieser Artikel behandelt die Grundlagen der Navigation durch die Konsole.  

## <a name="open-the-console"></a><a name="bkmk_open"></a> Öffnen der Konsole

Die Configuration Manager-Konsole wird immer auf dem Standortserver installiert. Sie können sie auch auf anderen Computern installieren. Weitere Informationen finden Sie unter [Installieren der Configuration Manager-Konsole](../deploy/install/install-consoles.md).

Die einfachste Methode zum Öffnen der Konsole auf einem Windows 10-Computer besteht darin, auf **Start** zu klicken und `Configuration Manager console` einzugeben. Sie müssen möglicherweise nicht die gesamte Zeichenfolge für Windows eingeben, um das gewünschte Ergebnis anzuzeigen.

Suchen Sie beim Durchsuchen des Startmenüs nach dem Symbol der **Configuration Manager-Konsole** in der Gruppe **Microsoft Endpoint Manager**.

![Symbole für Microsoft Endpoint Manager im Startmenü](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Der Startmenüpfad wurde in Version 1910 geändert. In Version 1906 und früher lautet der Ordnername **System Center**. Wenn Sie Configuration Manager auf Version 1910 oder höher aktualisieren, müssen Sie sicherstellen, dass Sie jede interne Dokumentation aktualisieren, die Sie beibehalten, um diesen neuen Speicherort einzuschließen.

## <a name="connect-to-a-site-server"></a>Herstellen einer Verbindung mit einem Standortserver

Die Konsole stellt eine Verbindung mit Ihrem Standortserver der zentralen Verwaltung oder mit Ihren primären Standortservern her. Sie können eine Configuration Manager-Konsole jedoch nicht mit einem sekundären Standort verbinden. Während der Installation haben Sie den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des Standortservers angegeben, mit dem die Konsole eine Verbindung herstellt.

Führen Sie die folgenden Schritte aus, um eine Verbindung mit einem anderen Standortserver herzustellen:

1. Klicken Sie auf den Pfeil am oberen Rand des [Menübands](#ribbon), und klicken Sie dann auf **Mit einem neuen Standort verbinden**.  

    ![Verbinden der Konsole mit einem neuen Standort](media/connect-to-a-new-site.png)  

2. Geben Sie den FQDN des Standortservers ein. Wenn Sie zuvor mit dem Standortserver verbunden waren, können Sie den Server aus der Dropdownliste auswählen.  

    ![Standortverbindungsfenster: Eingeben des FQDN des Standortservers](media/site-server-fqdn.png)  

3. Wählen Sie **Verbinden** aus.  

Ab Version 1810 können Sie die mindestens erforderliche Authentifizierungsebene für den Administratorzugriff auf Configuration Manager-Standorte angeben. Diese Funktion verpflichtet Administratoren dazu, sich mit der erforderlichen Ebene bei Windows anzumelden. Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Navigation

Möglicherweise werden einige Bereiche der Konsole abhängig von der Ihnen zugewiesenen Sicherheitsrolle nicht angezeigt. Weitere Informationen zu Rollen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Arbeitsbereiche

Die Configuration Manager-Konsole verfügt über vier **Arbeitsbereiche**:  

- **Bestand und Konformität**  

- **Softwarebibliothek**  

- **Überwachung**  

- **Verwaltung**  

![Arbeitsbereiche mit Kontextmenü in Configuration Manager](media/configuration-manager-workspaces.png)  

Sie können die Schaltflächen im Arbeitsbereich neu anordnen, indem Sie auf den nach unten zeigenden Pfeil klicken und **Optionen des Navigationsbereichs** auswählen. Wählen Sie ein Element aus, das **nach oben** oder **nach unten** verschoben werden soll. Klicken Sie auf **Zurücksetzen**, um die Standardreihenfolge der Schaltflächen wiederherzustellen.  

![Neuanordnen von Arbeitsbereichen im Fenster „Optionen des Navigationsbereichs“](media/navigation-pane-options.png)  

Sie können die Schaltfläche eines Arbeitsbereichs minimieren, indem Sie auf **Weniger Schaltflächen anzeigen** klicken. Der letzte Arbeitsbereich in der Liste wird zuerst minimiert. Klicken Sie auf eine minimierte Schaltfläche, und klicken Sie dann auf **Weitere Schaltflächen anzeigen**, um die ursprüngliche Darstellung der Schaltfläche wiederherzustellen.

![Minimierte Arbeitsbereiche in der Configuration Manager-Konsole](media/workspace-buttons.png)  

### <a name="nodes"></a>Knoten

Arbeitsbereiche bestehen aus einer Sammlung von **Knoten**. Ein Beispiel hierfür ist der Knoten **Softwareupdategruppen** im Arbeitsbereich **Softwarebibliothek**.

Sobald Sie sich in einem Knoten befinden, können Sie auf den Pfeil klicken, um den Navigationsbereich zu minimieren.  

![Beispielknoten und hervorgehobener Pfeil zum Minimieren](media/software-update-groups-node.png)  

Verwenden Sie die **Navigationsleiste**, um in der Konsole zu navigieren, wenn Sie den Navigationsbereich minimiert haben.  

![Minimierter Navigationsbereich in Configuration Manager](media/minimized-navigation-pane.png)  

Knoten werden in der Konsole manchmal in Ordnern organisiert. Wenn Sie den Ordner auswählen, wird für diesen in der Regel ein **Navigationsindex** oder ein **Dashboard** angezeigt.  

![Navigationsindex zu Softwareupdates in Configuration Manager](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Menüband

Das Menüband befindet sich im oberen Bereich der Configuration Manager-Konsole. Das Menüband kann mehrere Registerkarten enthalten und mit dem Pfeil auf der rechten Seite minimiert werden. Die Schaltflächen im Menüband ändern sich abhängig von dem Knoten. Die meisten Schaltflächen im Menüband sind auch in Kontextmenüs verfügbar.  

![Beispielmenüband, mit mehreren Registerkarten und dem Pfeil zum Minimieren hervorgehoben](media/ribbon.png)

### <a name="details-pane"></a>Detailbereich

Sie können durch Überprüfen des Detailbereichs zusätzliche Informationen zu Elementen abrufen. Der Detailbereich kann eine Registerkarte oder mehrere Registerkarten enthalten. Die Registerkarten variieren je nach Knoten.  

![Beispiel für den Detailbereich in Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Spalten

Sie können Spalten hinzufügen, entfernen, neu anordnen und ihre Größe ändern. Mithilfe dieser Aktionen können Sie die von Ihnen bevorzugten Daten anzeigen. Die verfügbaren Spalten variieren je nach Knoten. Klicken Sie mit der rechten Maustaste auf eine vorhandene Spaltenüberschrift, und wählen Sie anschließend ein Element aus, um eine Spalte zu Ihrer Ansicht hinzuzufügen oder zu entfernen. Sie können Spalten neu anordnen, indem Sie die Spaltenüberschrift an die gewünschte Position ziehen.  

![Spalte in Configuration Manager hinzufügen](media/add-columns.png)  

Sie können im unteren Bereich des Kontextmenüs der Spalten die Sortierung oder Gruppierung nach einer Spalte auswählen. Sie können die Sortierung nach einer Spalte auch auswählen, indem Sie auf die zugehörige Überschrift klicken.  

![Gruppieren nach einer Spalte in Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> Aufheben der Sperre für das Bearbeiten von Objekten

<!--4786915-->

Wenn die Configuration Manager-Konsole nicht mehr reagiert, können Sie möglicherweise 30 Minuten lang (bis die Sperre aufgehoben wird) keine weiteren Änderungen vornehmen. Diese Sperre ist Teil des SEDO-Systems (Serialized Editing of Distributed Objects) für Configuration Manager. Weitere Informationen finden Sie unter [Configuration Manager SEDO (SEDO für Configuration Manager)](../../../develop/core/understand/sedo.md).

Ab der [Current Branch-Version 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences) können Sie die Sperre für eine Tasksequenz löschen. Ab Version 1910 können Sie die Sperre für ein beliebiges Objekt in der Configuration Manager-Konsole löschen.

Diese Aktion gilt nur für Benutzerkonten mit Sperren. Es muss dabei das Gerät verwendet werden, über das der Standort die Sperre erstellt hat. Wenn Sie versuchen, auf ein gesperrtes Objekt zuzugreifen, können Sie jetzt die Option **Änderungen verwerfen** auswählen und die Bearbeitung des Objekts fortsetzen. Diese Änderungen würden sowieso gelöscht werden, sobald die Sperre aufgehoben wird.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> Anzeigen kürzlich verbundener Konsolen

<!--3699367-->
Ab Version 1902 können Sie die letzten Verbindungen für die Configuration Manager-Konsole abrufen. In der Ansicht finden Sie aktive Verbindungen sowie die Verbindungen, die kürzlich hergestellt wurden. Es werden immer die aktuelle Konsolenverbindung in der Liste und nur die Verbindungen angezeigt, die über die Configuration Manager-Konsole hergestellt wurden. Es werden keine PowerShell oder SDK-basierten Verbindungen mit dem SMS-Anbieter angezeigt. Instanzen, die älter als 30 Tage sind, werden aus der Liste entfernt.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> Voraussetzungen für das Anzeigen von verbundenen Konsolen

- Ihr Konto muss über die **Leseberechtigung** für das Objekt **SMS_Site** verfügen.

- Konfigurieren Sie die REST-API für den Verwaltungsdienst. Weitere Informationen finden Sie unter [Was ist der Verwaltungsdienst?](../../../develop/adminservice/overview.md).

### <a name="view-connected-consoles"></a>Anzeigen von verbundenen Konsolen

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**.  

2. Erweitern Sie **Sicherheit**, und wählen Sie den Knoten **Konsolenverbindungen** aus.  

3. Zeigen Sie die neuesten Verbindungen mit den folgenden Eigenschaften an:  

    - Benutzername
    - Computername
    - Code des verbundenen Standorts
    - Konsolenversion
    - Zeitpunkt der letzten Verbindung: Wann der Benutzer die Konsole zum letzten Mal *geöffnet* hat.
    - In Version 1910 wurde die Spalte **Last Connected Time** (Zeitpunkt der letzten Verbindung) durch die Spalte **Last Console Heartbeat** (Letzter Konsolentakt) ersetzt. <!--4923997-->
       - Eine geöffnete Konsole im Vordergrund sendet alle 10 Minuten einen Takt.

![Anzeigen der Verbindungen mit der Configuration Manager-Konsole](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> Starten eines Microsoft Teams-Chats über Konsolenverbindungen
<!--4923997-->
*(eingeführt in Version 1910)*

Ab Version 1910 können Sie über den Knoten **Konsolenverbindungen** mithilfe von Microsoft Teams Nachrichten an andere Configuration Manager-Administratoren senden. Wenn Sie einen **Microsoft Teams-Chat** mit einem Administrator starten möchten, wird Microsoft Teams gestartet und ein Chat mit dem Benutzer geöffnet.

### <a name="prerequisites"></a>Voraussetzungen

- Um einen Chat mit einem Administrator zu starten, muss das Konto dieses Administrators mit [Azure AD oder der Active Directory-Benutzerermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser) ermittelt worden sein.
- Auf dem Gerät, von dem aus Sie die Konsole ausführen, muss Microsoft Teams installiert sein.
Hinweis:
- [alle Voraussetzungen für das Anzeigen von verbundenen Konsolen](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Starten eines Microsoft Teams-Chats

1. Wechseln Sie zu **Verwaltung** > **Sicherheit** > **Konsolenverbindungen**.
1. Klicken Sie mit der rechten Maustaste auf die Konsolenverbindung eines Benutzers, und wählen Sie **Microsoft Teams-Chat starten** aus.
    - Wenn der Benutzerprinzipalname für den ausgewählten Administrator nicht gefunden wird, ist die Option **Microsoft Teams-Chat starten** abgeblendet.
    - Eine Fehlermeldung einschließlich eines Downloadlinks wird angezeigt, wenn Microsoft Teams nicht auf dem Gerät installiert ist, von dem aus Sie die Konsole ausführen.
    - Wenn Microsoft Teams auf dem Gerät installiert ist, von dem aus Sie die Konsole ausführen, wird ein Chat mit dem Benutzer geöffnet.

### <a name="known-issues"></a>Bekannte Probleme

Die Fehlermeldung, die Sie darüber informiert, dass Microsoft Teams nicht installiert ist, wird nicht angezeigt, wenn der folgende Registrierungsschlüssel nicht vorhanden ist:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Um dieses Problem zu umgehen, erstellen Sie den Registrierungsschlüssel manuell.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a> Configuration Manager-Konsolenbenachrichtigungen

<!--3556016, fka 1318035-->
Ab Configuration Manager Version 1902 benachrichtigt die Konsole Sie bei folgenden Ereignissen:

- Ein Update ist für Configuration Manager selbst verfügbar.
- Lebenszyklus- und Verwaltungsereignisse treten in der Umgebung auf.

Diese Benachrichtigung wird als Leiste am oberen Rand des Konsolenfensters unter dem Menüband dargestellt. Es ersetzt die vorherige Oberfläche, wenn Configuration Manager-Updates verfügbar sind. Diese Benachrichtigungen in der Konsole enthalten wichtige Informationen, beeinträchtigen aber nicht Ihre Arbeit in der Konsole. Sie können kritische Benachrichtigungen nicht verwerfen. Die Konsole zeigt alle Benachrichtigungen in einem neuen Benachrichtigungsbereich der Titelleiste an.

![Benachrichtigungsleiste und -Flag in der Konsole](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Konfigurieren eines Standorts zur Anzeige von nicht kritischen Benachrichtigungen

Sie können die Eigenschaften jedes Standorts so konfigurieren, dass nicht kritische Benachrichtigungen angezeigt werden.

1. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und wählen Sie dann den Knoten **Standorte** aus.
1. Wählen Sie den Standort aus, den Sie für nicht kritische Benachrichtigungen konfigurieren möchten.
1. Wählen Sie im Menüband **Eigenschaften** aus.
1. Wählen Sie auf der Registerkarte **Warnungen** die Option **Konsolenbenachrichtigungen für nicht kritische Integritätsänderungen der Website aktivieren** aus.
   - Wenn Sie diese Einstellung aktivieren, sehen alle Konsolenbenutzer Benachrichtigungen der Typen „Kritisch“, „Warnung“ und „Information“. Diese Einstellung ist standardmäßig aktiviert.  
   - Wenn Sie diese Einstellung deaktivieren, sehen Konsolenbenutzer nur kritische Benachrichtigungen.  

Die meisten Konsolenbenachrichtigungen gelten pro Sitzung. Die Konsole wertet Abfragen aus, wenn sie von einem Benutzer gestartet wird. Wenn Sie Änderungen in den Benachrichtigungen anzeigen möchten, starten Sie die Konsole neu. Verwirft ein Benutzer eine nicht kritische Benachrichtigung, wird sie erneut angezeigt, wenn die Konsole neu gestartet wird und die Benachrichtigung noch immer gültig ist.

Die folgenden Benachrichtigungen werden alle fünf Minuten neu ausgewertet:

- Standort befindet sich im Wartungsmodus  
- Site is in recovery mode (Standort befindet sich im Wiederherstellungsmodus)  
- Site is in upgrade mode (Standort befindet sich im Upgrademodus)  

Benachrichtigungen unterliegen den Berechtigungen der rollenbasierten Verwaltung. Wenn ein Benutzer z. B. nicht über Berechtigungen zum Anzeigen von Configuration Manager-Updates verfügt, werden ihm diese Benachrichtigungen nicht angezeigt.

Einige Benachrichtigungen verfügen über eine zugehörige Aktion. Wenn die Konsolenversion beispielsweise nicht mit der Standortversion übereinstimmt, klicken Sie **Install the new console version** (Neue Konsolenversion installieren). Diese Aktion startet den Konsoleninstaller.

Die folgenden Benachrichtigungen treten häufig im Technical Preview-Branch auf:  

- Evaluation version is within 30 days of expiration (Evaluierungsversion läuft innerhalb von 30 Tagen ab) (Warnung): Die Evaluierungsversion läuft ab dem aktuellen Datum innerhalb von 30 Tagen ab.  
- Evaluation version is expired (Evaluierungsversion ist abgelaufen) (Kritisch): Zum aktuellen Datum liegt das Ablaufdatum bereits in der Vergangenheit.  
- Console version mismatch (Konflikt der Konsolenversionen) (Kritisch): Die Konsolenversion entspricht nicht der Standortversion.  
- Site upgrade is available (Standortupgrade ist verfügbar) (Warnung): Es ist ein neues Updatepaket verfügbar.  

Weitere Informationen und Unterstützung bei der Problembehandlung finden Sie in der Datei **SmsAdminUI.log** auf dem Konsolencomputer. Diese Protokolldatei befindet sich standardmäßig im folgenden Pfad: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> Dashboard für die konsoleninterne Dokumentation

<!--3556019 FKA 1357546-->
Ab Configuration Manager Version 1902 befindet sich im neuen Arbeitsbereich **Community** ein Knoten **Dokumentation**. Dieser Knoten enthält aktuelle Informationen zur Configuration Manager-Dokumentation und Supportartikel. Er enthält folgende Abschnitte:  

### <a name="product-documentation-library"></a>Produktdokumentationsbibliothek

- **Empfohlen**: eine manuell zusammengestellte Liste mit wichtigen Artikeln
- **Trends**: die beliebtesten Artikel im letzten Monat
- **Kürzlich aktualisiert**: im letzten Monat aktualisierte Artikel

### <a name="support-articles"></a>Supportartikel

- **Artikel zur Problembehandlung**: Exemplarische Vorgehensweisen mit Anleitungen, die Ihnen bei der Problembehandlung von Configuration Manager-Komponenten und -Features helfen.
- **Neue und aktualisierte Supportartikel**: Artikel, die neu sind oder in den letzten zwei Monaten aktualisiert wurden.

### <a name="troubleshooting-connection-errors"></a>Beheben von Konnektivitätsproblemen
Der Knoten **Dokumentation** verfügt nicht über eine explizite Proxykonfiguration. Er verwendet einen beliebigen, vom Betriebssystem definierten Proxy im Systemsteuerungsapplet **Internetoptionen**. Um den Vorgang nach einem Verbindungsfehler zu wiederholen, aktualisieren Sie den Knoten **Dokumentation**.


## <a name="command-line-options"></a>Befehlszeilenoptionen

Die Configuration Manager-Konsole verfügt über folgende Befehlszeilenoptionen:

|Option|Beschreibung|  
|------------|-----------------|  
|`/sms:debugview=1`|Eine DebugView-Anwendung wird in alle ResultViews eingeschlossen, die eine Ansicht angeben. DebugView zeigt Basiseigenschaften (Namen und Werte) an.|  
|`/sms:NamespaceView=1`|Zeigt die Namespaceansicht in der Konsole an.|  
|`/sms:ResetSettings`|Die Konsole ignoriert vom Benutzer gespeicherte Verbindungs- und Ansichtszustände. Die Fenstergröße wird nicht zurückgesetzt.|  
|`/sms:IgnoreExtensions`|Deaktiviert alle Configuration Manager-Erweiterungen.|  
|`/sms:NoRestore`|Die Konsole ignoriert die zuletzt gespeicherte Navigation im Knoten.|  


## <a name="tips"></a>Tipps

### <a name="general"></a>Allgemein

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Verbesserungen bei der Konsolensuche
<!--4640570-->
*(eingeführt in Version 1910)*

- Sie können die Suchoption **Alle Unterordner** aus den Knoten **Treiberpakete** und **Abfragen** verwenden.<!--2841181,5424892--> Seit Version 2002 können Sie diese Option auch aus den Knoten **Konfigurationselemente** und **Konfigurationsbaselines** verwenden.<!--5891241-->

- Wenn eine Suche mehr als 1.000 Ergebnisse zurückgibt, wählen Sie die Schaltfläche **OK** in der Hinweisleiste aus, um weitere Ergebnisse anzuzeigen.<!--4640570-->

    ![Screenshot der Hinweisleiste bei zu vielen Suchergebnissen](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Der Standardgrenzwert für Suchergebnisse beträgt 1.000. Sie können diesen Standardwert ändern. Navigieren Sie in der Configuration Manager-Konsole zur Registerkarte **Suchen** des Menübands. Wählen Sie in der Gruppe **Optionen** die Option **Sucheinstellungen** aus. Ändern Sie den Wert für **Suchergebnisse**. Es kann länger dauern, bis eine größere Anzahl von Suchergebnissen angezeigt wird.
    >
    > Standardmäßig sind die obere Maximalgrenze 100.000 Ergebnisse. Um diesen Grenzwert zu ändern, legen Sie den DWORD-Wert **QueryResultCountMaximum** im folgenden Registrierungsschlüssel fest:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > Die konsoleninterne Einstellung entspricht dem Wert **QueryResultCountLimit** im gleichen Schlüssel. Ein Administrator kann diese Werte in der HKLM-Struktur für alle Benutzer des Geräts konfigurieren. Der HKCU-Wert überschreibt die HKLM-Einstellung.

#### <a name="role-based-administration-for-folders"></a>Rollenbasierte Verwaltung für Ordner
<!--3600867-->
*(Eingeführt in Version 1906)*

Sie können Sicherheitsbereiche für Ordner festlegen. Wenn Sie Zugriff auf ein Objekt im Ordner, aber keinen Zugriff auf den Ordner haben, können Sie das Objekt nicht anzeigen. Ebenso wird das Objekt nicht angezeigt, wenn Sie Zugriff auf einen Ordner, jedoch nicht auf ein darin enthaltenes Objekt haben. Klicken Sie mit der rechten Maustaste auf einen Ordner, klicken Sie auf **Sicherheitsbereiche festlegen**, und wählen Sie anschließend die anzuwendenden Sicherheitsbereiche aus.

#### <a name="views-sort-by-integer-values"></a>Sortierung von Ansichten nach ganzzahligen Werten

*(Eingeführt in Version 1902)*

Wir haben die Art und Weise verbessert, in der verschiedene Ansichten Daten sortieren. Beispielsweise werden im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung** die folgenden Spalten jetzt als Zahlen anstatt als Zeichenfolgenwerte sortiert:  

- Fehlerzahl
- Anzahl in Bearbeitung
- Anzahl Sonstige
- Anzahl erfolgreich
- Anzahl unbekannt  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Verschieben der Warnung wegen einer großen Anzahl von Ergebnissen

*(Eingeführt in Version 1902)*

Wenn Sie einen Knoten in der Konsole auswählen, der mehr als 1.000 Ergebnisse zurückgibt, zeigt Configuration Manager folgende Warnung an:

> Configuration Manager hat eine große Menge von Ergebnissen zurückgegeben. Sie können die Ergebnisse mithilfe der Suche eingrenzen. Oder klicken Sie hier, um maximal 100.000 Ergebnisse anzuzeigen.

Zwischen dieser Warnung und dem Suchfeld ist kein zusätzliches Leerzeichen vorhanden. Diese Verschiebung hilft, zu verhindern, dass versehentlich die Warnung zum Anzeigen von mehr Ergebnissen ausgewählt wird.

#### <a name="send-feedback"></a>Senden von Feedback

*(Eingeführt in Version 1806)*
<!--1357542-->

Übermitteln Sie Feedback zum Produkt über die Konsole.  

- **Lächeln senden**: Senden Sie Feedback zu Dingen, die Ihnen gefallen haben.  

- **Stirnrunzeln senden**: Senden Sie Feedback zu Dingen, die Ihnen nicht gefallen haben.  

- **Vorschlag senden**: Leitet Sie zu UserVoice weiter, wo Sie Ihre Ideen teilen können.  

Weitere Informationen finden Sie unter [Produktfeedback](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Arbeitsbereich „Assets und Konformität“

#### <a name="real-time-actions-from-device-lists"></a>Echtzeitaktionen in Gerätelisten
<!--4616810-->
*(Eingeführt in Version 1906)*

Es gibt verschiedene Möglichkeiten, eine Liste von Geräten im Arbeitsbereich **Bestand und Konformität** unter dem Knoten **Geräte** anzuzeigen.

- Wählen Sie im Arbeitsbereich **Bestand und Konformität** den Knoten **Gerätesammlungen** aus. Wählen Sie eine Gerätesammlung und dann die Aktion **Mitglieder anzeigen** aus. Diese Aktion öffnet Unterknoten des Knotens **Geräte** mit der Geräteliste für diese Sammlung.  

  - Wenn Sie den Unterknoten „Sammlung“ auswählen, können Sie auf dem Menüband nun **CMPivot** in der Gruppe „Sammlung“ starten.  

- Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Bereitstellungen**. Wählen Sie eine Bereitstellung aus, und klicken Sie auf dem Menüband auf **Status anzeigen**. Doppelklicken Sie im Bereich „Bereitstellungsstatus“ auf den gesamten Bestand, um zu einer Geräteliste zu gelangen.  

  - Wenn Sie ein Gerät in dieser Liste auswählen, können Sie auf dem Menüband in der Gruppe „Gerät“ **CMPivot** und **Skripts ausführen** starten.  


#### <a name="collections-tab-in-devices-node"></a>Registerkarte „Sammlungen“ im Knoten „Geräte“
<!--4616810-->
*(Eingeführt in Version 1906)*

Wechseln Sie im Arbeitsbereich **Bestand und Konformität** zum Knoten **Geräte**, und wählen Sie ein Gerät aus. Wechseln Sie im Detailbereich zur neuen Registerkarte **Sammlungen**. Auf dieser Registerkarte finden Sie die Sammlungen, zu denen dieses Gerät gehört. 

> [!Note]  
> - Diese Registerkarte ist derzeit nicht in einem Unterknoten „Geräte“ unter dem Knoten **Gerätesammlungen** verfügbar. Beispielsweise, wenn Sie die Option **Mitglieder anzeigen** für eine Sammlung auswählen.
> - Diese Registerkarte wird für einige Benutzer möglicherweise nicht erwartungsgemäß aufgefüllt. Sie müssen die Sicherheitsrolle **Hauptadministrator** haben, um die vollständige Liste der Sammlungen anzuzeigen, zu denen ein Gerät gehört. Dies ist ein bekanntes Problem. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Hinzufügen der SMBIOS GUID-Spalte zu den Knoten „Geräte“ und „Gerätesammlungen“

*(Eingeführt in Version 1906)*

<!--4526580-->
Sowohl im Knoten **Geräte** als auch im Knoten **Gerätesammlungen** können Sie nun eine neue Spalte für **SMBIOS GUID** hinzufügen. Dieser Wert ist identisch mit der **BIOS GUID**-Eigenschaft der Klasse „Systemressource“. Es handelt wich um einen eindeutigen Bezeichner für die Gerätehardware.

#### <a name="search-device-views-using-mac-address"></a>Geräteansichten mithilfe der MAC-Adresse durchsuchen

<!--3600878-->
*(Eingeführt in Version 1902)*

Sie können in einer Geräteansicht der Configuration Manager-Konsole nach einer MAC-Adresse suchen. Diese Eigenschaft ist für Administratoren bei der Betriebssystembereitstellung hilfreich, wenn sie Probleme mit PXE-basierten Bereitstellungen beheben. Fügen Sie zur Ansicht einer Liste von Geräten die Spalte **MAC-Adresse** hinzu. Verwenden Sie das Suchfeld, um die Suchkriterien für die **MAC-Adresse** hinzuzufügen.

#### <a name="view-users-for-a-device"></a>Anzeigen von Benutzern eines Geräts

Ab Version 1806 sind folgende Spalten im Knoten **Geräte** verfügbar:  

- **Primäre(r) Benutzer** <!--1357280-->  

- **Aktuell angemeldeter Benutzer** <!--1358202-->  

    > [!NOTE]  
    > Zur Anzeige des derzeit angemeldeten Benutzers sind [Benutzerermittlung](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) und [Affinität zwischen Benutzer und Gerät](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) erforderlich.  

Weitere Informationen zum Anzeigen einer nicht standardmäßigen Spalte finden Sie unter [Spalten](#columns).

#### <a name="improvement-to-device-search-performance"></a>Verbesserung der Gerätesuchleistung

<!-- 3614690 -->
Ab Version 1806 wird das Stichwort bei der Suche in einer Gerätesammlung nicht in allen Objekteigenschaften gesucht. Wenn Sie nichts Bestimmtes suchen, wird in den folgenden vier Eigenschaften gesucht:

- Name
- Primäre(r) Benutzer
- Aktuell angemeldeter Benutzer
- Benutzername der letzten Anmeldung

Dieses Verhalten verkürzt die Suche nach Namen insbesondere in einer großen Umgebung erheblich. Benutzerdefinierte Suchvorgänge anhand spezifischer Kriterien sind von dieser Änderung nicht betroffen.


### <a name="software-library-workspace"></a>Arbeitsbereich „Softwarebibliothek“

#### <a name="order-by-program-name-in-task-sequence"></a>Sortieren nach Programmname in der Tasksequenz
<!--4616810-->
*(Eingeführt in Version 1906)*

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie den Knoten **Tasksequenzen** aus. Bearbeiten Sie eine Tasksequenz, um anschließend den Schritt [Paket installieren](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) auszuwählen oder hinzuzufügen. Wenn ein Paket mehr als ein Programm enthält, werden die Programme in der Dropdownliste nun alphabetisch sortiert.

#### <a name="task-sequences-tab-in-applications-node"></a>Registerkarte „Tasksequenzen“ im Knoten „Anwendungen“
<!--4616810-->
*(Eingeführt in Version 1906)*

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**. Wechseln Sie dann zum Knoten **Anwendungen**, und wählen Sie eine Anwendung aus. Wechseln Sie im Detailbereich zur neuen Registerkarte **Tasksequenzen**. Diese Registerkarte listet die Tasksequenzen auf, die auf diese Anwendung verweisen.

#### <a name="drill-through-required-updates"></a>Ausführen eines Drillthrough durch erforderliche Updates
<!--4224414-->
*(Eingeführt in Version 1906)*

1. Navigieren Sie in der Configuration Manager-Konsole an eine der folgenden Stellen:

   - **Softwarebibliothek** > **Softwareupdates** > **Alle Softwareupdates**
   - **Softwarebibliothek** > **Windows 10-Wartung** > **Alle Windows 10-Updates**
   - **Softwarebibliothek** > **Office 365-Clientverwaltung** > **Office 365-Updates**

1. Wählen Sie ein beliebiges Update aus, das für mindestens ein Gerät erforderlich ist.
1. Öffnen Sie die Registerkarte **Zusammenfassung**, und sehen Sie sich das Kreisdiagramm unter **Statistiken** an.
1. Klicken Sie auf der rechten Seite neben dem Kreisdiagramm auf den Link **Erforderliche anzeigen**, um einen Drilldown für die Geräteliste auszuführen.
1. Über diese Aktion gelangen Sie unter **Geräte** zu einem temporären Knoten, unter dem die Geräte angezeigt werden, für die das Update erforderlich ist. Außerdem können Sie Aktionen für den Knoten ausführen, z. B. können Sie eine neue Sammlung aus der Liste erstellen.

> [!NOTE]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

#### <a name="maximize-the-browse-registry-window"></a>Maximieren des Fensters zum Durchsuchen der Registrierung

<!--3594151 includes all MMS 1902 console changes-->
*(Eingeführt in Version 1902)*

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**, und wählen Sie dann den Knoten **Anwendungen** aus.
1. Wählen Sie eine Anwendung mit einem Bereitstellungstyp aus, der eine Erkennungsmethode umfasst. Z. B. eine Windows Installer-Erkennungsmethode.
1. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungstypen**.
1. Öffnen Sie die Eigenschaften eines Bereitstellungstyps, und wechseln Sie zu der Registerkarte **Erkennungsmethode**. Wählen Sie **Klausel hinzufügen** aus.
1. Ändern Sie den **Einstellungstyp** in **Registrierung**, und wählen Sie **Durchsuchen** aus, um das Fenster **Registrierung durchsuchen** zu öffnen. Sie können dieses Fenster jetzt maximieren.  

#### <a name="edit-a-task-sequence-by-default"></a>Standardmäßiges Bearbeiten einer Tasksequenz

*(Eingeführt in Version 1902)*

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie den Knoten **Tasksequenzen** aus. **Bearbeiten** ist jetzt die Standardaktion, wenn Sie eine Tasksequenz öffnen. Zuvor war die Standardaktion **Eigenschaften**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Wechseln von einer Anwendungsbereitstellung zu der Sammlung

*(Eingeführt in Version 1902)*

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**, und wählen Sie dann den Knoten **Anwendungen** aus.
1. Wählen Sie eine Anwendung aus. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungen**.
1. Wählen Sie eine Bereitstellung aus, und wählen Sie dann die neue Option **Sammlung** im Menüband auf der Registerkarte „Bereitstellung“ aus. Durch diese Aktion wechselt die Ansicht zu der Sammlung, die das Ziel der Bereitstellung ist.
   - Diese Aktion ist in dieser Ansicht auch im Kontextmenü der Bereitstellung verfügbar.


### <a name="monitoring-workspace"></a>Arbeitsbereich „Überwachung“

#### <a name="correct-names-for-client-operations"></a>Richtige Namen für Clientvorgänge
<!--4616810-->
*(Eingeführt in Version 1906)*

Wählen Sie im Arbeitsbereich **Überwachung** die Option **Clientvorgänge** aus. Der Vorgang **Zum nächsten Softwareupdatepunkt wechseln** ist jetzt ordnungsgemäß benannt.

#### <a name="show-collection-name-for-scripts"></a>Anzeigen des Sammlungsnamen für Skripts
<!--4616810-->
*(Eingeführt in Version 1906)*

Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Skriptstatus**. Er enthält nun zusätzlich zur ID den **Sammlungsnamen**.

#### <a name="remove-content-from-monitoring-status"></a>Entfernen von Inhalten aus der Überwachung des Status

*(Eingeführt in Version 1902)*

1. Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und wählen Sie **Inhaltsstatus** aus.
1. Wählen Sie ein Element in der Liste aus, und wählen Sie die Option **Anzeigestatus** im Menüband aus.
1. Klicken Sie im Bereich „Bestandsdetails“ mit der rechten Maustaste auf einen Verteilungspunkt, und wählen Sie die neue Option **Entfernen** aus. Durch diese Aktion wird dieser Inhalt aus dem ausgewählten Verteilungspunkt entfernt.

#### <a name="copy-details-in-monitoring-views"></a>Kopieren von Details in Überwachungsansichten

*(Eingeführt in Version 1806)*
<!--1357856-->
Informationen können für die folgenden Überwachungsknoten aus dem Bereich **Bestandsdetails** kopiert werden:  

- **Status der Inhaltsverteilung**  

- **Bereitstellungsstatus**  

![Bereitstellungsstatusansicht, Bestandsdetails kopieren](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Arbeitsbereich „Verwaltung“

<!--4223683-->
Ab Version 1906 können Sie für einige Knoten unter dem Knoten **Sicherheit** die Verwendung des Verwaltungsdiensts aktivieren. Diese Änderung ermöglicht der Konsole die Kommunikation mit dem SMS-Anbieter über HTTPS anstatt WMI. Weitere Informationen finden Sie unter [Einrichten des Verwaltungsdiensts](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Nächste Schritte

[Barrierefreiheitsfunktionen](../../understand/accessibility-features.md)

[Tasksequenz-Editor](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
