---
title: Verwenden von Wartungsfenstern
titleSuffix: Configuration Manager
description: Verwenden Sie Sammlungen und Wartungsfenster zur effektiven Veraltung von Clients in Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428545"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Verwenden von Wartungsfenstern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Wartungsfenster, um festzulegen, wann Configuration Manager Tasks ausführen kann, die sich auf Geräte auswirken. Mithilfe von Wartungsfenstern können Sie sicherstellen, dass Konfigurationsänderungen für Clients zu Zeiten vorgenommen werden, in denen die Produktivität nicht beeinträchtigt wird. Das nächste Wartungsfenster eines Geräts wird im Softwarecenter auf der Registerkarte **Installationsstatus** angezeigt. <!--1358131-->

Bei den folgenden Tasks werden Wartungsfenster unterstützt:

- Anwendungs- und Paketbereitstellung

- Softwareupdatebereitstellungen

- Bereitstellen und Bewerten von Kompatibilitätseinstellungen

- Betriebssystem- und benutzerdefinierte Tasksequenzbereitstellungen

Konfigurieren Sie Wartungsfenster mit einem Gültigkeitsdatum, einer Start- und Endzeit sowie einem Wiederholungsmuster. Die maximale Dauer eines Fensters muss weniger als 24 Stunden betragen. Die Konsole lässt keine einzelnen Wartungsfenster zu, die länger als 24 Stunden dauern. Wenn Sie z. B. ein Wartungsfenster zulassen möchten, das sich über den gesamten Samstag und Sonntag erstreckt, müssen Sie zwei Wartungsfenster mit einer Dauer von jeweils 24 Stunden erstellen.<!-- MEMDocs#310 -->

In der Standardeinstellung sind Computerneustarts durch Bereitstellungen außerhalb von Wartungsfenstern nicht zulässig. Sie können die Standardeinstellung jedoch außer Kraft setzen. Wartungsfenster wirken sich lediglich auf den Zeitpunkt aus, an dem die Bereitstellung ausgeführt wird. Bei Bereitstellungen, bei denen Inhalte heruntergeladen und lokal ausgeführt werden, können die Inhalte außerhalb des Wartungsfensters heruntergeladen werden.

Wenn ein Client Mitglied einer Gerätesammlung mit Wartungsfenster ist, wird eine Bereitstellung nur dann ausgeführt, wenn die maximal zulässige Laufzeit nicht die Dauer des Fensters überschreitet. Wenn die Bereitstellung nicht ausgeführt werden kann, generiert der Client eine Warnung. Anschließend wird die Bereitstellung während des nächsten geplanten Fensters mit ausreichend Zeit erneut ausgeführt.

## <a name="multiple-maintenance-windows"></a>Mehrere Wartungsfenster

Wenn ein Clientcomputer Mitglied mehrerer Gerätesammlungen mit Wartungsfenstern ist, gelten die folgenden Regeln:  

- Wenn sich die Wartungsfenster nicht überschneiden, behandelt der Client sie als zwei unabhängige Wartungsfenster.

- Wenn sich die Wartungsfenster überschneiden, behandelt der Client sie für die gesamte Dauer beider Fenster als ein einzelnes Fenster. Beispiel: Sie erstellen zwei Wartungsfenster für eine Sammlung. Das erste Fenster beginnt um 6:00 Uhr und endet um 7:00 Uhr, das zweite beginnt um 6:30 Uhr und endet um 7:30 Uhr. Aufgrund der 30-minütigen Überscheidung beträgt die Dauer des kombinierten Wartungsfensters 90 Minuten (von 6:00 Uhr bis 7:30 Uhr).

Wenn ein Benutzer eine Anwendung über das Softwarecenter installiert, wird die Anwendung umgehend vom Client gestartet. Dabei hat die Absicht des Benutzers Vorrang vor der Absicht des Administrators.

Wenn für eine Anwendungsbereitstellung mit der Einstellung **Erforderlich** die Installationsfrist außerhalb der Geschäftszeiten erreicht wird, die ein Benutzer im Softwarecenter konfiguriert, installiert der Client die Anwendung. Die Absicht des Administrators hat Vorrang vor der Absicht des Benutzers.

