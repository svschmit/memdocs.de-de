---
title: Verwalten von Apps für lokales MDM
titleSuffix: Configuration Manager
description: Verwalten von Anwendungen für die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9fafcc4b5462afb1b8e528837ea6ba61203e73d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347140"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Verwalten von Apps für die lokale Verwaltung mobiler Geräte (MDM) in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie Geräte mit Configuration Manager lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) verwalten, können Sie die folgenden Anwendungs Typen verwalten:

- Windows Phone-App-Paket (XAP-Datei)
- Windows Phone-App-Paket (in Windows Phone Store)
- Windows Installer über MDM
- Webanwendung.

Allgemeine Informationen zum Verwalten von Configuration Manager Anwendungen und Bereitstellungs Typen finden Sie unter [Verwaltungsaufgaben für Configuration Manager Anwendungen](../../apps/deploy-use/management-tasks-applications.md).

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Erstellen Windows Phone Anwendung

In einer Configuration Manager-Anwendung ist mindestens ein Bereitstellungstyp enthalten. Der Bereitstellungstyp umfasst die Installationsdateien und Informationen, die zum Bereitstellen von Software auf einem Gerät erforderlich sind. Bereitstellungstypen verfügen auch über Regeln, aus denen hervorgeht, wann und wie die Software bereitgestellt wird.

Die allgemeinen Schritte zum Erstellen einer APP und Bereitstellungs Typen finden Sie unter [Erstellen einer Anwendung](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager unterstützt die folgenden App-Dateitypen für Windows Mobile-Geräte:

|Gerätetyp|Unterstützte Dateitypen|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Stellen Sie Windows Phone-Apps als **Verfügbar** oder **Erforderlich** bereit. Verwenden Sie Bereitstellungen außerdem zum Deinstallieren von Apps.

## <a name="deploy-and-monitor-apps"></a>Bereitstellen und Überwachen von apps

Bereitstellen und Überwachen von Anwendungen für mobile Geräte in Configuration Manager dieselben wie für andere Geräte, wie z. b. Desktops und Server. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md)
- [Überwachen von Anwendungen](../../apps/deploy-use/monitor-applications-from-the-console.md)

Überprüfen Sie die folgenden Einschränkungen, die für Mobile gerätespezifisch sind:

- MDM-registrierte Geräte unterstützen keine simulierten Bereitstellungen, Einstellungen für Benutzerfreundlichkeit oder Zeitplanung.

- Fügen Sie einer einzelnen APP nicht mehr als 100 Gebiets Schemas hinzu. Dadurch wird verhindert, dass die APP auf dem Gerät installiert wird.

## <a name="next-step"></a>Nächster Schritt

Wenn Sie Änderungen vornehmen, deinstallieren oder eine bereitgestellte Anwendung durch eine neue Anwendung ersetzen möchten, verwalten Sie Sie genauso wie jede beliebige app in Configuration Manager. Weitere Informationen finden Sie unter [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md).
