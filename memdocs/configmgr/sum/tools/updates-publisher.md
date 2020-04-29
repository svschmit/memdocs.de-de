---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Verwenden von System Center Updates Publisher zum Verwalten benutzerdefinierter Updates
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700028"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Gilt für: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) ist ein eigenständiges Tool, mit dem unabhängige Softwarehersteller oder Entwickler branchenspezifischer Anwendungen benutzerdefinierte Updates verwalten können. Diese benutzerdefinierte Updateverwaltung schließt Updates mit Abhängigkeiten ein, z. B. Treiber und Updatepakete.

Mit Updates Publisher können Sie Folgendes ausführen:

-   Importieren von Updates aus externen Katalogen (nicht von Microsoft stammenden Updatekatalogen).
-   Ändern von Updatedefinitionen einschließlich Anwendbarkeit und Bereitstellungsmetadaten.
-   Exportieren von Updates in externe Kataloge.
-   Veröffentlichen von Updates auf einem Updateserver.

Nach der Veröffentlichung von Updates auf einem Updateserver können Sie mit Configuration Manager Updates erkennen und auf Ihren verwalteten Geräten bereitstellen.

## <a name="workspaces"></a>Arbeitsbereiche
Wenn Sie Updates Publisher öffnen, wird standardmäßig der Knoten „Übersicht“ des *Arbeitsbereichs „Updates“* angezeigt.

![Updates Publisher-Konsole](media/console1.png)


Updates Publisher ist in vier Arbeitsbereiche unterteilt.


**Arbeitsbereich „Updates“:** Verwenden Sie diesen Arbeitsbereich, um Softwareupdates und Updatepakete zu [erstellen](create-updates-with-updates-publisher.md) und zu [verwalten](manage-updates-with-updates-publisher.md). Dieser Arbeitsbereich umfasst das Zuweisen von Updates und Paketen zu einer Veröffentlichung, das Veröffentlichen und das Exportieren in ein anderes Update Publisher-Repository.

**Arbeitsbereich „Veröffentlichungen“:** In diesem Arbeitsbereich [verwalten Sie Veröffentlichungen](updates-publisher-publications.md). Eine Veröffentlichung ist eine Gruppe von Updates, die Sie erstellen, um das Exportieren und Veröffentlichen von Updates zu vereinfachen.

Das Verwalten von Veröffentlichungen umfasst das Veröffentlichen von Updates auf einem Server, damit Ihre Clients sie finden und installieren können, das Exportieren von Updates und Paketen für die Verwendung durch andere Updates Publisher-Installationen, oder das Ändern des Inhalts oder von Details einer Veröffentlichung.

**Arbeitsbereich „Regeln“:** Hier [verwalten Sie Anwendbarkeitsregeln](updates-publisher-applicability-rules.md), die gespeichert und anschließend mit Updates verwendet werden können, die Sie bereitstellen. Es gibt zwei Typen von Regeln:

-   „Installierbar“-Regeln – diese Regeln helfen zu bestimmen, ob ein Client ein Update installieren sollte.
-   „Installiert“-Regeln – diese Regeln überprüfen, ob ein Update bereits installiert ist.

**Arbeitsbereich „Kataloge“:** Nutzen Sie diesen Arbeitsbereich zum Hinzufügen und [Verwalten von Softwareupdatekatalogen](updates-publisher-catalogs.md). Dieser Arbeitsbereich schließt den Import von Softwareupdates aus diesen Katalogen in das Updates Publisher-Repository ein.

## <a name="whats-new-in-system-center-updates-publisher"></a>Neues in System Center Updates Publisher

>[!NOTE] 
> Die neueste Version von System Center Updates Publisher wurde am 6. November 2019 veröffentlicht. Weitere Informationen finden Sie im Abschnitt [Releaseverlauf](#release-history).

Es gibt einen neuen Erstellungsmodus in System Center Updates Publisher, der Sie bei der Erstellung Ihrer Updates unterstützt. Wenn Sie den Erstellungsmodus aktivieren, wird dem Startbildschirm der Arbeitsbereich **Kategorien** hinzugefügt. Eine neue **Detectoid**-Schaltfläche wird auch zum Arbeitsbereich **Updates** hinzugefügt, wenn der Erstellungsmodus aktiviert ist.

### <a name="to-enable-authoring-mode"></a>So aktivieren Sie den Erstellungsmodus

1. Klicken Sie in der oberen linken Ecke der Konsole auf die Registerkarte **Eigenschaften** von **Updates Publisher**, und wählen Sie dann **Optionen** aus.
1. Wechseln Sie zu den Optionen für die **Erstellung**.
1. Aktivieren Sie das Kontrollkästchen für **Erstellungsmodus aktivieren**.

![Aktivieren des Erstellungsmodus für Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Informationen zum Arbeitsbereich „Kategorien“

Der Arbeitsbereich „Kategorien“ ermöglicht es Erstellern von Updates, zusammengehörige Updates zu organisieren. Wenn Sie z. B. ein OEM sind, möchten Sie vielleicht Ihre Updates auf der Grundlage von Modellen oder Produktlinien organisieren. Sie können mehrere Kategorien und untergeordnete Kategorien, aber keine untergeordneten Kategorien von Unterkategorien definieren, da Sie auf zwei Ebenen beschränkt sind.

![Screenshot des Arbeitsbereichs „Kategorien“](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Zuweisen eines Updates zu einer Kategorie

Nachdem Sie Ihr Update erstellt haben, können Sie es einer Kategorie zuweisen, indem Sie das Update auswählen und dann auf die Schaltfläche **Kategorisieren** klicken. Sie können auch mit der rechten Maustaste auf das Update klicken und **Kategorisieren** auswählen.

![Screenshot zur Kategorisierung eines Updates](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Informationen zu Detectoids

Sobald der Erstellungsmodus aktiviert ist, können Sie Detectoids für Updates erstellen. Detectoids sind nützlich, wenn Sie über mehrere Updates verfügen, die dieselbe Regel (oder einen Satz von Regeln) verwenden, um die Anwendbarkeit zu ermitteln. In diesen Fällen würden Sie eine Detectoid erstellen und es als Voraussetzung für ein Update zuweisen. Sie können einem erstellten Update mehrere Detectoids zuweisen.


### <a name="create-a-detectoid"></a>Erstellen einer Detectoid

1. Öffnen Sie den Arbeitsbereich **Updates**.
1. Klicken Sie im Menüband auf die Schaltfläche **Detectoid**.
1. Befolgen Sie die Anweisungen im Assistenten, um Ihre Detectoid zu erstellen.



![Aktualisieren der Voraussetzungen mithilfe einer Detectoid](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Releaseverlauf

- [2019 RTW-Version 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Veröffentlicht: 6. November 2019
- [Updaterollup-Version 6.0.283.0 von KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Veröffentlicht: 7. September 2018
- [2017 RTW-Version 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Veröffentlicht: 26. März 2018


## <a name="next-steps"></a>Nächste Schritte
[Installieren](install-updates-publisher.md) Sie zuerst Updates Publisher, und [konfigurieren](updates-publisher-options.md) Sie dann die Optionen.
