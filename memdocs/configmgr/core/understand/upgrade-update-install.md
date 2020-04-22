---
title: Grundlegendes zu Upgrades, Updates und der Installation
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über den Unterschied zwischen den Begriffen Installation, Update und Upgrade beim Verwalten einer Configuration Manager-Infrastruktur.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706718"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Informationen zu Upgrade, Update und Installation für einen Standort und eine Hierarchieinfrastruktur

*Gilt für: Configuration Manager (Current Branch)*

Beim Verwalten von Configuration Manager-Standorten und der Hierarchieinfrastruktur werden die Begriffe *Upgrade*, *Update* und *Installation* verwendet, um drei verschiedene Konzepte zu beschreiben.

## <a name="upgrade"></a>Upgrade

Die Begriffe *Upgrade* oder *direktes Upgrade* werden verwendet, wenn Sie einen Configuration Manager 2012-Standort oder eine Configuration Manager 2012-Hierarchie in einen Standort bzw. eine Hierarchie mit Current Branch von Configuration Manager konvertieren.

Wenn Sie ein Upgrade von System Center 2012 Configuration Manager auf Current Branch von Configuration Manager durchführen, verwenden Sie weiterhin dieselben Server zum Hosten Ihrer Standorte und Standortserver und behalten vorhandene Daten und Konfigurationen für Configuration Manager bei.  Dies unterscheidet sich von der [Migration](../migration/migrate-data-between-hierarchies.md), die eine Möglichkeit darstellt, Ihre Konfigurationen und Daten zu verwalteten Geräten beizubehalten, während Sie neue Standorte mit Current Branch von Configuration Manager verwenden, die auf neuer Hardware installiert sind.

Weitere Informationen finden Sie unter [Upgrade auf Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).



## <a name="update"></a>Update
Der Begriff *Update* wird für die Installation von konsoleninternen Updates für Configuration Manager und für Out-of-Band-Updates verwendet, die nicht von der Configuration Manager-Konsole aus übermittelt werden können. Konsoleninterne Updates können die Version des Current Branch-Standorts (oder des Technical Preview-Standorts) ändern, sodass eine höhere Version ausgeführt wird. Wenn an Ihrem Standort beispielsweise Version 1806 ausgeführt wird, können Sie ein Update für Version 1810 installieren. Mithilfe von Updates können auch bekannte Probleme behoben werden, ohne die Standortversion zu ändern.      

In der Regel werden mit Updates Sicherheitsfixes, Qualitätsverbesserungen und neue Funktionen zu Ihren vorhanden Bereitstellung hinzugefügt. Wenn Sie Technical Preview Branch verwenden, können Sie mit einem Update eine neuere Version der Technical Preview installieren.
- Sie entscheiden, wann das konsoleninterne Update – beginnend mit dem Standort der obersten Ebene Ihrer Hierarchie – installiert werden soll.
- Sie können jedes Update installieren, das in der Konsole verfügbar ist. Beispiel: Wenn an Ihrem Standort Version 1802 ausgeführt wird und Version 1806 und 1810 angeboten werden, sollten Sie Version 1810 installieren, weil jede Version die Funktionen in zuvor veröffentlichten Versionen einschließt.
- Wenn die Installation eines neuen Updates an Ihrem Standort der obersten Ebene abgeschlossen wurde, wird auch beim untergeordneten primären Standort das Update gestartet. Sie können jedoch [Dienstfenster](../servers/manage/service-windows.md) einrichten, um den Installationszeitpunkt von Updates zu bestimmen.
- An sekundären Standorten werden Updates nicht automatisch installiert. Dort müssen Sie Updates in der Configuration Manager-Konsole manuell starten.

Weitere Informationen finden Sie unter [Updates für Configuration Manager](../servers/manage/updates.md) und [Technical Preview für Configuration Manager](../get-started/technical-preview.md).



## <a name="install"></a>Installation
Der Begriff *Installation* wird verwendet, wenn eine neue Configuration Manager-Hierarchie von Grund auf neu erstellt wird oder zusätzliche Standorte zu einer vorhandenen Hierarchie hinzufügt werden.  

Bei der Installation eines neuen primären Standorts oder eines Standorts der zentralen Verwaltung ist der Speicherort der Datei „Setup.exe“ und die damit verbundenen und von Ihnen verwendeten Quelldateien von Ihrem Installationsszenario abhängig.

Weitere Informationen finden Sie unter [Vorbereitung zur Installation von Standorten ](../servers/deploy/install/prepare-to-install-sites.md).
