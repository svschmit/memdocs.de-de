---
title: Benutzerleitfaden für Softwarecenter
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu Features und Funktionen des Softwarecenters.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706808"
---
# <a name="software-center-user-guide"></a>Benutzerleitfaden für Softwarecenter

*Gilt für: Configuration Manager (Current Branch)*

Mit dem Softwarecenter installiert der IT-Administrator Ihrer Organisation Anwendungen und Softwareupdates und führt Upgrades für Windows durch. In diesem Benutzerleitfaden werden die Softwarecenter-Funktionen für Benutzer des Computers beschrieben.

Allgemeine Hinweise zu Softwarecenter-Funktionen:

- In diesem Artikel werden die neuesten Softwarecenter-Features beschrieben. Wenn Ihre Organisation eine ältere Softwarecenter-Version verwendet, die immer noch unterstützt wird, sind nicht alle Features verfügbar. Weitere Informationen erhalten Sie von Ihrem IT-Administrator.

- Ihr IT-Administrator deaktiviert möglicherweise einige Softwarecenter-Funktionen. Das Anwendungsverhalten kann daher je nach Einstellungen variieren.

- Wenn mehrere Benutzer ein Gerät gleichzeitig verwenden, z. B. über mehrere Remotedesktopsitzungen, wird der Benutzer mit der niedrigsten Sitzungs-ID der einzige sein, dem alle verfügbaren Bereitstellungen im Softwarecenter angezeigt werden. Benutzern mit höheren Sitzungs-IDs werde einige der Bereitstellungen im Softwarecenter möglicherweise nicht angezeigt. Den Benutzern mit höheren Sitzungs-IDs werden z. B. zwar bereitgestellte Anwendungen, nicht aber bereitgestellte Pakete oder Tasksequenzen angezeigt. In der Zwischenzeit werden dem Benutzer mit der niedrigsten Sitzungs-ID alle bereitgestellten Anwendungen, Pakete und Tasksequenzen angezeigt.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Öffnen des Softwarecenters

Das Softwarecenter können Sie auf einem Windows 10-Computer besonders einfach starten, indem Sie auf **Start** klicken und `Software Center` eingeben. Sie müssen möglicherweise nicht die gesamte Zeichenfolge für Windows eingeben, um das gewünschte Ergebnis anzuzeigen.

Alternativ können Sie auch über das Startmenü in der Menübandgruppe **Microsoft Endpoint Manager** nach dem **Softwarecenter**-Symbol suchen.

