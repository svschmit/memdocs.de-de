---
title: Vorbereiten auf Bereitstellungen für unbekannte Computer
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Betriebssysteme auf Computern bereitstellen, die nicht von Configuration Manager in der Configuration Manager-Umgebung verwaltet werden.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708818"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Vorbereiten auf Bereitstellungen für unbekannte Computer in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Thema, um Betriebssysteme für unbekannte Computer in Ihrer Configuration Manager-Umgebung bereitzustellen. Ein unbekannter Computer ist ein Computer, der nicht von Configuration Manager verwaltet wird. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge. Zu unbekannten Computern gehören die folgenden:  

- Computer, auf denen kein Configuration Manager-Client installiert ist  

- Computer, die nicht in Configuration Manager importiert wurden  

- Computer, die von Configuration Manager nicht ermittelt wurden  

  Sie können Betriebssysteme mit den folgenden Bereitstellungsmethoden für unbekannte Computer bereitstellen:  

- [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Verwenden startbarer Medien zum Bereitstellen eines Betriebssystems](../deploy-use/create-bootable-media.md)  

- [Verwenden vorab bereitgestellter Medien zum Bereitstellen eines Betriebssystems](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Bereitstellungsworkflow bei unbekannten Computern  
 Im Folgenden wird der grundlegende Workflow zum Bereitstellen eines Betriebssystems für einen unbekannten Computer beschrieben:  

-   Wählen Sie ein unbekanntes Computerobjekt aus, das Sie für die Bereitstellung verwenden möchten. Sie können das Betriebssystem einem der unbekannten Computerobjekte in der Sammlung **Alle unbekannten Computer** hinzufügen, oder Sie können die Objekte in der Sammlung **Alle unbekannten Computer** einer anderen Sammlung hinzufügen. In Configuration Manager gibt es in der Sammlung **Alle unbekannten Computer** zwei unbekannte Computerobjekte. Eins davon ist für x86-Computer, das andere für x64-Computer.  

    > [!NOTE]  
    >  Das Objekt **x 86 unbekannter Computer** ist für Computer, die nur x86-fähig sind. Das Objekt **x64 Unbekannter Computer** ist für Computer bestimmt, die x86- und x64-fähig sind. Mit anderen Worten, diese Objekte beschreiben die Architektur des Zielcomputers. Es wird nicht das Betriebssystem beschrieben, das Sie auf dem Zielcomputer bereitstellen möchten.  

-   Konfigurieren Sie einen PXE-fähigen Verteilungspunkt, oder erstellen Sie ein Medium zur Unterstützung von Bereitstellungen für unbekannte Computer.  

-   Stellen Sie die Tasksequenz zum Installieren des Betriebssystems bereit.  

## <a name="unknown-computer-installation-process"></a>Installationsprozess eines unbekannten Computers  
 Wenn ein Computer erstmals von PXE oder Medien gestartet wird, wird von Configuration Manager geprüft, ob in der Configuration Manager-Datenbank ein Eintrag für diesen Computer besteht. Ist dies der Fall, wird von Configuration Manager geprüft, ob Tasksequenzen für diesen Eintrag bereitgestellt wurden. Besteht kein Eintrag, wird von Configuration Manager geprüft, ob Tasksequenzen für ein unbekanntes Computerobjekt bereitgestellt wurden. In beiden Fällen wird von Configuration Manager eine der folgenden Aktionen ausgeführt:  

- Wenn eine Tasksequenz verfügbar ist, wird der Benutzer von Configuration Manager dazu aufgefordert, die Tasksequenz auszuführen.  

- Wenn eine erforderliche Tasksequenz verfügbar ist, wird die Tasksequenz von Configuration Manager automatisch ausgeführt.  

- Wenn für einen Eintrag keine Tasksequenz bereitgestellt wurde, wird von Configuration Manager eine entsprechende Fehlermeldung generiert.  

  Wenn ein unbekannter Computer gestartet wird, wird er von Configuration Manager nicht als unbekannter Computer, sondern als nicht bereitgestellter Computer erkannt. Das bedeutet, dass der Computer nun die Tasksequenzen erhalten kann, die dem unbekannten Computerobjekt bereitgestellt wurden. Von der bereitgestellten Tasksequenz wird anschließend ein Betriebssystemimage installiert, das den Configuration Manager-Client enthalten muss.  

  Nach der Installation des Configuration Manager-Clients wird ein Eintrag für den Computer erstellt, und der Computer wird in der entsprechenden Configuration Manager-Sammlung angezeigt. Wenn beim Installieren des Betriebssystemimages oder des Configuration Manager-Clients ein Fehler auftritt, wird für den Computer ein Eintrag „Unbekannt“ erstellt, und der Computer wird in der Sammlung **Alle Systeme** angezeigt.  

> [!NOTE]  
>  Beim Installieren des Betriebssystemabbilds können Variablen der Sammlung, nicht jedoch Computervariablen von diesem Computer durch die Tasksequenz abgerufen werden.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Aktivieren der Unterstützung für unbekannte Computer  
 Verwenden Sie die folgenden Angaben, um die Unterstützung für unbekannte Computer zu aktivieren, wenn Sie ein Betriebssystem unter Verwendung von PXE, startbaren Medien und vorab bereitgestellten Medien bereitstellen:  

-   **PXE**  

     Aktivieren Sie bei einem PXE-fähigen Verteilungspunkt auf der Registerkarte **PXE** das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren** . Weitere Informationen finden Sie unter [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)(Konfigurieren von Verteilungspunkten zur Annahme von PXE-Anforderungen).  

-   **Startbare Medien**  

     Wählen Sie im Assistenten zum Erstellen von Tasksequenzmedien auf der Seite **Sicherheit** das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren** . Weitere Informationen finden Sie unter [Konfigurieren von Verteilungspunkten zum Akzeptieren von PXE-Anforderungen](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) und [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Vorab bereitgestellte Medien**  

     Wählen Sie im Assistenten zum Erstellen von Tasksequenzmedien auf der Seite **Sicherheit** das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren** . Weitere Informationen finden Sie unter [Erstellen von vorab bereitgestellten Medien](../deploy-use/create-prestaged-media.md).  
