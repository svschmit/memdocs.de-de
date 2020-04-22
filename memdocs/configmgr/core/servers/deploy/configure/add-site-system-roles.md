---
title: Hinzufügen von Standortsystemrollen
titleSuffix: Configuration Manager
description: Grundlegendes zu Configuration Manager-Standortsystemrollen und wie sie zum Erweitern der Funktionalität und der Kapazität Ihres Standorts hinzugefügt werden
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8a4ef1c4377e7b5ffba4ab0f04394ff1253c40df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704898"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>Hinzufügen von Standortsystemrollen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Jeder Configuration Manager-Standort unterstützt mehrere Standortsystemrollen. Jede Rolle erweitert die Funktionalität und Kapazität Ihres Standorts, um dem Standort Dienste bereitzustellen und Benutzer und Geräten zu verwalten. Jede Standortsystemrolle auf einem Standortserver muss sich am selben Standort befinden.

Von Configuration Manager werden keine Standortsystemrollen für mehrere Standorte auf einem einzigen Standortsystemserver unterstützt.

> [!TIP]
> Wenn Sie mit den Grundlagen von Standortsystemrollen oder den Unterschieden zwischen Standortserver, Standortsystemserver und Standortsystemrollen nicht vertraut sind, lesen Sie [Grundlagen von Configuration Manager](../../../understand/fundamentals.md).

In den folgenden Artikeln werden Verfahren und die zugehörigen Details für die Installation von Standortsystemrollen ausführlich beschrieben:

- [Installieren von Standortsystemrollen](install-site-system-roles.md): Grundlegende Hinweise zur Verwendung der beiden konsoleninternen Assistenten zum Installieren neuer Standortsystemrollen.

- [Installieren von cloudbasierten Verteilungspunkten](install-cloud-based-distribution-points-in-microsoft-azure.md): Verwenden Sie Microsoft Azure zum Hosten von Inhalten, die Sie für Clients bereitstellen.

- [Installieren von Standortsystemrollen für die lokale Verwaltung mobiler Geräte (MDM)](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md): Richten Sie Ihre Standortsystemrollen ein, damit diese die Verwaltung moderner Geräte mit der lokalen Configuration Manager-Verwaltung mobiler Geräte unterstützen.

- [Konfigurationsoptionen für Standortsystemrollen](configuration-options-for-site-system-roles.md): Einige Standortsystemrollen unterstützen Konfigurationen, für die mehr Details erforderlich sind als innerhalb der Benutzeroberfläche erklärt werden können.

- [Entfernen einer Standortsystemrolle](../install/uninstall-sites-and-hierarchies.md#bkmk_role): Anleitungen und Verfahren zum Entfernen von Rollen von Standortsystemservern.
