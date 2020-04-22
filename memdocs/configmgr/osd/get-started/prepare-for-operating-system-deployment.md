---
title: Vorbereiten der Betriebssystembereitstellung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Vorbereiten auf die Betriebssystembereitstellung in Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708838"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Vorbereiten der Betriebssystembereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Es gibt mehrere Dinge, die Sie in Configuration Manager ausführen müssen, bevor Sie Betriebssysteme bereitstellen können. Verwenden Sie die folgenden Artikel, um die Betriebssystembereitstellung vorzubereiten:  

-   [Verwalten von Startimages](manage-boot-images.md)  

-   [Verwalten von Betriebssystemimages](manage-operating-system-images.md)  

-   [Verwalten von Betriebssystemupgradepaketen](manage-operating-system-upgrade-packages.md)  

-   [Verwalten von Treibern](manage-drivers.md)  

-   [Verwalten des Benutzerzustands](manage-user-state.md)  

-   [Vorbereiten auf Bereitstellungen für unbekannte Computer](prepare-for-unknown-computer-deployments.md)  

-   [Zuordnen von Benutzern zu einem Zielcomputer](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>BS-Imagegröße  

BS-Images sind groß. Beispielsweise beträgt die Imagegröße für Windows 7 mindestens 3 GB. Die Größe des Image und die Anzahl der Computer, auf denen Sie das BS gleichzeitig bereitstellen, haben Einfluss auf die Netzwerkleistung und die verfügbare Bandbreite. Stellen Sie sicher, dass Sie die Netzwerkleistung testen. Durch das Testen können Sie besser messen, wie sich die Imagebereitstellung auswirken könnte und wie lange es dauert, die Bereitstellung abzuschließen. Configuration Manager-Aktivitäten, die sich auf die Leistung des Netzwerks auswirken, umfassen die Verteilung des Images an einen Verteilungspunkt sowie die Verteilung des Images von einem Standort an einen anderen und das Herunterladen des Images auf den Client.  

Sie müssen auch genügend Speicherplatz auf den Verteilungspunkten einplanen, auf denen die BS-Images gehostet werden.  

Weitere Informationen finden Sie unter [Zusätzliche Überlegungen zur Planung von Verteilungspunkten](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Cachegröße des Clients  

Wenn Inhalt von Configuration Manager-Clients heruntergeladen wird, wird automatisch der intelligente Hintergrundübertragungsdienst (Background Intelligent Transfer Service oder BITS) verwendet, sofern dieser verfügbar ist. Wenn Sie eine Tasksequenz bereitstellen, mit der ein BS installiert wird, können Sie über eine Bereitstellungsoption festlegen, dass das vollständige Image von den Configuration Manager-Clients vor der Ausführung der Tasksequenz in einen lokalen Cache heruntergeladen wird.  

Wenn ein Configuration Manager-Client ein BS-Image herunterladen muss, aber nicht genügend Platz im Cache vorhanden ist, kann der Client den Platz in seinem Cache löschen. Er überprüft die anderen Pakete im Cache, um festzustellen, ob das Löschen eines der ältesten Pakete genügend Speicherplatz für das Image zur Verfügung stellt. Wenn durch das Löschen von Paketen nicht genügend Speicherplatz freigegeben wird, wird das Image nicht vom Client heruntergeladen, und bei der Bereitstellung tritt ein Fehler auf. Das kann der Fall sein, wenn sich ein großes Paket im Cache befindet, das aufgrund der Konfiguration im Cache verbleiben muss. Falls durch das Löschen von Paketen genügend Speicherplatz im Cache freigegeben werden kann, wird der Löschvorgang vom Client ausgeführt, und das Abbild wird in den Cache heruntergeladen.  

Der Standardcache auf Configuration Manager-Clients ist möglicherweise für die meisten BS-Bereitstellungen nicht groß genug. Wenn Sie das vollständige Image in den Clientcache herunterladen möchten, müssen Sie die Größe des Clientcaches auf den Zielcomputern so anpassen, dass das bereitzustellende Image darin aufgenommen werden kann.  

Weitere Informationen hierzu finden Sie unter [Konfigurieren des Clientcache](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


