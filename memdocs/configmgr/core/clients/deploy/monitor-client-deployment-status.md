---
title: Überwachen des Clientbereitstellungsstatus
titleSuffix: Configuration Manager
description: Überwachen Sie den Status der Clientbereitstellung in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693848"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Überwachen des Status der Clientbereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Das standortweite Bereitstellen von Clients nimmt einige Zeit in Anspruch, und einige Installationen verlaufen beim ersten Mal nicht erfolgreich. Mithilfe der Configuration Manager-Konsole können Sie die Clientbereitstellungen innerhalb einer Sammlung überwachen, denn sie berichtet in Echtzeit über den Status der Clientbereitstellungen.  

> [!NOTE]  
>  Die Configuration Manager-Konsole stellt die beste und zuverlässigste Methode zum Überwachen von Clientbereitstellungen dar (wie in diesem Artikel beschrieben). Der Bereich **Clientstatus** im Konsolenarbeitsbereich **Überwachung** gibt den Status der Clientbereitstellungen genau und in Echtzeit wieder. Sie können Clientbereitstellungen auch mit anderen Tools überwachen, z. B. mit Server-Manager in Windows Server oder mit System Center Operations Manager. Allerdings erhalten Sie dann unter Umständen Alarme für normale Aktivitäten bei Clientinstallation. Bedingt durch die Funktionsweise des Clientinstallationsprogramms (CCMSetup.exe) in verschiedenen Umgebungen, generieren diese anderen Tools möglicherweise falsche Alarme und Warnmeldungen, die den Zustand der Clientbereitstellungen nicht genau widerspiegeln.  

 Im Arbeitsbereich **Überwachung** der Konsole können Sie die folgenden Statusmeldungen für die Clientbereitstellungen überwachen, die aktuell in einer von Ihnen angegebenen Sammlung ausgeführt werden:  

- Kompatibel  

- In Bearbeitung  

- Nicht kompatibel  

- Failed  

- Unbekannt  

  Configuration Manager berichtet über die Bereitstellungen geordnet nach Produktionsclients oder Präproduktionsclients. Außerdem können Sie mit der Configuration Manager-Konsole ein Diagramm mit den fehlerhaften Bereitstellungen in einem angegebenen Zeitraum anzeigen. Anhand dieser Daten können Sie leicht feststellen, ob Ihre Maßnahmen zur Fehlerbehebung die Erfolgsrate Ihrer Bereitstellungen mit der Zeit anwachsen lassen.  

## <a name="to-monitor-client-deployments"></a>So überwachen Sie den Status von Clientbereitstellungen  

- Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** > **Clientstatus**.  

- Klicken Sie je nach der Version der zu überwachenden Clients auf **Produktionsclientbereitstellung** oder auf **Präproduktionsclientbereitstellung**.  

- Schauen Sie sich die Diagramme zum Clientbereitstellungsstatus und zu den Fehlern bei der Clientbereitstellung an.  

- Wenn Sie den Geltungsbereich des Berichts ändern möchten, klicken Sie auf **Durchsuchen...** {}, und wählen Sie eine andere Sammlung aus.  

  Weitere Informationen zu Präproduktionsclientbereitstellungen finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung](../../../core/clients/manage/upgrade/test-client-upgrades.md).

  > [!NOTE]
  > Der Bereitstellungsstatus auf den Computern, auf denen Standortsystemrollen in einer Präproduktionssammlung gehostet werden, kann eventuell als **Nicht kompatibel** gemeldet werden, selbst wenn der Client erfolgreich bereitgestellt wurde. Wenn Sie den Client in den Produktivbetrieb versetzen, wird der Bereitstellungsstatus ordnungsgemäß gemeldet.   

  Informationen zum Überwachen des Status von bereitgestellten Clients finden Sie unter [Überwachen von Clients](../../../core/clients/manage/monitor-clients.md).  

  Sie können mithilfe von Configuration Manager-Berichten weitere Informationen zum Status von Clients an Ihrem Standort erhalten. Weitere Informationen zum Ausführen von Berichten finden Sie unter [Einführung in die Berichterstellung](../../servers/manage/introduction-to-reporting.md).  
