---
title: Community Hub und GitHub
titleSuffix: Configuration Manager
description: Aktivieren und Verwenden von Community Hub in Configuration Manager
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b812fa3b373d6bd5bd2bebed8b1540ceb7bdd6
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262080"
---
# <a name="community-hub-and-github"></a>Community Hub und GitHub
<!--3555935, 3555936-->

Die IT-Administratorcommunity hat im Laufe der Jahre einen großen Wissensschatz aufgebaut. Anstatt Elemente wie Skripts und Berichte von Grund auf neu zu erfinden, haben wir einen **Configuration Manager-Community Hub** aufgebaut, in dem sich IT-Administratoren austauschen können. Durch die Nutzung der Arbeit anderer können Sie Stunden an Arbeit sparen. Der Community Hub fördert Kreativität, indem er auf der Arbeit anderer aufbaut und andere auf Ihrer Arbeit aufbauen lässt. GitHub hat bereits branchenweite Prozesse und Tools für die gemeinsame Nutzung entwickelt. Jetzt nutzt der Community Hub diese Tools direkt in der Configuration Manager-Konsole als Grundlage für die Weiterentwicklung dieser neuen Community. Für das erste Release werden die Inhalte, die im Community-Hub verfügbar gemacht werden, nur von Microsoft hochgeladen. In Zukunft werden IT-Administratoren in der Lage sein, über ihr eigenes GitHub-Konto selbst Inhalte hochzuladen.

> [!Note]  
> Der Community Hub ist ein optionales cloudbasiertes Feature. Es wurde erstmals im Juni 2020 eingeführt. Informationen dazu, wie Sie den Community Hub abonnieren, finden Sie unter [Optionale Features](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Informationen zum Community Hub

Der Community-Hub unterstützt die folgenden Objekte:

- CMPivot-Abfragen
- Applications
- Tasksequenzen
- Konfigurationselemente
- PowerShell-Skripts
- Berichte

## <a name="prerequisites"></a>Voraussetzungen

- Das Gerät, auf dem die Configuration Manager-Konsole für den Zugriff auf den Community Hub ausgeführt wird, benötigt folgende Komponenten:
   - .NET Framework Version 4.6 oder höher
   - Windows 10, Build 17110 oder höher
      - Windows Server wird nicht unterstützt, weshalb die Configuration Manager-Konsole auf einem vom Standortserver getrennten Gerät mit Windows 10 installiert werden muss.
   - Das angemeldete Benutzerkonto darf nicht das integrierte Administratorkonto sein.

- Der [Verwaltungsdienst](../../../develop/adminservice/set-up.md) in Configuration Manager muss eingerichtet und funktionsfähig sein.

- Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, müssen Sie der Configuration Manager-Konsole Zugriff auf Endpunkte im Internet gestatten. Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../plan-design/network/internet-endpoints.md#community-hub).

## <a name="permissions"></a>Berechtigungen

- Importieren eines Skripts: Berechtigung **Erstellen** für die Klasse **SMS_Scripts**
- Importieren eines Berichts: Sicherheitsrolle „Hauptadministrator“


## <a name="use-the-community-hub"></a>Verwenden des Community Hubs

1. Gehen Sie im Arbeitsbereich **Community** zum Hub **Community**.
1. Wählen Sie ein Element zum Herunterladen aus.
1. Sie benötigen entsprechende Berechtigungen an Ihrem Configuration Manager-Standort, um Objekte vom Hub herunterzuladen und in den Standort zu importieren.
    - Importieren eines Skripts: Berechtigung **Erstellen** für die Klasse „SMS_Scripts“
    - Importieren eines Berichts: Sicherheitsrolle „Hauptadministrator“
1. Heruntergeladene Berichte werden in einem Berichtordner mit dem Namen **hub** auf dem Reporting Services-Punkt bereitgestellt. Heruntergeladene Skripts finden Sie im Knoten **Skripts ausführen**.
1. Zeigen Sie alle Elemente an, die von Ihrer Organisation aus dem Hub heruntergeladen wurden, indem Sie im **Community Hub**-Knoten auf **Ihre Downloads** klicken.

[![Alle Elemente, die vom Community-Hub heruntergeladen werden](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über das Erstellen und Verwenden der folgenden Objekte:

- [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduction to reporting (Einführung in die Berichterstellung)](introduction-to-reporting.md)
- [Erstellen und Verwalten von Tasksequenzen](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Erstellen und Bereitstellen einer Anwendung](../../../apps/get-started/create-and-deploy-an-application.md)
- [Erstellen von Konfigurationselementen](../../../compliance/deploy-use/create-configuration-items.md)