---
title: Dashboard für Surface-Geräte
titleSuffix: Configuration Manager
description: Abrufen von Informationen zu Surface-Geräten mit dem Dashboard
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: cbea7d7e126b120145533b7cf19822b54b3cb701
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607965"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Dashboard für Surface-Geräte in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Ab Version 1802 erhalten Sie mit dem Dashboard für Surface-Geräte einen kompakten Überblick über Informationen zu Surface-Geräten in Ihrer Umgebung. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Öffnen des Dashboards für Surface-Geräte

Gehen Sie folgendermaßen vor, um das Dashboard für Surface-Geräte zu öffnen: 

1. Öffnen Sie die Configuration Manager-Konsole. 
2. Klicken Sie auf den Knoten **Überwachung**. 
3. Klicken Sie auf **Surface-Geräte**, um das Dashboard zu laden.

**Dashboard für Surface-Geräte**
![Surface device dashboard](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Abrufen von Informationen im Dashboard für Surface-Geräte

Im Dashboard für Surface-Geräte werden drei Diagramme für Ihre Umgebung angezeigt: 

- **Prozent der Surface-Geräte:** Prozentsatz der Surface-Geräte in Ihrer gesamten Umgebung

    ![Diagramm „Prozent der Surface-Geräte“](media/Percent-Surface-Devices.PNG)
- **Surface-Modelle:** Anzahl der Geräte pro Surface-Modell 
  - Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Prozentzahl der Surface-Geräte angezeigt, die zum ausgewählten Modell gehören. 

       ![Diagramm „Surface-Modelle“](media/Surface-Models-Hover.PNG)
  - Wenn Sie auf einen Diagrammabschnitt klicken, wird die Geräteliste für das Modell aufgerufen. 
      ![Geräteliste für Surface-Modell](media/Surface-Model-Device-List.PNG)

- **Top 5-Firmwareversionen**: Diagramm mit den fünf am häufigsten verwendeten Firmwaremodellen in Ihrer Umgebung 
  - Wenn Sie mit dem Mauszeiger auf einen Diagrammabschnitt zeigen, wird die Anzahl der Surface-Geräte angezeigt, die zur ausgewählten Firmwareversion gehören. Ab Configuration Manager Version 1806 wird durch Klicken auf einen Diagrammabschnitt eine Liste relevanter Geräte angezeigt. <!--1358654-->
     ![Surface-Firmware-QuickInfo](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zu Surface-Geräten finden Sie auf der [Surface](https://www.microsoft.com/surface)-Website.

Weitere Informationen zur Bereitstellung von Surface-Firmwareupdates in Configuration Manger finden Sie unter [Verwalten von Surface-Treiberupdates](../../../sum/deploy-use/surface-drivers.md).




