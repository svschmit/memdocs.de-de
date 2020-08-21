---
title: Änderungen an der Configuration Manager-Konsole und Tipps zu ihrer Nutzung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Änderungen an der Configuration Manager-Konsole und Tipps zu ihrer Nutzung.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0a434f013da48d660efa78f5e2cdca6ced0826d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700717"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Änderungen an der Configuration Manager-Konsole und Tipps zu ihrer Nutzung

*Gilt für: Configuration Manager (Current Branch)*

Nachstehend erfahren Sie mehr zu Änderungen an der Configuration Manager-Konsole und Tipps zu ihrer Nutzung:

## <a name="general-tips"></a>Allgemeine Tipps

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Verbesserungen bei der Konsolensuche
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

### <a name="role-based-administration-for-folders"></a>Rollenbasierte Verwaltung für Ordner
<!--3600867-->
*(Eingeführt in Version 1906)*

Sie können Sicherheitsbereiche für Ordner festlegen. Wenn Sie Zugriff auf ein Objekt im Ordner, aber keinen Zugriff auf den Ordner haben, können Sie das Objekt nicht anzeigen. Ebenso wird das Objekt nicht angezeigt, wenn Sie Zugriff auf einen Ordner, jedoch nicht auf ein darin enthaltenes Objekt haben. Klicken Sie mit der rechten Maustaste auf einen Ordner, klicken Sie auf **Sicherheitsbereiche festlegen**, und wählen Sie anschließend die anzuwendenden Sicherheitsbereiche aus.

### <a name="views-sort-by-integer-values"></a>Sortierung von Ansichten nach ganzzahligen Werten

*(Eingeführt in Version 1902)*

Wir haben die Art und Weise verbessert, in der verschiedene Ansichten Daten sortieren. Beispielsweise werden im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung** die folgenden Spalten jetzt als Zahlen anstatt als Zeichenfolgenwerte sortiert:  

- Fehlerzahl
- Anzahl in Bearbeitung
- Anzahl Sonstige
- Anzahl erfolgreich
- Anzahl unbekannt  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Verschieben der Warnung wegen einer großen Anzahl von Ergebnissen

*(Eingeführt in Version 1902)*

Wenn Sie einen Knoten in der Konsole auswählen, der mehr als 1.000 Ergebnisse zurückgibt, zeigt Configuration Manager folgende Warnung an:

> Configuration Manager hat eine große Menge von Ergebnissen zurückgegeben. Sie können die Ergebnisse mithilfe der Suche eingrenzen. Oder klicken Sie hier, um maximal 100.000 Ergebnisse anzuzeigen.

Zwischen dieser Warnung und dem Suchfeld ist kein zusätzliches Leerzeichen vorhanden. Diese Verschiebung hilft, zu verhindern, dass versehentlich die Warnung zum Anzeigen von mehr Ergebnissen ausgewählt wird.

### <a name="send-feedback"></a>Senden von Feedback

*(Eingeführt in Version 1806)*
<!--1357542-->

Übermitteln Sie Feedback zum Produkt über die Konsole.  

- **Lächeln senden**: Senden Sie Feedback zu Dingen, die Ihnen gefallen haben.  

- **Stirnrunzeln senden**: Senden Sie Feedback zu Dingen, die Ihnen nicht gefallen haben.  

- **Vorschlag senden**: Leitet Sie zu UserVoice weiter, wo Sie Ihre Ideen teilen können.  