Wenn mehrere Wartungsfenster vorhanden sind, werden Softwareupdates vom Client standardmäßig nur in Fenstern vom Typ **Softwareupdate** installiert. Wartungsfenster vom Typ **Alle Bereitstellungen** werden ignoriert, sofern sie nicht die einzigen Wartungsfenster sind. Sie können dieses Verhalten über die folgende Clienteinstellung in der Gruppe **Softwareupdates** konfigurieren: **Installation von Softwareupdates im Wartungsfenster „Alle Bereitstellungen“ aktivieren, wenn das Wartungsfenster „Softwareupdate“ verfügbar ist**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs#1317 -->

> [!NOTE]
> Diese Einstellung gilt auch für Wartungsfenster, die Sie so konfigurieren, dass sie auf **Tasksequenzen** angewendet werden.<!-- SCCMDocs-pr #4596 -->
>
> Wenn für den Client nur ein Fenster **Alle Bereitstellungen** verfügbar ist, werden Softwareupdates oder Tasksequenzen weiterhin in diesem Fenster installiert.

## <a name="configure-maintenance-windows"></a>Konfigurieren von Wartungsfenstern

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**.

1. Wählen Sie den Knoten **Gerätesammlungen** und anschließend eine Sammlung aus.

    > [!NOTE]
    > Es können keine Wartungsfenster für die Sammlung **Alle Systeme** erstellt werden.

1. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.

1. Wechseln Sie zur Registerkarte **Wartungsfenster**, und wählen Sie das Symbol **Neu** aus.

    1. Legen Sie in **Name** einen eindeutigen Namen für das Wartungsfenster dieser Sammlung fest.

    1. Konfigurieren Sie die Einstellungen für die **Zeit**:

        - **Gültig ab**: Das Startdatum des Wartungsfensters. Als Standardeinstellung wird das aktuelle Datum festgelegt.

        - **Start** und **Ende**: Die Start- und die Endzeit des Wartungsfensters. Anhand dieser Einstellung wird die **Dauer** des Wartungsfensters berechnet. Die Mindestdauer beträgt fünf Minuten, die maximale Dauer 24 Stunden. Die Standarddauer beträgt drei Stunden, von 01:00 Uhr bis 04:00 Uhr.

        - **Universal Coordinated Time (UTC)** : Aktivieren Sie diese Option, damit der Client die UTC-Zeitzone für die Start- und Endzeit verwendet. Wenn eine Sammlung regional oder global verteilte Geräte umfasst, wird das Wartungsfenster so festgelegt, dass es für alle Geräte innerhalb der Sammlung gleichzeitig stattfindet. Deaktivieren Sie diese Option, wenn der Client die lokale Zeitzone des Geräts verwenden soll. Diese Option ist standardmäßig deaktiviert.

    1. Konfigurieren Sie das Wiederholungsmuster. Als Standardeinstellung ist eine einwöchige Wiederholung am aktuellen Wochentag festgelegt.

    1. **Diesen Zeitplan anwenden auf**: Das Fenster gilt standardmäßig für **Alle Bereitstellungen**. Sie können **Softwareupdates** oder **Tasksequenzen** auswählen, um festzulegen, welche Bereitstellungen in diesem Fenster ausgeführt werden.

        > [!TIP]
        > Wenn Sie mehrere Wartungsfenster unterschiedlicher Typen für eine Sammlung konfigurieren, sollten Sie mit dem Verhalten der Clients vertraut sein. Weitere Informationen finden Sie unter [Mehrere Wartungsfenster](#multiple-maintenance-windows).

1. Wählen Sie **OK** aus, um Ihre Einstellungen zu speichern und das Fenster zu schließen.

In den Sammlungseigenschaften werden auf der Registerkarte **Wartungsfenster** alle konfigurierten Fenster angezeigt.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a> Verwenden von PowerShell

PowerShell kann zum Konfigurieren von Wartungsfenstern verwendet werden. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)
