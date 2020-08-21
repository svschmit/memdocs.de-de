---
title: Configuration Manager-Konsole
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zur Navigation durch die Configuration Manager-Konsole.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126493"
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


## <a name="next-steps"></a>Nächste Schritte

- [Konsolenbenachrichtigungen](admin-console-notifications.md)
- [Tipps für die Konsole](admin-console-tips.md)
- [Barrierefreiheitsfunktionen](../../understand/accessibility-features.md)
- [Tasksequenz-Editor](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
