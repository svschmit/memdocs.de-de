---
title: Community Hub und GitHub
titleSuffix: Configuration Manager
description: Aktivieren und Verwenden von Community Hub in Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128170"
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


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Direkte Links zu Elementen im Community Hub
<!--4224406-->
*(In Version 2006 eingeführt)* Über einen direkten Link können Sie in der Configuration Manager-Konsole einfach zu Elementen im Knoten „Community Hub“ navigieren und auf sie verweisen. Zweck dieses Features ist es, die Zusammenarbeit zu erleichtern und die Möglichkeit zu schaffen, Links zu Community Hub-Elementen mit Ihren Kollegen zu teilen. Diese Deep Links gelten derzeit nur für Elemente im Knoten „Community Hub“ der Konsole.

### <a name="prerequisites-for-direct-links"></a>Voraussetzungen für direkte Links

- Configuration Manager-Konsole ab Version 2006
- Wenn Sie einem Community Hub-Link folgen, können Sie nicht das lokale integrierte Administratorkonto verwenden.

### <a name="sharing-and-opening-direct-links"></a>Freigeben und Öffnen direkter Links

So geben Sie ein Element frei
1. Wechseln Sie im Hub zum Element, und wählen Sie **Freigeben** aus.
1. Fügen Sie den kopierten Link ein, und geben Sie ihn für andere frei.

So öffnen Sie einen freigegebenen Link
1. Klicken Sie auf einem Computer, auf dem die Configuration Manager-Konsole installiert ist, auf den Link.
   - Über diesen Link können Sie beispielsweise das Skript [Configure Edge Auto Update](https://communityhub.microsoft.com/item/7200) teilen (`https://communityhub.microsoft.com/item/7200`).
1. Wählen Sie nach Aufforderung **Community Hub starten** aus.
1. Die Konsole wird direkt mit dem Skript im Community Hub geöffnet.

## <a name="known-issues"></a><a name="bkmk_known"></a> Bekannte Probleme

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>Beim Ausführen der Konsole als anderer Benutzer kann nicht auf den Knoten „Community Hub“ zugegriffen werden
<!--7826897-->
Wenn Sie als Benutzer mit geringeren Rechten angemeldet sind und **Ausführen als** ein anderer Benutzer wählen, um die Configuration Manager-Konsole zu öffnen, können Sie möglicherweise nicht auf den Knoten **Community Hub** zugreifen.

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>Heruntergeladene Berichte werden nicht von der Seite „Downloads“ entfernt
<!--7851305-->
Wenn Sie einen heruntergeladenen Bericht vom Knoten **Überwachung** > **Berichte** löschen, wird der Bericht nicht von der Seite **Community Hub** > **Ihre Downloads** gelöscht, und es ist nicht möglich, den Bericht erneut herunterzuladen. 

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über das Erstellen und Verwenden der folgenden Objekte:

- [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduction to reporting (Einführung in die Berichterstellung)](introduction-to-reporting.md)
- [Erstellen und Verwalten von Tasksequenzen](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Erstellen und Bereitstellen einer Anwendung](../../../apps/get-started/create-and-deploy-an-application.md)
- [Erstellen von Konfigurationselementen](../../../compliance/deploy-use/create-configuration-items.md)