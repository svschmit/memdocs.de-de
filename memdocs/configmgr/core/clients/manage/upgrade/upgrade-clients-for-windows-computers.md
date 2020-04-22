---
title: Upgraden von Clients unter Windows
titleSuffix: Configuration Manager
description: Upgraden von Clients für Windows-Computer in Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7476f27c050a7870cd8f860f2e1b6bfa3d68a7e9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696288"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Vorgehensweise: Upgraden von Clients für Windows-Computer in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Aktualisieren Sie den Configuration Manager-Client auf Windows-Computern mithilfe von Clientinstallationsmethoden oder den Features für automatisches Clientupgrade. Die folgenden Clientinstallationsmethoden eignen sich für ein Upgrade der Clientsoftware auf Windows-Computern:  

- Gruppenrichtlinieninstallation  

- Anmeldeskriptinstallation  

- Manuelle Installation  

- Upgradeinstallation  

Weitere Informationen finden Sie unter [Gewusst wie: Bereitstellen von Clients für Windows-Computer in Configuration Manager](../../deploy/deploy-clients-to-windows-computers.md).

Schließen Sie Clients vom Upgrade aus, indem Sie eine Ausschlusssammlung angeben. Weitere Informationen finden Sie unter [Ausschließen von Clientupgrades für Windows-Computer in System Center Configuration Manager](exclude-clients-windows.md). Bei ausgeschlossenen Clients wird weiterhin CCMSETUP heruntergeladen und ausgeführt, allerdings kein Upgrade vorgenommen.

> [!TIP]  
> Wenn Sie ein Upgrade Ihrer Serverinfrastruktur von einer früheren Version von Configuration Manager durchführen, führen Sie die Serverupgrades aus, bevor Sie die Configuration Manager-Clients aktualisieren. Dieser Vorgang umfasst die Installation aller Current Branch-Updates. Das neueste Current Branch-Update enthält die neueste Version des Clients. Aktualisieren Sie Clients, nachdem Sie alle Configuration Manager-Updates installiert haben.

> [!NOTE]
> Wenn Sie den Standort für die Clients während des Upgrades neu zuweisen möchten, können Sie den neuen Standort mithilfe der client.msi-Eigenschaft `SMSSITECODE` angeben. Wenn Sie den Wert von `AUTO` für den `SMSSITECODE` verwenden, geben Sie auch `SITEREASSIGN=TRUE` an. Diese Eigenschaft ermöglicht die automatische Neuzuweisung des Standorts während des Upgrades. Weitere Informationen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation in System Center Configuration Manager – SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a> Informationen zum automatischen Clientupgrade

Konfigurieren Sie den Standort für die automatische Aktualisierung der Clients auf die neueste Configuration Manager-Version. Wenn Configuration Manager erkennt, dass die Version eines zugewiesenen Clients älter ist als die Hierarchieversion, wird der Client automatisch aktualisiert. Dieses Szenario umfasst das Upgrade des Clients auf die neueste Version, wenn versucht wird, den Client einem Configuration Manager-Standort zuzuweisen.  

Ein Client kann in den folgenden Szenarien automatisch aktualisiert werden:  

- Die Clientversion ist niedriger als die in der Hierarchie verwendete Version.  

- Auf dem Client am Standort der zentralen Verwaltung (Central Administration Site, CAS) ist ein Sprachpaket installiert, und auf dem vorhandenen Client nicht.  

- Eine erforderliche Clientkomponente in der Hierarchie weist eine andere als die auf dem Client installierte Version auf.  

- Mindestens eine Clientinstallationsdatei liegt in einer anderen Version vor.  

> [!NOTE]  
> Um die verschiedenen in Ihrer Hierarchie vorhandenen Versionen des Configuration Manager-Clients zu ermitteln, können Sie im Berichtsordner **Standort – Clientinformationen** den Bericht **Anzahl von Configuration Manager-Clients nach Clientversionen** ausführen.  

Configuration Manager erstellt standardmäßig ein Upgradepaket. Das Paket wird automatisch an alle Verteilungspunkte in der Hierarchie gesendet. Wenn Sie Änderungen am Client Paket am CAS vornehmen, aktualisiert Configuration Manager das Paket automatisch und verteilt es neu. Ein Beispiel für eine Änderung ist, wenn Sie ein Clientsprachpaket hinzufügen. Wenn Sie das automatische Clientupgrade aktivieren, wird das neue Clientsprachpaket automatisch auf allen Clients installiert.

> [!NOTE]  
> Configuration Manager sendet das Clientupgradepaket nicht automatisch an cloudbasierte Verteilungspunkte von Configuration Manager.  