![Symbole für Microsoft Endpoint Manager im Startmenü](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Der Startmenüpfad wurde in Version 1910 geändert. In Version 1906 und früher lautet der Ordnername **Microsoft System Center**. Wenn Sie Configuration Manager auf Version 1910 oder höher aktualisieren, müssen Sie sicherstellen, dass Sie jede interne Dokumentation aktualisieren, die Sie beibehalten, um diesen neuen Speicherort einzuschließen.

## <a name="applications"></a>Applications

Klicken Sie auf die Registerkarte **Anwendungen** zum Suchen und Installieren von Anwendungen, die Ihr IT-Administrator für Sie oder auf diesem Computer bereitstellt.

- **Alle:** Hierdurch werden alle Anwendungen angezeigt, die Sie installieren können.
- **Erforderlich**: Hierdurch werden alle Anwendungen angezeigt, deren Verwendung vom IT-Administrator erzwungen wird. Wenn Sie eine dieser Anwendungen deinstallieren, installiert das Softwarecenter sie erneut.
- **Filter:** Ihr IT-Administrator kann Kategorien für Anwendungen erstellen. Falls Kategorien verfügbar sind, können Sie durch Auswählen der Dropdownliste die Ansicht so filtern, dass nur Anwendungen einer bestimmten Kategorie angezeigt werden. Klicken Sie auf **Alle**, um sich alle Anwendungen anzeigen zu lassen.
- **Sortieren nach:** Hierdurch wird die Liste der Anwendungen neu geordnet. Standardmäßig wird als Sortieroption **Zuletzt verwendet** festgelegt. Seit Kurzem verfügbare Anwendungen werden mit der Markierung **Neu** aufgeführt, die für sieben Tage angezeigt wird.
- **Suchen:** Können Sie bestimmte Elemente nicht finden? können Sie im Suchfeld Stichwörter eingeben, um nach den Elementen suchen.
- **Ansicht wechseln**: Wählen Sie zum Wechseln zwischen Listenansicht und Kachelansicht die jeweiligen Symbole aus. Die Standardansicht für die Anwendungsliste ist die Kachelansicht.
    - Kachelansicht: Ihr IT-Administrator kann die Symbole anpassen. Unter der Kachel befinden sich der Anwendungsname, der Herausgeber und die Version.
    - Listenansicht: In dieser Ansicht werden das Anwendungssymbol, der Name, der Herausgeber, die Version und der Status angezeigt.

### <a name="install-multiple-applications"></a>Mehrere Anwendungen installieren

<!-- 1357126 -->
Sie können mehrere Anwendungen gleichzeitig installieren und müssen nicht auf den Abschluss einer Installation warten, bevor Sie mit der nächsten fortfahren. Dies ist allerdings nur bei Anwendungen möglich, für die die folgenden Voraussetzungen erfüllt sind:

- Die App wird Ihnen angezeigt.
- Die App wurde noch nicht heruntergeladen und ist noch nicht installiert.
- Ihr IT-Administrator benötigt keine Genehmigung zur Installation der App.

Gehen Sie folgendermaßen vor, um mehrere Anwendungen gleichzeitig zu installieren:

1. Wählen Sie das Mehrfachauswahlsymbol aus, um den Mehrfachauswahlmodus in der Listenansicht zu nutzen. ![Mehrfachauswahlsymbol im Softwarecenter](media/software-center-multi-select-apps.png) in der oberen rechten Ecke.
2. Wählen Sie mindestens zwei Apps aus, die installiert werden müssen, indem Sie das Kontrollkästchen links neben den Apps in der Liste aktivieren.
3. Wählen Sie die Schaltfläche **Install Selected** (Auswahl installieren) aus.

Die Apps werden wie gewöhnlich installiert, allerdings nacheinander.


## <a name="updates"></a>Updates

Wählen Sie die Registerkarte **Updates** aus, um sich Softwareupdates anzeigen zu lassen, die Ihr IT-Administrator auf diesem Computer bereitgestellt hat.  

- **Alle:** Hierdurch werden alle Updates angezeigt, die Sie installieren können.
- **Erforderlich**: Hierdurch werden alle Updates angezeigt, deren Installation vom IT-Administrator erzwungen wird.
- **Sortieren nach:** Hierdurch wird die Liste der Updates neu geordnet. Die Standardsortieroption für diese Liste ist **Anwendungsname: A bis Z**.

Wählen Sie zum Installieren von Updates die Option **Alle installieren** aus.

Wenn Sie nur bestimmte Updates installieren möchten, wählen Sie das Symbol aus, um den Mehrfachauswahlmodus zu nutzen. Überprüfen Sie die Updates, die installiert werden sollen, und wählen Sie anschließend **Auswahl installieren** aus.


## <a name="operating-systems"></a>Betriebssysteme

Wählen Sie die Registerkarte **Betriebssysteme** aus, um Windows-Versionen anzeigen zu lassen und zu installieren, die Ihr IT-Administrator auf diesem Computer bereitgestellt hat.  

- **Alle:** Hierdurch werden alle Windows-Versionen angezeigt, die Sie installieren können.
- **Erforderlich**: Hierdurch werden alle Upgrades angezeigt, deren Installation vom IT-Administrator erzwungen wird.
- **Sortieren nach:** Hierdurch wird die Liste der Updates neu geordnet. Die Standardsortieroption für diese Liste ist **Anwendungsname: A bis Z**.


## <a name="installation-status"></a>Installationsstatus

Wählen Sie die Registerkarte **Installationsstatus** aus, um sich den Status von Anwendungen anzeigen zu lassen. Folgende Status können angezeigt werden:

- **Installiert:** Diese Anwendung wurde bereits vom Softwarecenter auf diesem Computer installiert.
- **Der Downloadvorgang wird ausgeführt:** Die Software, die auf diesem Computer installiert werden soll, wird derzeit vom Softwarecenter heruntergeladen.
- **Fehlgeschlagen:** Das Softwarecenter hat bei der Softwareinstallation einen Fehler erkannt.
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

- Wählen Sie aus den jeweiligen Dropdownlisten die früheste und späteste Uhrzeit aus, zu der Sie diesen Computer verwenden. Die Standardwerte sind **5:00** und **22:00**.

- Aktivieren Sie die Kontrollkästchen neben den Wochentagen, um festzulegen, wann Sie diesen Computer üblicherweise verwenden. Standardmäßig werden von Softwarecenter nur die Kontrollkästchen für Werktage aktiviert.  

Geben Sie an, ob Sie diesen Computer regelmäßig für Ihre Arbeit nutzen. Ihr Administrator installiert möglicherweise automatisch Anwendungen auf primären Computern oder stellt primären Computern zusätzliche Anwendungen zur Verfügung. <!--3485366-->

- Wählen Sie **Ich verwende diesen Computer regelmäßig für meine Arbeit**, wenn der von Ihnen verwendete Computer ein primärer Computer ist.

### <a name="power-management"></a>Energieverwaltung

Ihr IT-Administrator kann Richtlinien zur Energieverwaltung festlegen. Diese unterstützen Ihre Organisation dabei, Strom zu sparen, wenn dieser Computer nicht verwendet wird.

Aktivieren Sie das Kontrollkästchen neben **Do not apply power settings from my IT department to this computer** (Energieeinstellungen meiner IT-Abteilung nicht auf diesen Computer anwenden), wenn dieser Computer von der Richtlinie ausgenommen werden soll. Diese Einstellung ist standardmäßig deaktiviert, und vom Computer werden die Energieeinstellungen verwendet.

### <a name="computer-maintenance"></a>Computerwartung

Geben Sie an, wie Änderungen an der Software vor Ablauf der Frist vom Softwarecenter übernommen werden sollen.

- **Automatically install or uninstall required software and restart the computer only outside of the specified business hours** (Erforderliche Software ausschließlich außerhalb der angegebenen Geschäftszeiten automatisch installieren oder deinstallieren und den Computer neu starten): Diese Einstellung ist standardmäßig deaktiviert.
- **Suspend Software Center activities when my computer is in presentation mode** (Softwarecenter-Aktivitäten anhalten, wenn sich der Computer im Präsentationsmodus befindet): Diese Einstellung ist standardmäßig aktiviert.
- **Sync Policy** (Synchronisierungsrichtlinie): Wählen Sie diese Schaltfläche nur aus, wenn Sie von Ihrem IT-Administrator dazu aufgefordert werden. Dieser Computer überprüft mit einer Serverabfrage, ob neue Anwendungen, Softwareupdates oder Betriebssysteme verfügbar sind.

### <a name="remote-control"></a>Remotesteuerung

Angeben von Einstellungen für Remotezugriff und Remotesteuerung für Ihren Computer

- **Remotezugriffseinstellungen von Ihrer IT-Abteilung verwenden**: Dieses Kontrollkästchen ist standardmäßig aktiviert.
- **Zugelassene Remotezugriffsstufe**: Wählen Sie eine der folgenden drei Optionen aus:
    - **Remotezugriff nicht zulassen**
    - **Nur anzeigen**
    - **Vollständig**: Diese Stufe ist standardmäßig aktiviert.
- **Remotesteuerung dieses Computers durch Administratoren zulassen, wenn ich abwesend bin**. Diese Einstellung ist standardmäßig auf **Ja** festgelegt.
- **Wenn ein Administrator versucht, diesen Computer remote zu steuern**: Diese Einstellung verfügt über zwei Optionen:
    - **Jedes Mal nach Berechtigung fragen**: Diese Option ist standardmäßig ausgewählt.
    - **Keine Berechtigung anfordern**
- **Während der Remotesteuerung Folgendes anzeigen**: Beide Optionen sind standardmäßig aktiviert.
    - **Statussymbol im Benachrichtigungsbereich**
    - **Sitzungsverbindungsleiste auf dem Desktop**
- **Sound wiedergeben**: Diese Einstellung verfügt über drei Optionen:
    - **Bei Start und Ende der Sitzung**: Standardmäßig ist diese Einstellung aktiviert.
    - **Wiederholt während der Sitzung**
    - **Nie**

    Weitere Informationen finden Sie unter [Einführung in die Remotesteuerung](../clients/manage/remote-control/introduction-to-remote-control.md).
    

## <a name="custom-tab-in-software-center"></a>Registerkarte „Benutzerdefiniert“ im Softwarecenter

Möglicherweise hat Ihr IT-Administrator eine zusätzliche Registerkarte im Softwarecenter hinzugefügt. Diese Registerkarte wird von Ihrem Administrator benannt, und führt zu einer von ihm angegebenen Website. Es kann sich z.B. um eine Registerkarte mit dem Namen „Helpdesk“ handeln, die zur Helpdesk-Website Ihres Unternehmens führt. <!--1358132-->
