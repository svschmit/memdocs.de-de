---
title: Konfigurieren des zwischengespeicherten Inhalts
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Clients Bereitstellungsinhalte für das Betriebssystem herunterladen können, bevor ein Benutzer die Tasksequenz installiert.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 184bdc58ac6dc0e311875cc1ddab8c605d8eec32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704208"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Konfigurieren der in einem vorgeschalteten Cache gespeicherten Inhalte für Tasksequenzen

*Gilt für: Configuration Manager (Current Branch)*

<!--1021244-->
Clients können mithilfe des Features zum Vorabzwischenspeichern für verfügbare Bereitstellungen von Tasksequenzen relevante Inhalte herunterladen, bevor der Benutzer die Tasksequenz installiert. Der Client kann Inhalte für Tasksequenzen, durch die [ein Betriebssystem aktualisiert](create-a-task-sequence-to-upgrade-an-operating-system.md) oder [ein Betriebssystemimage installiert](create-a-task-sequence-to-install-an-operating-system.md) wird, in einem vorgeschalteten Cache speichern.

> [!Note]  
> In Version 1910 wird dieses Feature standardmäßig von Configuration Manager aktiviert. In Version 1906 oder früher aktiviert Configuration Manager dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Beispiel: Alle Benutzer sollen über eine einzige direkte Upgradetasksequenz verfügen, und es stehen viele verschiedene Architekturen und Sprachen zur Verfügung. In Vorgängerversionen startet der Download von Inhalten, wenn der Benutzer eine bereitgestellte Tasksequenz im Softwarecenter herunterlädt. Durch diese Verzögerung verzögert sich auch der Installationsstart. Alle Inhalte, auf die in der Tasksequenz verwiesen wird, werden heruntergeladen. Dieser Inhalt umfasst das Betriebssystem-Upgradepaket für alle Sprachen und Architekturen. Wenn jedes Upgradepaket in etwa eine Größe von 3 GB hat, ist der Gesamtinhalt sehr groß.

Mit dem Vorabzwischenspeichern von Inhalten können Sie den Client dahingehend einschränken, dass er nur die zutreffenden Inhalte und alle anderen referenzierten Inhalte herunterladen darf, wenn er die Bereitstellung empfängt. Wenn der Benutzer im Softwarecenter auf **Installieren** klickt, ist der Inhalt bereit. Die Installation startet sofort, da der Inhalt sich auf dem lokalen Laufwerk befindet.

In Version 1902 von Configuration Manager und früher galt dieses Verhalten nur für das *Betriebssystem-Upgradepaket*. Das Paket ist der Inhalt, für den Sie die entsprechende Architektur oder Sprache angeben. Wenn die Tasksequenz z. B. auch auf mehrere Treiberpakete verweist, lädt der Client sie alle herunter. Die Tasksequenz-Engine wertet die Bedingungen für die Schritte aus, während die Tasksequenz ausgeführt wird, nicht im Voraus. Der Client verwendet die Tags in den Paketeigenschaften, um zu bestimmen, welche Inhalte vorab zwischengespeichert werden sollen.

Ab Version 1906<!--4224642--> Nun können Sie mithilfe der Speicherung in einem vorgeschalteten Cache den Bandbreitenbedarf für die folgenden Arten von Inhalten verringern:

- Betriebssystemupgradepakete
- Betriebssystemimages
- Treiberpakete
- Pakete

## <a name="configure-pre-caching"></a>Konfigurieren der Speicherung in einem vorgeschalteten Cache

Das Konfigurieren des Features für die Speicherung in einem vorgeschalteten Cache besteht aus drei Schritten:

1. [Erstellen und Konfigurieren der Pakete](#bkmk_createpkg)
2. [Erstellen einer Tasksequenz mit bedingten Schritten](#bkmk_createts)
3. [Bereitstellen der Tasksequenz und Aktivierung der Speicherung in einem vorgeschalteten Cache](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a> 1. Erstellen und Konfigurieren der Pakete

Der Client wertet Attribute der Pakete aus, um zu entscheiden, welche Inhalte er zur Speicherung in einem vorgeschalteten Cache herunterlädt.  

#### <a name="os-upgrade-package"></a>Betriebssystem-Upgradepaket

Erstellen Sie [Betriebssystem-Upgradepakete](../get-started/manage-operating-system-upgrade-packages.md) für bestimmte Architekturen und Sprachen. Geben Sie **Architektur** und **Sprache** auf der Registerkarte **Datenquelle** der Eigenschaften an.

#### <a name="os-image"></a>Betriebssystemabbild

Erstellen Sie [Betriebssystemimages](../get-started/manage-operating-system-images.md) für bestimmte Architekturen und Sprachen. Geben Sie **Architektur** und **Sprache** auf der Registerkarte **Datenquelle** der Eigenschaften an.

#### <a name="driver-package"></a>Treiberpaket

Erstellen Sie [Treiberpakete](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) für bestimmte Hardwaremodelle. Geben Sie bei den entsprechenden Eigenschaften in der Registerkarte **Allgemein** das **Modell** an.

Der Client wertet das Modell anhand der Eigenschaft **Name** der WMI-Klasse **Win32_ComputerSystemProduct** aus, um zu ermitteln, welches Treiberpaket im Zuge der vorgeschalteten Zwischenspeicherung heruntergeladen werden soll.

> [!TIP]
> Für die eigentliche Abfrage wird eine `LIKE`-Anweisung mit Platzhaltern verwendet: `select * from win32_computersystemproduct where name like "%yourstring%"`. Wenn Sie beispielsweise `Surface` als Modell angeben, gibt die Abfrage alle Modelle aus, die diese Zeichenfolge enthalten.<!-- 6315551 -->

#### <a name="package"></a>Paket

Erstellen Sie [Pakete](../../apps/deploy-use/packages-and-programs.md) für bestimmte Architekturen und Sprachen. Geben Sie **Architektur** und **Sprache** auf der Registerkarte **Allgemein** der zugehörigen Eigenschaften an.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a> 2. Erstellen einer Tasksequenz

Erstellen Sie eine Tasksequenz mit bedingten Schritten für die verschiedenen Sprachen und Architekturen oder mit verschiedenen Hardwaremodellen für Treiberpakete.

|Content|Schritt|
|---------|---------|
|Betriebssystem-Upgradepaket|[Upgraden des Betriebssystems](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|Betriebssystemabbild|[Betriebssystemimage anwenden](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Treiberpaket|[Treiberpaket anwenden](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Paket|[Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Beispielsweise wird im folgenden Schritt **Betriebssystem aktualisieren** die englische Version verwendet:  

![Der Tasksequenz-Editor zeigt mehrere Upgrade OS-Schritte für ENU, DEU und JPN](../media/precacheproperties2.png)

![Tasksequenz-Editor, Registerkarte „Optionen“, Anzeige der WMI WQL-Abfrage für „Locale“ und „OSArchitecture“](../media/precacheoptions2.png)  

> [!Tip]
> Die folgende WMI-Abfrage wird für ein Betriebssystem mit Englisch (Vereinigte Staaten) und 64-Bit-Architektur empfohlen:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Fügen Sie zuerst die Sprache hinzu, indem Sie die Bedingung für die **Betriebssystemsprache** festlegen. Bearbeiten Sie dann die WMI-Abfrage so, dass sie die Architekturklausel beinhaltet.


### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a> 3. Bereitstellen der Tasksequenz

[Stellen Sie die Tasksequenz bereit](deploy-a-task-sequence.md). Konfigurieren Sie für die Zwischenspeicherungsfunktion die folgenden Einstellungen:  

- Wählen Sie auf der Registerkarte **Allgemein** die Option **Inhalt für diese Tasksequenz vorab herunterladen** aus.  

- Konfigurieren Sie auf der Registerkarte **Bereitstellungseinstellungen** die Tasksequenz als **Verfügbar**.  

- Wählen Sie auf der Registerkarte **Zeitplanung** die derzeit ausgewählte Zeit für die Einstellung **Verfügbarkeitsdatum der Bereitstellung festlegen** aus. Der Client beginnt mit dem Zwischenspeichern des Inhalts zur verfügbaren Zeit der Bereitstellung. Wenn ein Zielclient diese Richtlinie empfängt, liegt der verfügbare Zeitpunkt in der Vergangenheit. Das bedeutet, dass der Download des Zwischenspeichers direkt startet. Wenn der Client diese Richtlinie empfängt, aber der verfügbare Zeitpunkt in der Zukunft liegt, beginnt der Client erst mit dem Zwischenspeichern des Inhalts, wenn dieser Zeitpunkt erreicht wurde.  

- Konfigurieren Sie auf der Registerkarte **Verteilungspunkte** die Einstellungen der **Bereitstellungsoptionen**. Wenn der Inhalt nicht vorab zwischengespeichert wird, bevor ein Benutzer die Installation startet, verwendet der Client diese Einstellungen.  

    > [!Important]  
    > Verwenden Sie für Tasksequenzen, bei denen ein Betriebssystemimage installiert wird, nicht die Bereitstellungsoption **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist**. Wenn die Tasksequenz den Datenträger zurücksetzt, bevor sie das Betriebssystemimage anwendet, entfernt sie den Clientcache. Da der Inhalt nicht mehr vorhanden ist, kann die Tasksequenz nicht ausgeführt werden.<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>Benutzerfreundlichkeit

- Wenn der Client die Bereitstellungsrichtlinie empfängt, startet er nach Ablauf des verfügbaren Zeitpunkts der Bereitstellung mit dem Vorabzwischenspeichern des Inhalts. Dieser Inhalt umfasst alle referenzierten Pakete, jedoch nur das Betriebssystem-Upgradepaket, das den Architektur- und Sprachattributen für das Paket entspricht.  

- Wenn der Client die Bereitstellung für Benutzer verfügbar macht, wird eine Benachrichtigung angezeigt, um Benutzer über die neue Bereitstellung zu informieren. Die Tasksequenz ist jetzt im Softwarecenter sichtbar. Der Benutzer kann zum Softwarecenter navigieren und auf **Installieren** klicken, um die Installation zu starten.  

- Wenn der Client den Inhalt nicht vollständig zwischengespeichert hat, und der Benutzer die Tasksequenz installiert, verwendet der Client die Einstellungen, die Sie auf der Registerkarte **Bereitstellungsoption** der Bereitstellung angegeben haben.  


## <a name="see-also"></a>Weitere Informationen:

- [Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Szenario eines Upgrades von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)