Aktivieren Sie das automatische Clientupgrade in Ihrer Hierarchie. Diese Konfiguration hält Ihre Clients mit weniger Aufwand auf dem neuesten Stand.  

Wenn Sie Ihre Configuration Manager-Standortsysteme auch als Clients verwalten, legen Sie fest, ob sie in den automatischen Upgradevorgang eingeschlossen werden sollen. Sie können alle Server oder eine bestimmte Sammlung von einem Clientupgrade ausschließen. Einige Configuration Manager-Standortrollen nutzen das Clientframework gemeinsam. Beispielsweise Verwaltungspunkt und Pullverteilungspunkt. Diese Rollen werden aktualisiert, wenn Sie den Standort aktualisieren, sodass die Clientversion auf diesen Servern gleichzeitig aktualisiert wird.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a> Konfigurieren automatischer Clientupgrades

Gehen Sie wie folgt vor, um das automatische Clientupgrade am CAS zu konfigurieren. Diese Konfiguration gilt für alle Clients in der Hierarchie.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Standortkonfiguration**, und klicken Sie dann auf den Knoten **Standorte**.  

1. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

1. Wechseln Sie zur Registerkarte **Clientupdate**. Überprüfen Sie Version und Datum des Produktionsclients. Stellen Sie sicher, dass es sich um die Version handelt, die Sie für ein Upgrade Ihrer Clients verwenden möchten. Wenn es sich nicht um die erwartete Clientversion handelt, müssen Sie den Präproduktionsclient ggf. auf eine Produktionsversion heraufstufen. Weitere Informationen finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung](test-client-upgrades.md).  

1. Wählen Sie die Option **Alle Clients in der Hierarchie mithilfe des Produktionsclients aktualisieren** aus. Wählen Sie zum Bestätigen **OK** aus.  

1. Wenn Sie keine Clientupgrades auf Server anwenden möchten, wählen Sie **Server nicht aktualisieren** aus.  

1. Geben Sie die Anzahl von Tagen an, in denen Geräte das Upgrade des Clients durchführen müssen. Nachdem das Gerät die Richtlinie empfangen hat, wird der Client in einem zufälligen Intervall innerhalb dieser Anzahl von Tagen aktualisiert. Dieses Verhalten verhindert, dass eine große Anzahl von Clients gleichzeitig aktualisiert wird.

    > [!NOTE]
    > Ein Computer muss ausgeführt werden, um den Client upzugraden. Falls ein Computer nicht ausgeführt wird, wenn er wie geplant das Upgrade erhalten soll, wird das Upgrade nicht ausgeführt. Wenn der Computer eingeschaltet ist und Richtlinien empfängt, wird das Upgrade für einen zufälligen Zeitpunkt in der zulässigen Anzahl von Tagen geplant. Tritt dieser Fall nach Ablauf der Anzahl von Tagen ein, wird das Upgrade zu einem zufälligen Zeitpunkt innerhalb von 24 Stunden nach dem Neustart des Computers geplant.
    >
    > Aufgrund dieses Verhaltens dauert das Upgrade von Computern, die regelmäßig heruntergefahren werden, möglicherweise länger als erwartet, wenn die zufällig geplante Upgradezeit nicht in die normale Arbeitszeit fällt.

1. Um Clients vom Upgrade auszuschließen, wählen Sie **Angegebene Clients von Upgrade ausschließen** aus, und geben Sie die auszuschließende Sammlung an. Weitere Informationen finden Sie unter [Ausschließen von Clientupgrades für Windows-Computer in System Center Configuration Manager](exclude-clients-windows.md).

1. Wählen Sie die Option **Installationspakete des Clients automatisch an Verteilungspunkte verteilen, die für vorab bereitgestellten Inhalt aktiviert wurden** aus, wenn der Standort das Clientinstallationspaket auf Verteilungspunkte kopieren soll, die Sie für [vorab bereitgestellten Inhalt](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) aktiviert haben.  

1. Wählen Sie **OK** aus, um die Einstellungen zu speichern und „Eigenschaften von Hierarchieeinstellungen“ zu schließen.

Diese Einstellungen werden beim nächsten Herunterladen einer Richtlinie auf Clients übertragen.

> [!NOTE]
> Bei Clientupgrades werden Configuration Manager-Wartungsfenster berücksichtigt, die Sie konfiguriert haben.

## <a name="next-steps"></a>Nächste Schritte

Alternative Methoden zum Aktualisieren von Clients finden Sie unter [Bereitstellen von Clients auf Windows-Computern](../../deploy/deploy-clients-to-windows-computers.md).

Ausschließen bestimmter Clients von automatischen Upgrades. Weitere Informationen finden Sie unter [Ausschließen von Clientupgrades für Windows-Computer in System Center Configuration Manager](exclude-clients-windows.md).
