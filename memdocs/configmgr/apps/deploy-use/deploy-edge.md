---
title: Bereitstellen und Aktualisieren von Microsoft Edge, Version 77 und höher
titleSuffix: Configuration Manager
description: Bereitstellen und Aktualisieren von Microsoft Edge, Version 77 und höher mit Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2c3a542355dfa01e5f4f5be12f7b1bac10f30250
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689518"
---
# <a name="microsoft-edge-management"></a>Microsoft Edge-Verwaltung

*Gilt für: Configuration Manager (Current Branch)*

Die brandneue Version von Microsoft Edge ist einsatzbereit. Ab Configuration Manager, Version 1910, können Sie jetzt [Microsoft Edge, Version 77 und höher](https://docs.microsoft.com/deployedge/), für Ihre Benutzer bereitstellen. Zum Installieren des ausgewählten Microsoft Edge-Builds wird ein PowerShell-Skript verwendet. Das Skript deaktiviert auch automatische Updates für Microsoft Edge, sodass diese mit Configuration Manager verwaltet werden können.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a> Microsoft Edge bereitstellen
<!--4561024-->
Administratoren können den Betakanal (Beta Channel), den Entwicklerkanal (Dev Channel) oder den stabilen Kanal (Stable Channel) sowie eine Version des bereitzustellenden Microsoft Edge-Clients auswählen. Jedes Release umfasst Erkenntnisse und Verbesserungen unserer Kunden und unserer Community.

### <a name="prerequisites-for-deploying"></a>Voraussetzungen für die Bereitstellung

Für Clients, die auf eine Microsoft Edge-Bereitstellung abzielen:

- Die PowerShell-[Ausführungsrichtlinie](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) kann nicht auf „Restricted“ festgelegt werden.
  - PowerShell wird ausgeführt, um die Installation durchzuführen.

Das Gerät, auf dem die Configuration Manager-Konsole ausgeführt wird, benötigt Zugriff auf die folgenden Endpunkte:

|Standort|Verwendung|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Informationen zu Releases von Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Inhalt für Microsoft Edge-Releases|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a> Updaterichtlinien für Microsoft Edge überprüfen

#### <a name="configuration-manager-version-1910"></a>Configuration Manager Version 1910

In Version 1910 schaltet das Installationsskript bei Bereitstellung von Microsoft Edge automatische Updates für Microsoft Edge aus, sodass diese mit Configuration Manager verwaltet werden können. Sie können dieses Verhalten mit dem Tool „Gruppenrichtlinie“ ändern. Weitere Informationen finden Sie unter [Planen Ihrer Bereitstellung von Microsoft Edge](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) und [Microsoft Edge – Update-Richtlinien](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies).

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager, Version 2002 und höher
<!--4561024-->
Ab Version 2002 können Sie eine Microsoft Edge-Anwendung erstellen, die für den Empfang von automatischen Updates eingerichtet ist, anstatt automatische Updates zu deaktivieren. Mit dieser Änderung können Sie Updates für Microsoft Edge mit Configuration Manager verwalten oder automatische Updates durch Microsoft Edge zulassen. Wenn Sie die Anwendung erstellen, wählen Sie auf der Seite **Microsoft Edge-Einstellungen** die Option **Microsoft Edge das automatische Aktualisieren der Clientversion auf dem Gerät des Endbenutzers erlauben** aus. Wenn Sie zuvor eine Gruppenrichtlinie verwendet haben, um dieses Verhalten zu ändern, überschreibt die Gruppenrichtlinie die Einstellung, die während der Installation von Microsoft Edge von Configuration Manager vorgenommen wird.

[![Einstellung für automatisches Microsoft Edge-Update](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Erstellen einer Bereitstellung

Erstellen einer Microsoft Edge-Anwendung mit der integrierten Anwendungsfunktionalität zur einfacheren Microsoft Edge-Verwaltung:

1. In der-Konsole wird unter **Softwarebibliothek** ein neuer Knoten mit dem Namen **Microsoft Edge-Verwaltung** angezeigt.
1. Wählen Sie im Menüband die Option **Microsoft Edge-Anwendung erstellen** aus, oder klicken Sie mit der rechten Maustaste auf den Knoten **Microsoft Edge-Verwaltung**.

   ![Klicken mit der rechten Maustaste auf den Knoten „Microsoft Edge-Verwaltung“](./media/4561024-create-microsoft-edge-application.png)

1. Geben Sie auf der Seite **Anwendungseinstellungen** des Assistenten einen Namen, eine Beschreibung und einen Speicherort für den Inhalt der App an. Stellen Sie sicher, dass der von Ihnen als Inhaltsort angegebene Ordner leer ist.
1. Wählen Sie auf der Seite **Microsoft Edge-Einstellungen** Folgendes aus:
   - Den Kanal für die Bereitstellung
   - Die Version für die Bereitstellung
   - Ob Sie **Microsoft Edge das automatische Aktualisieren der Clientversion auf dem Gerät des Endbenutzers erlauben** möchten (ab Version 2002)
1. Entscheiden Sie auf der Seite **Bereitstellung**, ob Sie die Anwendung bereitstellen möchten. Wenn Sie **Ja**auswählen, können Sie die Bereitstellungseinstellungen für die Anwendung angeben. Weitere Informationen zu Bereitstellungseinstellungen finden Sie unter [Bereitstellungen von Anwendungen](deploy-applications.md#bkmk_deploy-general).
1. Im **Softwarecenter-** auf dem Clientgerät kann der Benutzer die Anwendung anzeigen und installieren.

   ![Seite "Microsoft Edge-Einstellungen" im Bereitstellungs-Assistenten](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Protokolldateien für die Bereitstellung

|Standort|Protokoll|Verwendung|
|---|---|---|
| Standortserver|SMSProv.log|Zeigt Details an, wenn die Erstellung der App oder die Bereitstellung fehlschlägt.|
| [Unterschiedlich](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Zeigt Details an, wenn der Inhaltsdownload fehlschlägt.|
| Client|  AppEnforce.log|Zeigt Installationsinformationen an.|

## <a name="update-microsoft-edge"></a>Aktualisieren von Microsoft Edge
<!--4831871-->

Ab Configuration Manager Version 1910 wird ein Knoten mit der Bezeichnung **Alle Microsoft Edge-Updates** in der **Microsoft Edge-Verwaltung** angezeigt. Dieser Knoten unterstützt Sie bei der Verwaltung von Updates für alle Microsoft Edge-Kanäle.<!--initial edge updates released Jan 15,2020-->

1. Um Updates für Microsoft Edge zu erhalten, stellen Sie sicher, dass die Klassifizierung **Updates** und das Produkt **Microsoft Edge** [zur Synchronisierung ausgewählt ist](../../sum/get-started/configure-classifications-and-products.md).

   [![Auswahl von Microsoft Edge als Produkt in den Softwareupdatepunkteigenschaften](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Knoten **Microsoft Edge-Verwaltung**, und klicken Sie auf den Knoten **Alle Microsoft Edge-Updates**.

1. Klicken Sie bei Bedarf im Menüband auf **Softwareupdates synchronisieren**, um eine Synchronisierung zu starten. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates](../../sum/get-started/synchronize-software-updates.md).

   ![Node für alle Microsoft Edge-Updates](./media/4831871-all-microsoft-edge-updates.png)

1. Verwalten Sie Microsoft Edge-Updates, und stellen Sie diese bereit, so wie bei jedem anderen Update auch. Fügen Sie diese beispielsweise Ihrer [Regel für die automatische Bereitstellung](../../sum/deploy-use/automatically-deploy-software-updates.md) hinzu. Zu den allgemeinen Updatetasks, die Sie über den Knoten **Alle Microsoft Edge-Updates** durchführen können, gehören:

   - [Erstellen einer Bereitstellung in Phasen](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Manuelles Bereitstellen von Softwareupdates](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Herunterladen von Softwareupdates](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Microsoft Edge-Verwaltungsdashboard
<!--3871913-->
*(eingeführt in Version 2002)*

Ab Configuration Manager 2002 bietet das Microsoft Edge-Verwaltungsdashboard Einblicke in die Nutzung von Microsoft Edge und anderen Browsern. Das Dashboard ermöglicht Ihnen Folgendes:

- Sehen, auf wie vielen Ihrer Geräte Microsoft Edge installiert wurde
- Sehen, auf wie vielen Clients verschiedene Versionen von Microsoft Edge installiert sind
   - In diesem Diagramm ist der Canary-Kanal nicht enthalten.
- Anzeigen der installierten Browser auf Geräten
- Anzeigen des bevorzugten Browsers nach Gerät <!--5907383-->
   - Derzeit ist das Diagramm für das Release 2002 leer.

### <a name="prerequisites-for-the-dashboard"></a>Voraussetzungen für das Dashboard

Aktivieren Sie die folgenden Eigenschaften in den unten angegebenen [Hardwareinventur](../../core/clients/manage/inventory/extend-hardware-inventory.md)-Klassen für das Microsoft Edge-Verwaltungsdashboard:

- **Installierte Software: Asset Intelligence (SMS_InstalledSoftware)**
   - Softwarecode
   - Produktname
   - Produktversion

- **Standardbrowser (SMS_DefaultBrowser)**
   - Browserprogramm-ID

- **SMS_BrowserUsage (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>Anzeigen des Dashboards

Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Microsoft Edge-Verwaltung**, um das Dashboard aufzurufen. Ändern Sie die Sammlung für die Graphdaten, indem Sie auf **Durchsuchen** klicken und eine andere Sammlung auswählen. Ihre fünf größten Sammlungen werden automatisch in der Dropdownliste angezeigt. Wenn Sie eine Sammlung auswählen, die nicht in der Liste enthalten ist, wird die neu ausgewählte Sammlung unten in der Dropdownliste angezeigt.

[![Microsoft Edge-Verwaltungsdashboard](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von Anwendungen](monitor-applications-from-the-console.md)

[Überwachen von Softwareupdates](../../sum/deploy-use/monitor-software-updates.md)

[Verwalten und Überwachen von Bereitstellungen in Phasen](../../osd/deploy-use/manage-monitor-phased-deployments.md)