Weitere Informationen finden Sie unter [Produktfeedback](../../understand/find-help.md#BKMK_1806Feedback).


## <a name="assets-and-compliance-workspace"></a>Arbeitsbereich „Assets und Konformität“

### <a name="real-time-actions-from-device-lists"></a>Echtzeitaktionen in Gerätelisten
<!--4616810-->
*(Eingeführt in Version 1906)*

Es gibt verschiedene Möglichkeiten, eine Liste von Geräten im Arbeitsbereich **Bestand und Konformität** unter dem Knoten **Geräte** anzuzeigen.

- Wählen Sie im Arbeitsbereich **Bestand und Konformität** den Knoten **Gerätesammlungen** aus. Wählen Sie eine Gerätesammlung und dann die Aktion **Mitglieder anzeigen** aus. Diese Aktion öffnet Unterknoten des Knotens **Geräte** mit der Geräteliste für diese Sammlung.  

  - Wenn Sie den Unterknoten „Sammlung“ auswählen, können Sie auf dem Menüband nun **CMPivot** in der Gruppe „Sammlung“ starten.  

- Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Bereitstellungen**. Wählen Sie eine Bereitstellung aus, und klicken Sie auf dem Menüband auf **Status anzeigen**. Doppelklicken Sie im Bereich „Bereitstellungsstatus“ auf den gesamten Bestand, um zu einer Geräteliste zu gelangen.  

  - Wenn Sie ein Gerät in dieser Liste auswählen, können Sie auf dem Menüband in der Gruppe „Gerät“ **CMPivot** und **Skripts ausführen** starten.  


### <a name="collections-tab-in-devices-node"></a>Registerkarte „Sammlungen“ im Knoten „Geräte“
<!--4616810-->
*(Eingeführt in Version 1906)*

Wechseln Sie im Arbeitsbereich **Bestand und Konformität** zum Knoten **Geräte**, und wählen Sie ein Gerät aus. Wechseln Sie im Detailbereich zur neuen Registerkarte **Sammlungen**. Auf dieser Registerkarte finden Sie die Sammlungen, zu denen dieses Gerät gehört. 

> [!Note]  
> - Diese Registerkarte ist derzeit nicht in einem Unterknoten „Geräte“ unter dem Knoten **Gerätesammlungen** verfügbar. Beispielsweise, wenn Sie die Option **Mitglieder anzeigen** für eine Sammlung auswählen.
> - Diese Registerkarte wird für einige Benutzer möglicherweise nicht erwartungsgemäß aufgefüllt. Sie müssen die Sicherheitsrolle **Hauptadministrator** haben, um die vollständige Liste der Sammlungen anzuzeigen, zu denen ein Gerät gehört. Dies ist ein bekanntes Problem. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Hinzufügen der SMBIOS GUID-Spalte zu den Knoten „Geräte“ und „Gerätesammlungen“

*(Eingeführt in Version 1906)*

<!--4526580-->
Sowohl im Knoten **Geräte** als auch im Knoten **Gerätesammlungen** können Sie nun eine neue Spalte für **SMBIOS GUID** hinzufügen. Dieser Wert ist identisch mit der **BIOS GUID**-Eigenschaft der Klasse „Systemressource“. Es handelt wich um einen eindeutigen Bezeichner für die Gerätehardware.

### <a name="search-device-views-using-mac-address"></a>Geräteansichten mithilfe der MAC-Adresse durchsuchen

<!--3600878-->
*(Eingeführt in Version 1902)*

Sie können in einer Geräteansicht der Configuration Manager-Konsole nach einer MAC-Adresse suchen. Diese Eigenschaft ist für Administratoren bei der Betriebssystembereitstellung hilfreich, wenn sie Probleme mit PXE-basierten Bereitstellungen beheben. Fügen Sie zur Ansicht einer Liste von Geräten die Spalte **MAC-Adresse** hinzu. Verwenden Sie das Suchfeld, um die Suchkriterien für die **MAC-Adresse** hinzuzufügen.

### <a name="view-users-for-a-device"></a>Anzeigen von Benutzern eines Geräts

Ab Version 1806 sind folgende Spalten im Knoten **Geräte** verfügbar:  

- **Primäre(r) Benutzer** <!--1357280-->  

- **Aktuell angemeldeter Benutzer** <!--1358202-->  

    > [!NOTE]  
    > Zur Anzeige des derzeit angemeldeten Benutzers sind [Benutzerermittlung](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) und [Affinität zwischen Benutzer und Gerät](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) erforderlich.  

Weitere Informationen zum Anzeigen einer nicht standardmäßigen Spalte finden Sie unter [Verwenden der Configuration Manager-Konsole](admin-console.md#columns) im Abschnitt „Spalten“.

### <a name="improvement-to-device-search-performance"></a>Verbesserung der Gerätesuchleistung

<!-- 3614690 -->
Ab Version 1806 wird das Stichwort bei der Suche in einer Gerätesammlung nicht in allen Objekteigenschaften gesucht. Wenn Sie nichts Bestimmtes suchen, wird in den folgenden vier Eigenschaften gesucht:

- Name
- Primäre(r) Benutzer
- Aktuell angemeldeter Benutzer
- Benutzername der letzten Anmeldung

Dieses Verhalten verkürzt die Suche nach Namen insbesondere in einer großen Umgebung erheblich. Benutzerdefinierte Suchvorgänge anhand spezifischer Kriterien sind von dieser Änderung nicht betroffen.


## <a name="software-library-workspace"></a>Arbeitsbereich „Softwarebibliothek“

### <a name="order-by-program-name-in-task-sequence"></a>Sortieren nach Programmname in der Tasksequenz
<!--4616810-->
*(Eingeführt in Version 1906)*

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie den Knoten **Tasksequenzen** aus. Bearbeiten Sie eine Tasksequenz, um anschließend den Schritt [Paket installieren](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) auszuwählen oder hinzuzufügen. Wenn ein Paket mehr als ein Programm enthält, werden die Programme in der Dropdownliste nun alphabetisch sortiert.

### <a name="task-sequences-tab-in-applications-node"></a>Registerkarte „Tasksequenzen“ im Knoten „Anwendungen“
<!--4616810-->
*(Eingeführt in Version 1906)*

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**. Wechseln Sie dann zum Knoten **Anwendungen**, und wählen Sie eine Anwendung aus. Wechseln Sie im Detailbereich zur neuen Registerkarte **Tasksequenzen**. Diese Registerkarte listet die Tasksequenzen auf, die auf diese Anwendung verweisen.

### <a name="drill-through-required-updates"></a>Ausführen eines Drillthrough durch erforderliche Updates
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
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

### <a name="maximize-the-browse-registry-window"></a>Maximieren des Fensters zum Durchsuchen der Registrierung

<!--3594151 includes all MMS 1902 console changes-->
*(Eingeführt in Version 1902)*

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**, und wählen Sie dann den Knoten **Anwendungen** aus.
1. Wählen Sie eine Anwendung mit einem Bereitstellungstyp aus, der eine Erkennungsmethode umfasst. Z. B. eine Windows Installer-Erkennungsmethode.
1. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungstypen**.
1. Öffnen Sie die Eigenschaften eines Bereitstellungstyps, und wechseln Sie zu der Registerkarte **Erkennungsmethode**. Wählen Sie **Klausel hinzufügen** aus.
1. Ändern Sie den **Einstellungstyp** in **Registrierung**, und wählen Sie **Durchsuchen** aus, um das Fenster **Registrierung durchsuchen** zu öffnen. Sie können dieses Fenster jetzt maximieren.  

### <a name="edit-a-task-sequence-by-default"></a>Standardmäßiges Bearbeiten einer Tasksequenz

*(Eingeführt in Version 1902)*

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie den Knoten **Tasksequenzen** aus. **Bearbeiten** ist jetzt die Standardaktion, wenn Sie eine Tasksequenz öffnen. Zuvor war die Standardaktion **Eigenschaften**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Wechseln von einer Anwendungsbereitstellung zu der Sammlung

*(Eingeführt in Version 1902)*

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**, und wählen Sie dann den Knoten **Anwendungen** aus.
1. Wählen Sie eine Anwendung aus. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungen**.
1. Wählen Sie eine Bereitstellung aus, und wählen Sie dann die neue Option **Sammlung** im Menüband auf der Registerkarte „Bereitstellung“ aus. Durch diese Aktion wechselt die Ansicht zu der Sammlung, die das Ziel der Bereitstellung ist.
   - Diese Aktion ist in dieser Ansicht auch im Kontextmenü der Bereitstellung verfügbar.


## <a name="monitoring-workspace"></a>Arbeitsbereich „Überwachung“

### <a name="correct-names-for-client-operations"></a>Richtige Namen für Clientvorgänge
<!--4616810-->
*(Eingeführt in Version 1906)*

Wählen Sie im Arbeitsbereich **Überwachung** die Option **Clientvorgänge** aus. Der Vorgang **Zum nächsten Softwareupdatepunkt wechseln** ist jetzt ordnungsgemäß benannt.

### <a name="show-collection-name-for-scripts"></a>Anzeigen des Sammlungsnamen für Skripts
<!--4616810-->
*(Eingeführt in Version 1906)*

Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Skriptstatus**. Er enthält nun zusätzlich zur ID den **Sammlungsnamen**.

### <a name="remove-content-from-monitoring-status"></a>Entfernen von Inhalten aus der Überwachung des Status

*(Eingeführt in Version 1902)*

1. Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und wählen Sie **Inhaltsstatus** aus.
1. Wählen Sie ein Element in der Liste aus, und wählen Sie die Option **Anzeigestatus** im Menüband aus.
1. Klicken Sie im Bereich „Bestandsdetails“ mit der rechten Maustaste auf einen Verteilungspunkt, und wählen Sie die neue Option **Entfernen** aus. Durch diese Aktion wird dieser Inhalt aus dem ausgewählten Verteilungspunkt entfernt.

### <a name="copy-details-in-monitoring-views"></a>Kopieren von Details in Überwachungsansichten

*(Eingeführt in Version 1806)*
<!--1357856-->
Informationen können für die folgenden Überwachungsknoten aus dem Bereich **Bestandsdetails** kopiert werden:  

- **Status der Inhaltsverteilung**  

- **Bereitstellungsstatus**  

![Bereitstellungsstatusansicht, Bestandsdetails kopieren](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Arbeitsbereich „Verwaltung“

<!--4223683-->
Ab Version 1906 können Sie für einige Knoten unter dem Knoten **Sicherheit** die Verwendung des Verwaltungsdiensts aktivieren. Diese Änderung ermöglicht der Konsole die Kommunikation mit dem SMS-Anbieter über HTTPS anstatt WMI. Weitere Informationen finden Sie unter [Einrichten des Verwaltungsdiensts](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Nächste Schritte

- [Verwendung der Konsole](admin-console.md)
- [Konsolenbenachrichtigungen](admin-console-notifications.md)
- [Barrierefreiheitsfunktionen](../../understand/accessibility-features.md)