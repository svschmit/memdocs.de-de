---
title: Bereitstellen von Konfigurationsbaselines
titleSuffix: Configuration Manager
description: Stellen Sie Konfigurationsbaselines bereit, um Bereitstellungen von Konfigurationsbaselines zu definieren und um Konfigurationsbaselines zu Bereitstellungen hinzuzufügen oder aus diesen zu entfernen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692448"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Bereitstellen von Konfigurationsbaselines in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In Configuration Manager müssen Konfigurationsbaselines für eine oder mehrere Sammlungen von Benutzern oder Geräten bereitgestellt werden, bevor von den Clientgeräten in diesen Sammlungen die Kompatibilität mit der Konfigurationsbaseline ausgewertet werden kann.  

Mithilfe des Dialogfelds **Konfigurationsbasislinien bereitstellen** , können Sie Bereitstellungen für Konfigurationsbasislinien definieren. Dazu gehören das Hinzufügen oder Entfernen von Konfigurationsbasislinien zu bzw. von Bereitstellungen sowie das Angeben des Auswertungszeitplans.  

## <a name="deploy-a-configuration-baseline"></a>Bereitstellen einer Konfigurationsbasislinie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Wählen Sie in der Liste **Konfigurationsbasislinien** die Konfigurationsbasislinie aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Wählen Sie im Dialogfeld **Konfigurationsbasislinien bereitstellen** die bereitzustellenden Konfigurationsbasislinien in der Liste **Verfügbare Konfigurationsbasislinien** aus. Klicken Sie auf **Hinzufügen** , um diese zur Liste **Ausgewählte Konfigurationsbasislinien** hinzuzufügen.  

    > [!IMPORTANT]  
    >  Wenn Sie ein Konfigurationselement ändern, das einer bereitgestellten Konfigurationsbasislinie hinzugefügt wurde, wird das überarbeitete Konfigurationselement bis zum nächsten geplanten Auswertungszeitpunkt nicht auf Kompatibilität geprüft.  

5.  Geben Sie die folgenden zusätzlichen Informationen an:  

    -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird:** Stellt automatisch Regeln wieder her, die nicht mit der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), der Registrierung, den Skripts und sämtlichen Einstellungen für die von Configuration Manager registrierten mobile Geräte kompatibel sind.  

    -   **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn ein Wartungsfenster für die Sammlung konfiguriert wurde, für die Sie die Konfigurationsbasislinie bereitstellen, aktivieren Sie diese Option, um Kompatibilitätseinstellungen zum Wiederherstellen des Werts außerhalb des Wartungsfensters zuzulassen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

6.  **Warnung generieren:** Konfiguriert eine Warnung, die generiert wird, sobald die Kompatibilität einer Konfigurationsbaseline zu einem bestimmten Datum und einer bestimmten Uhrzeit unterhalb eines angegebenen Prozentsatzes liegt. Sie können außerdem angeben, ob eine Warnung an System Center Operations Manager gesendet werden soll.  

7.  **Sammlung:** Klicken Sie auf **Durchsuchen** , um die Sammlung auszuwählen, in der Sie die Konfigurationsbasislinie bereitstellen möchten.  

8.  **Geben Sie den Zeitplan für die Kompatibilitätsauswertung dieser Konfigurationsbaseline an:** Gibt den Zeitplan an, nach dem die bereitgestellte Konfigurationsbaseline auf Clientcomputern ausgewertet wird. Dabei kann es sich um einen einfachen oder benutzerdefinierten Zeitplan handeln.  

    > [!NOTE]  
    >  Wenn die Konfigurationsbasislinie für einen Computer bereitgestellt wird, wird sie innerhalb von zwei Stunden ab der von Ihnen geplanten Startzeit auf Kompatibilität ausgewertet. Wenn sie für einen Benutzer bereitgestellt wird, wird sie beim Anmelden des Benutzers auf Kompatibilität ausgewertet.  

9. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbasislinien bereitstellen** zu schließen und die Bereitstellung zu erstellen. Weitere Informationen zum Überwachen der Bereitstellung finden Sie unter [Überwachen von Kompatibilitätseinstellungen](monitor-compliance-settings.md).  
