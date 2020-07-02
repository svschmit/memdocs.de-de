---
title: Benutzerleitfaden für Softwarecenter
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu Features und Funktionen des Softwarecenters.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715448"
---
# <a name="software-center-user-guide"></a>Benutzerleitfaden für Softwarecenter

*Gilt für: Configuration Manager (Current Branch)*

Mit dem Softwarecenter installiert der IT-Administrator Ihrer Organisation Anwendungen und Softwareupdates und führt Upgrades für Windows durch. In diesem Benutzerleitfaden werden die Softwarecenter-Funktionen für Benutzer des Computers beschrieben.

Das Softwarecenter wird automatisch auf Windows-Geräten installiert, die von Ihrer IT-Organisation verwaltet werden. Informationen zu den ersten Schritten finden Sie unter [Öffnen des Softwarecenters](#bkmk_open).

Allgemeine Hinweise zu Softwarecenter-Funktionen:

- In diesem Artikel werden die neuesten Softwarecenter-Features beschrieben. Wenn Ihre Organisation eine ältere Softwarecenter-Version verwendet, die immer noch unterstützt wird, sind nicht alle Features verfügbar. Weitere Informationen erhalten Sie von Ihrem IT-Administrator.

- Ihr IT-Administrator deaktiviert möglicherweise einige Softwarecenter-Funktionen. Das Anwendungsverhalten kann daher je nach Einstellungen variieren.

- Wenn mehrere Benutzer ein Gerät gleichzeitig verwenden, wird der Benutzer mit der niedrigsten Sitzungs-ID der einzige sein, dem alle verfügbaren Bereitstellungen im Softwarecenter angezeigt werden. Beispielsweise mehrere Benutzer in einer Remotedesktopumgebung. Benutzern mit höheren Sitzungs-IDs werde einige der Bereitstellungen im Softwarecenter möglicherweise nicht angezeigt. Den Benutzern mit höheren Sitzungs-IDs werden z. B. zwar bereitgestellte Anwendungen, nicht aber bereitgestellte Pakete oder Tasksequenzen angezeigt. In der Zwischenzeit werden dem Benutzer mit der niedrigsten Sitzungs-ID alle bereitgestellten Anwendungen, Pakete und Tasksequenzen angezeigt. Auf der Registerkarte **Benutzer** des Windows Task Managers werden alle Benutzer und ihre Sitzungs-IDs angezeigt.

- Ihr IT-Administrator kann die Farbe des Softwarecenters ändern und das Logo Ihrer Organisation hinzufügen.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Öffnen des Softwarecenters

Das Softwarecenter wird automatisch auf Windows-Geräten installiert, die von Ihrer IT-Organisation verwaltet werden. Das Softwarecenter können Sie auf einem Windows 10-Computer besonders einfach starten, indem Sie auf **Start** klicken und `Software Center` eingeben. Sie müssen möglicherweise nicht die gesamte Zeichenfolge für Windows eingeben, um das gewünschte Ergebnis anzuzeigen.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Softwarecenter: Gewünschtes Ergebnis im Startmenü":::

Suchen Sie zur Navigation über das Startmenü in der Menübandgruppe **Microsoft Endpoint Manager** nach dem **Softwarecenter**-Symbol.

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Symbole für Microsoft Endpoint Manager im Startmenü":::

> [!NOTE]
> Der obige Startmenüpfad ist für Versionen ab November 2019 (Version 1910) oder höher vorgesehen. In früheren Versionen lautet der Ordnername **Microsoft System Center**.

Wenn Sie das Softwarecenter nicht im Startmenü finden, wenden Sie sich an Ihren IT-Administrator.

## <a name="applications"></a>Applications

:::image type="content" source="media/software-center-apps.png" alt-text="Softwarecenter-Registerkarte „Anwendungen“" lightbox="media/software-center-apps.png":::

Wählen Sie die Registerkarte **Anwendungen** (1) zum Suchen und Installieren von Anwendungen, die Ihr IT-Administrator für Sie oder auf diesem Computer bereitstellt.

- **Alle** (2): Hierdurch werden alle verfügbaren Anwendungen angezeigt, die Sie installieren können.

- **Erforderlich** (3): Hierdurch werden alle Anwendungen angezeigt, deren Verwendung vom IT-Administrator erzwungen wird. Wenn Sie eine dieser Anwendungen deinstallieren, installiert das Softwarecenter sie erneut.

- **Filter** (4): Ihr IT-Administrator kann Kategorien für Anwendungen erstellen. Falls Kategorien verfügbar sind, können Sie durch Auswählen der Dropdownliste die Ansicht so filtern, dass nur Anwendungen einer bestimmten Kategorie angezeigt werden. Klicken Sie auf **Alle**, um sich alle Anwendungen anzeigen zu lassen.

- **Sortieren nach** (5): Hierdurch wird die Liste der Anwendungen neu geordnet. Standardmäßig wird als Sortieroption **Zuletzt verwendet** festgelegt. Kürzlich verfügbare Anwendungen werden mit einem **Neu**-Banner angezeigt, das sieben Tage lang sichtbar ist.

- **Suche** (6): Können Sie bestimmte Elemente nicht finden? können Sie im Suchfeld Stichwörter eingeben, um nach den Elementen suchen.

- Ansicht wechseln (7): Wählen Sie zum Wechseln zwischen Listenansicht und Kachelansicht die jeweiligen Symbole aus. Die Standardansicht für die Anwendungsliste ist die Kachelansicht.

|Symbol|Anzeigen|Beschreibung|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Mehrfachauswahlmodus**|Installieren Sie mehrere Anwendungen gleichzeitig. Weitere Informationen finden Sie unter [Mehrere Anwendungen installieren](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**Listenansicht**|In dieser Ansicht werden das Anwendungssymbol, der Name, der Herausgeber, die Version und der Status angezeigt.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Kachelansicht**|Ihr IT-Administrator kann die Symbole anpassen. Unter der Kachel befinden sich der Anwendungsname, der Herausgeber und die Version.|

### <a name="install-an-application"></a>Installieren einer Anwendung

Wählen Sie eine Anwendung aus der Liste aus, um weitere Informationen dazu anzuzeigen. Wählen Sie **Installieren**, um sie zu installieren. Wenn eine App bereits installiert ist, können Sie möglicherweise die Option zum **Deinstallieren** nutzen.

Die Installation einiger Apps setzt möglicherweise eine Genehmigung voraus.

- Wenn Sie versuchen, sie zu installieren, können Sie einen Kommentar und dann eine **Anforderung** der App eingeben.

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Softwarecenter: Anforderung der Genehmigung für die App-Installation":::

- Das Softwarecenter zeigt den Anforderungsverlauf an, und Sie können die Anforderung abbrechen.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Softwarecenter: App-Installation angefordert":::

- Wenn ein Administrator die Anforderung genehmigt, können Sie die App installieren. Wenn Sie warten, wird die App vom Softwarecenter automatisch außerhalb der Geschäftszeiten installiert.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Softwarecenter: App-Installation genehmigt":::

### <a name="install-multiple-applications"></a>Mehrere Anwendungen installieren

<!-- 1357126 -->
Sie können mehrere Anwendungen gleichzeitig installieren und müssen nicht auf den Abschluss einer Installation warten, bevor Sie mit der nächsten fortfahren. Die ausgewählten Apps müssen qualifiziert werden:

- Die App wird Ihnen angezeigt.
- Die App wurde noch nicht heruntergeladen und ist noch nicht installiert.
- Ihr IT-Administrator benötigt keine Genehmigung zur Installation der App.

Gehen Sie folgendermaßen vor, um mehrere Anwendungen gleichzeitig zu installieren:

1. Wählen Sie in der oberen rechten Ecke das Mehrfachauswahlsymbol aus: :::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. Wählen Sie mindestens zwei Apps zur Installation aus. Aktivieren Sie das Kontrollkästchen links neben jeder App in der Liste.

3. Wählen Sie die Schaltfläche **Auswahl installieren** aus.

Die Apps werden wie gewöhnlich installiert, allerdings nacheinander.

### <a name="share-an-application"></a>Freigeben einer Anwendung

Wenn Sie einen Link zu einer bestimmten App freigeben möchten, wählen Sie nach der Auswahl der App das Symbol **Freigabe** in der oberen rechten Ecke aus: :::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Teilen einer App aus dem Softwarecenter":::

**Kopieren** Sie die Zeichenfolge, und fügen Sie sie an anderer Stelle ein, z. B. in eine E-Mail. Beispiel: `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`. Alle anderen Personen in Ihrer Organisation, die das Softwarecenter nutzen, können mit dem Link dieselbe Anwendung öffnen.

## <a name="updates"></a>Updates

:::image type="content" source="media/software-center-updates.png" alt-text="Softwarecenter-Registerkarte „Updates“" lightbox="media/software-center-updates.png":::

Wählen Sie die Registerkarte **Updates** (1) aus, um sich Softwareupdates anzeigen zu lassen, die Ihr IT-Administrator auf diesem Computer bereitgestellt hat.  

- **Alle** (2): Hierdurch werden alle Updates angezeigt, die Sie installieren können.

- **Erforderlich** (3): Hierdurch werden alle Updates angezeigt, deren Installation vom IT-Administrator erzwungen wird.

- **Sortieren nach** (4): Hierdurch wird die Liste der Updates neu geordnet. Die Standardsortieroption für diese Liste ist **Anwendungsname: A bis Z**.

- **Suche** (5): Können Sie bestimmte Elemente nicht finden? können Sie im Suchfeld Stichwörter eingeben, um nach den Elementen suchen.

Wählen Sie zum Installieren von Updates die Option **Alle installieren** (6) aus.

Wenn Sie nur bestimmte Updates installieren möchten, wählen Sie das Symbol aus, um den Mehrfachauswahlmodus zu nutzen (7): :::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Überprüfen Sie die Updates, die installiert werden sollen, und wählen Sie anschließend **Auswahl installieren** aus.

## <a name="operating-systems"></a>Betriebssysteme

:::image type="content" source="media/software-center-os.png" alt-text="Softwarecenter-Registerkarte „Betriebssysteme“" lightbox="media/software-center-os.png":::

Wählen Sie die Registerkarte **Betriebssysteme** (1) aus, um Windows-Versionen anzeigen zu lassen und zu installieren, die Ihr IT-Administrator auf diesem Computer bereitgestellt hat.  

- **Alle** (2): Hierdurch werden alle Windows-Versionen angezeigt, die Sie installieren können.

- **Erforderlich** (3): Hierdurch werden alle Upgrades angezeigt, deren Installation vom IT-Administrator erzwungen wird.

- **Sortieren nach** (4): Hierdurch wird die Liste der Updates neu geordnet. Die Standardsortieroption für diese Liste ist **Anwendungsname: A bis Z**.

- **Suche** (5): Können Sie bestimmte Elemente nicht finden? können Sie im Suchfeld Stichwörter eingeben, um nach den Elementen suchen.

## <a name="installation-status"></a>Installationsstatus

Wählen Sie die Registerkarte **Installationsstatus** aus, um sich den Status von Anwendungen anzeigen zu lassen. Folgende Status können angezeigt werden:

- **Installiert:** Diese Anwendung wurde bereits vom Softwarecenter auf diesem Computer installiert.

- **Der Downloadvorgang wird ausgeführt:** Die Software, die auf diesem Computer installiert werden soll, wird derzeit vom Softwarecenter heruntergeladen.

- **Fehlgeschlagen:** Das Softwarecenter konnte die Software nicht installieren.

- **Scheduled to install after** (Geplante Installation nach): Zeigt Datum und Uhrzeit des nächsten Wartungsfensters des Geräts an, an dem anstehende Software installiert wird. Wartungsfenster werden von Ihrem IT-Administrator definiert.<!--1358131-->

  - Der Status wird auf den Registerkarten **Alle** und **Anstehend** angezeigt.

  - Sie können schon vor dem geplanten Wartungsfenster die Schaltfläche **Jetzt installieren** auswählen.

## <a name="device-compliance"></a>Gerätekonformität

Wählen Sie die Registerkarte **Gerätekonformität** aus, um sich den Konformitätsstatus dieses Computers anzeigen zu lassen.

Wählen Sie **Konformität überprüfen** aus, um die Einstellungen dieses Geräts mit den Sicherheitsrichtlinien abzugleichen, die von Ihrem IT-Administrator definiert wurden.

## <a name="options"></a>Optionen

Wählen Sie die Registerkarte **Optionen** aus, um sich zusätzliche Einstellungen für diesen Computer anzeigen zu lassen.

### <a name="work-information"></a>Arbeitsinformationen

Geben Sie Ihre üblichen Arbeitszeiten an. Ihr IT-Administrator kann Softwareinstallationen so planen, dass diese außerhalb der Geschäftszeiten durchgeführt werden. Legen Sie die Zeiten so fest, dass für Systemwartungsaufgaben mindestens vier Stunden täglich zur Verfügung stehen. Ihr IT-Administrator kann allerdings wichtige Anwendungen und Softwareupdates auch während der Geschäftszeiten installieren.

- Wählen Sie die früheste und späteste Uhrzeit aus, zu der Sie diesen Computer verwenden. Die Standardwerte sind **5:00** und **22:00**.

- Wählen Sie die Wochentage aus, um festzulegen, wann Sie diesen Computer üblicherweise verwenden. Standardmäßig werden vom Softwarecenter nur die Kontrollkästchen für Werktage aktiviert.

Geben Sie an, ob Sie diesen Computer regelmäßig für Ihre Arbeit nutzen. Ihr Administrator installiert möglicherweise automatisch Anwendungen auf primären Computern oder stellt primären Computern zusätzliche Anwendungen zur Verfügung.<!--3485366--> Wenn der von Ihnen verwendete Computer ein primärer Computer ist, wählen Sie **Ich verwende diesen Computer regelmäßig für meine Arbeit**.

### <a name="power-management"></a>Energieverwaltung

Ihr IT-Administrator kann Richtlinien zur Energieverwaltung festlegen. Diese unterstützen Ihre Organisation dabei, Strom zu sparen, wenn dieser Computer nicht verwendet wird.

Wenn dieser Computer von diesen Richtlinien ausgenommen werden soll, wählen Sie **Energieeinstellungen meiner IT-Abteilung nicht auf diesen Computer anwenden**. Diese Einstellung ist standardmäßig deaktiviert, und vom Computer werden die Energieeinstellungen verwendet.

### <a name="computer-maintenance"></a>Computerwartung

Geben Sie an, wie Änderungen an der Software vor Ablauf der Frist vom Softwarecenter übernommen werden sollen.

- **Automatically install or uninstall required software and restart the computer only outside of the specified business hours** (Erforderliche Software ausschließlich außerhalb der angegebenen Geschäftszeiten automatisch installieren oder deinstallieren und den Computer neu starten): Diese Einstellung ist standardmäßig deaktiviert.

- **Suspend Software Center activities when my computer is in presentation mode** (Softwarecenter-Aktivitäten anhalten, wenn sich der Computer im Präsentationsmodus befindet): Diese Einstellung ist standardmäßig aktiviert.

Wenn Sie von Ihrem IT-Administrator dazu aufgefordert werden, wählen Sie **Synchronisierungsrichtlinie**. Dieser Computer überprüft mit einer Serverabfrage, ob neue Anwendungen, Softwareupdates oder Betriebssysteme verfügbar sind.

### <a name="remote-control"></a>Remotesteuerung

Geben Sie Einstellungen für Remotezugriff und Remotesteuerung für Ihren Computer an.

**Remotezugriffseinstellungen von Ihrer IT-Abteilung verwenden**: Standardmäßig definiert Ihre IT-Abteilung die Einstellungen für Ihren Remotezugriff. Die anderen Einstellungen in diesem Abschnitt zeigen den Status der Einstellungen an, die Ihre IT-Abteilung definiert. Um Einstellungen zu ändern, deaktivieren Sie zuerst diese Option.

- **Zugelassene Remotezugriffsstufe**
  - **Remotezugriff nicht zulassen**: IT-Administratoren können nicht remote auf diesen Computer zugreifen, um Ihnen zu helfen.
  - **Nur anzeigen**: Ein IT-Administrator kann Ihren Bildschirm nur remote anzeigen.
  - **Vollständig**: Ein IT-Administrator kann diesen Computer remote steuern. Dies ist die Standardeinstellung.

- **Remotesteuerung dieses Computers durch Administratoren zulassen, wenn ich abwesend bin**. Diese Einstellung ist standardmäßig auf **Ja** festgelegt.

- **Wenn ein Administrator versucht, diesen Computer remote zu steuern**
  - **Jedes Mal nach Berechtigung fragen**: Dies ist die Standardeinstellung.
  - **Keine Berechtigung anfordern**

- **Während der Remotesteuerung Folgendes anzeigen**: Diese visuellen Benachrichtigungen sind standardmäßig aktiviert, um Sie darüber zu informieren, dass ein Administrator remote auf das Gerät zugreift.
  - **Statussymbol im Benachrichtigungsbereich**
  - **Sitzungsverbindungsleiste auf dem Desktop**

- **Sound wiedergeben**: Diese akustische Benachrichtigung informiert Sie darüber, dass ein Administrator remote auf das Gerät zugreift.
  - **Bei Start und Ende der Sitzung**: Dies ist die Standardeinstellung.
  - **Wiederholt während der Sitzung**
  - **Nie**

## <a name="custom-tabs"></a>Benutzerdefinierte Registerkarten

Der IT-Administrator kann die Standardregisterkarten entfernen oder dem Softwarecenter zusätzliche Registerkarten hinzufügen. Benutzerdefinierte Registerkarten werden von Ihrem Administrator benannt und öffnen eine Website, die der Administrator angibt. Es kann sich z. B. um eine Registerkarte mit dem Namen „Helpdesk“ handeln, die die Helpdesk-Website Ihrer IT-Organisation öffnet. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>Weitere Informationen für IT-Administratoren

Weitere Informationen zum Planen und Konfigurieren des Softwarecenters für IT-Administratoren finden Sie in den folgenden Artikeln:

- [Planen für Software Center](../../apps/plan-design/plan-for-software-center.md)
- [Clienteinstellungen für das Softwarecenter](../clients/deploy/about-client-settings.md#software-center)
- [Benachrichtigungen zum Geräteneustart](../clients/deploy/device-restart-notifications.md)
- [Einführung in die Remotesteuerung](../clients/manage/remote-control/introduction-to-remote-control.md)
