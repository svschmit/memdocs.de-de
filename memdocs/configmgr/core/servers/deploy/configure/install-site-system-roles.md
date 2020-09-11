---
title: Installieren von Standortsystemrollen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Standortsystemrollen zu einem vorhandenen oder neuen Standortsystemserver am Standort hinzufügen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8cb16b6fd703142e0c3c6400403207976b4208f5
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607570"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Installieren von Standortsystemrollen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In der Configuration Manager-Konsole gibt es zwei Methoden zum Installieren von Standortsystemrollen:

- **Hinzufügen von Standortsystemrollen:** Fügen Sie Standortsystemrollen zu einem vorhandenen Standortsystemserver am Standort hinzu.

- **Erstellen eines Standortsystemservers:** Legen Sie einen neuen Server als Standortsystemserver fest, und installieren Sie dann mehrere Rollen. Diese Methode unterscheidet sich nur auf der ersten Seite vom **Hinzufügen von Standortsystemrollen**. Zunächst legen Sie den Namen des Servers und den Standort fest, an dem Sie ihn installieren möchten.

> [!TIP]
> Wenn Sie eine Rolle auf einem Remotecomputer installieren, fügt Configuration Manager das Computerkonto auf dem Remotecomputer zu einer lokalen Gruppe auf dem Standortserver hinzu.
>
> Wenn Sie den Standort auf einem Domänencontroller installieren, ist die Gruppe auf dem Standortserver eine Domänengruppe anstelle einer lokalen Gruppe. In diesem Fall funktioniert die Systemrolle des Remotestandorts nicht sofort. Der Standortsystemserver muss neu gestartet werden, oder Sie müssen das Kerberos-Ticket für das Computerkonto des Remoteservers aktualisieren. Weitere Informationen finden Sie unter [Verwendete Konten](../../../plan-design/hierarchy/accounts.md).

Bevor die Standortsystemrolle installiert wird, überprüft Configuration Manager den Zielcomputer, um sicherzustellen, dass er die Anforderungen für die ausgewählten Rollen erfüllt.

Wenn Configuration Manager eine Standortsystemrolle installiert, werden Dateien standardmäßig auf dem ersten verfügbaren NTFS-formatierten Laufwerk installiert, das den der meiste Speicherplatz verfügbar ist. Erstellen Sie eine leere Datei namens **no_sms_on_drive.sms** im Stamm des Laufwerks, bevor Sie den Standortsystemserver installieren, damit Configuration Manager die Installation nicht auf bestimmten Laufwerken durchführt.

Configuration Manager verwendet das **Standortsystem-Installationskonto** zum Installieren der Rollen. Das Konto geben Sie bei der Installation der Rolle an. Dieses Konto ist standardmäßig das lokale Systemkonto des Standortservercomputers. Sie können ein Domänenbenutzerkonto als Standortsystem-Installationskonto festlegen. Weitere Informationen dazu finden Sie unter [Konten: Standortsystem-Installationskonto](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Installieren von Rollen auf einem vorhandenen Standortsystemserver

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Server und Standortsystemrollen**. Wählen Sie den vorhandenen Standortsystemserver aus, auf dem Sie die neuen Standortsystemrollen installieren möchten.

1. Klicken Sie im Menüband der Registerkarte **Start** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**.

1. Überprüfen Sie auf der Seite **Allgemein** die Einstellungen.

    > [!TIP]
    >  Stellen Sie sicher, dass Sie einen vollqualifizierten Internetdomänennamen festlegen, um über das Internet auf die Standortsystemrolle zugreifen zu können.

1. Wenn die Rollen auf diesem Server einen Internetproxy erfordern, legen Sie die Einstellungen für einen Proxyserver auf der Seite **Proxy** fest. Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](../../../plan-design/network/proxy-server-support.md).

1. Wählen Sie auf der Seite **Systemrollenauswahl** die Systemrollen aus, die Sie hinzufügen möchten.

1. Schließen Sie den Assistenten ab. Möglicherweise werden für bestimmte Rollen weitere Seiten angezeigt. Weitere Informationen finden Sie unter [Konfigurationsoptionen für Standortsystemrollen](configuration-options-for-site-system-roles.md).

> [!TIP]
> Das Windows PowerShell-Cmdlet **New-CMSiteSystemServer** erfüllt dieselbe Funktion wie dieses Verfahren. Weitere Informationen finden Sie unter [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Installieren von Rollen auf einem neuen Standortsystemserver

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Server und Standortsystemrollen**.

1. Klicken Sie im Menüband der Registerkarte **Start** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen**.

1. Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für das Standortsystem an.

    > [!TIP]
    > Stellen Sie sicher, dass Sie einen vollqualifizierten Internetdomänennamen festlegen, um über das Internet auf die neue Standortsystemrolle zugreifen zu können.

1. Wenn die Rollen auf diesem Server einen Internetproxy erfordern, legen Sie die Einstellungen für einen Proxyserver auf der Seite **Proxy** fest. Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](../../../plan-design/network/proxy-server-support.md).

1. Wählen Sie auf der Seite **Systemrollenauswahl** die Systemrollen aus, die Sie hinzufügen möchten.

1. Schließen Sie den Assistenten ab. Möglicherweise werden für bestimmte Rollen weitere Seiten angezeigt. Weitere Informationen finden Sie unter [Konfigurationsoptionen für Standortsystemrollen](configuration-options-for-site-system-roles.md).

> [!TIP]
> Das Windows PowerShell-Cmdlet **New-CMSiteSystemServer** erfüllt dieselbe Funktion wie dieses Verfahren. Weitere Informationen finden Sie unter [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver).

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurationsoptionen für Standortsystemrollen](configuration-options-for-site-system-roles.md)

- [Entfernen von Rollen](../install/uninstall-sites-and-hierarchies.md#bkmk_role)