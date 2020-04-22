---
title: Einführung in die Betriebssystembereitstellung
titleSuffix: Configuration Manager
description: Verstehen Sie die Konzepte, bevor Sie Betriebssysteme in Ihrer Configuration Manager-Umgebung bereitstellen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703868"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Einführung in die Betriebssystembereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können Configuration Manager dazu verwenden, Betriebssysteme auf vielen verschiedenen Wegen bereitzustellen. Verwenden Sie die Informationen in diesem Abschnitt, um zu verstehen, wie Betriebssysteme bereitgestellt und Tasks automatisiert werden. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> Vorgang der Betriebssystembereitstellung  
 In Configuration Manager gibt es mehrere Methoden, die Sie zum Bereitstellen eines Betriebssystems verwenden können. Unabhängig von der verwendeten Bereitstellungsmethode müssen Sie mehrere Aktionen ausführen:  

-   Identifizieren Sie Windows-Gerätetreiber, die zum Starten des bereitzustellenden Startimages oder zum Installieren des bereitzustellenden Betriebssystemimages erforderlich sind.  

-   Identifizieren Sie das Startabbild, das Sie zum Starten des Zielcomputers verwenden möchten.  

-   Verwenden Sie eine Tasksequenz, um ein Image des bereitzustellenden Betriebssystems zu erfassen. Alternativ können Sie ein Standardimage des Betriebssystems verwenden.  

-   Verteilen Sie das Startabbild, das Betriebssystemabbild sowie zugehörigen Inhalt an einen Verteilungspunkt.  

-   Erstellen Sie eine Tasksequenz mit den Schritten zum Bereitstellen des Startimages und des Betriebssystemimages.  

-   Stellen Sie die Tasksequenz für eine Sammlung von Computern bereit.  

-   Überwachen Sie die Bereitstellung.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> Betriebssystembereitstellungsszenarios  
 Es gibt viele Szenarien der Betriebssystembereitstellung in Configuration Manager, aus denen Sie je nach Umgebung und Zweck der Betriebssysteminstallation auswählen können.  Sie können z. B. einen vorhandenen Computer mit einer neuen Version von Windows partitionieren und formatieren oder Windows auf die neueste Version aktualisieren. Hilfe zur Ermittlung der Bereitstellungsmethode, die Ihren Bedürfnissen entspricht, finden Sie unter [Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Sie können aus den folgenden Szenarien für die Betriebssystembereitstellung auswählen:  

-   [Upgraden von Windows auf die neueste Version](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> Methoden zum Bereitstellen von Betriebssystemen  
 Es gibt mehrere Methoden, mit denen Sie Betriebssysteme für Configuration Manager-Clientcomputer bereitstellen können.  

- **PXE-initiierte Bereitstellungen:** Bei einer PXE-initiierten Bereitstellung wird die Bereitstellung von Clientcomputern über das Netzwerk angefordert. Das Betriebssystemabbild und ein Windows PE-Startabbild werden an einen Verteilungspunkt gesendet, der so konfiguriert ist, dass PXE-Startanforderungen akzeptiert werden. Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **Betriebssysteme über das Softwarecenter zur Verfügung stellen:** Sie können ein Betriebssystem bereitstellen und über das Softwarecenter zur Verfügung stellen. Configuration Manager-Clients können die Installation des Betriebssystems über das Softwarecenter initiieren. Weitere Informationen finden Sie unter [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Multicastbereitstellungen:** Multicastbereitstellungen sparen Netzwerkbandbreite, indem Daten gleichzeitig an mehrere Clients gesendet werden, anstatt eine Kopie der Daten über eine separate Verbindung an jeden Client einzeln zu senden. Bei dieser Bereitstellungsmethode wird das Betriebssystemabbild an einen Verteilungspunkt gesendet. Von diesem wird das Abbild wiederum bereitgestellt, wenn die Bereitstellung von Clientcomputern angefordert wird. Weitere Informationen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Bereitstellungen mit startbaren Medien:** Bei Bereitstellungen mit startfähigen Medien können Sie das Betriebssystem beim Starten des Zielcomputers bereitstellen. Beim Starten des Zielcomputers werden die Tasksequenz, das Betriebssystemabbild sowie sämtlicher anderer erforderlicher Inhalt aus dem Netzwerk abgerufen. Da dieser Inhalt nicht auf den Medien enthalten ist, können Sie den Inhalt aktualisieren, ohne die Medien neu erstellen zu müssen. Weitere Informationen finden Sie unter [Erstellen startbarer Medien](../deploy-use/create-bootable-media.md).  

- **Eigenständige Medienbereitstellungen:** Mit eigenständigen Medienbereitstellungen können Sie unter folgenden Umständen Betriebssysteme bereitstellen:  

  - In Umgebungen, in denen es nicht praktikabel ist, ein Betriebssystemabbild oder anderen große Pakete über das Netzwerk zu kopieren;  

  - in Umgebungen ohne Netzwerkverbindung oder mit geringer Netzwerkbandbreite.  

    Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](../deploy-use/create-stand-alone-media.md).  

- **Bereitstellungen vorab bereitgestellter Medien:** Bei Bereitstellungen mit vorab bereitgestellten Medien können Sie ein Betriebssystem für Computer bereitstellen, das nicht vollständig konfiguriert ist. Bei den vorab bereitgestellten Medien handelt es sich um eine WIM-Datei (Windows Imaging Format), die vom Hersteller auf einem Computer ohne Betriebssystem oder im Staging Center eines Unternehmens ohne Verbindung zur Configuration Manager-Umgebung installiert werden kann.  

   Später wird der Computer in der Configuration Manager-Umgebung unter Verwendung des auf den Medien bereitgestellten Startimages gestartet. Anschließend wird eine Verbindung mit dem Verwaltungspunkt des Standorts hergestellt und dort nach verfügbaren Tasksequenzen gesucht, mit denen der Downloadvorgang abgeschlossen wird. Durch diese Bereitstellungsmethode wird der Netzwerkdatenverkehr reduziert, da das Startabbild und Betriebssystemabbild bereits auf dem Zielcomputer vorhanden sind. Sie können auch Anwendungen, Pakete und Treiberpakete als vorab bereitgestellte Medien angeben. Weitere Informationen finden Sie unter [Erstellen vorab bereitgestellter Medien](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a> Startabbilder  
 Ein Startimage in Configuration Manager ist ein Windows PE-Image (WinPE), das während einer Betriebssystembereitstellung verwendet wird. Startimages dienen zum Starten eines Computers in Windows PE, einem minimalen Betriebssystem mit begrenzten Komponenten und Diensten zur Vorbereitung des Zielcomputers für die Windows-Installation. Configuration Manager stellt zwei Startimages bereit: je eins zur Unterstützung von x86- bzw. x64-Plattformen. Diese werden als Standardstartimages bezeichnet. Startimages, die Sie erstellen und zu Configuration Manager hinzufügen, werden als benutzerdefinierte Images bezeichnet. Standardstartimages können bei einem Update von Configuration Manager automatisch ersetzt werden. Weitere Informationen zu Startabbildern finden Sie im Thema [Verwalten von Startabbildern (Startimages)](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> Betriebssystemimages  
 Betriebssystemabbilder in Configuration Manager werden im WIM-Dateiformat (Windows Imaging) gespeichert. Sie stellen eine komprimierte Sammlung von Verweisdateien und -ordnern dar, die für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich sind. Bei allen Szenarien für die Betriebssystembereitstellung müssen Sie ein Betriebssystemabbild auswählen. Sie können das Standardimage des Betriebssystems verwenden oder das Betriebssystemimage von einem von Ihnen konfigurierten Referenzcomputer erstellen. Weitere Informationen finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a> Betriebssystem-Upgradepakete  
 Betriebssystem-Upgradepakete werden zum Aktualisieren eines Betriebssystems verwendet und sind von Setup initiierte Betriebssystembereitstellungen. Sie importieren Betriebssystem-Upgradepakete von einer DVD oder einem bereitgestellten ISO-Image in Configuration Manager. Weitere Informationen finden Sie unter [Manage operating system upgrade packages (Verwalten von Betriebssystem-Upgradepaketen)](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a> Medien zum Bereitstellen von Betriebssystemen  
 Sie können verschiedene Arten von Medien erstellen, die zum Bereitstellen von Betriebssystemen verwendet werden können. Hierzu gehören Erfassungsmedien, die zum Erfassen von Betriebssystemabbildern verwendet werden, sowie eigenständige, vorab bereitgestellte und startbare Medien, die zum Bereitstellen eines Betriebssystems verwendet werden. Mithilfe von Medien können Sie Betriebssysteme auf Computern ohne Netzwerkverbindung oder auf Computern bereitstellen, deren Verbindung mit Ihrem Configuration Manager-Standort eine geringe Bandbreite aufweist. Weitere Informationen zum Verwenden von Medien finden Sie unter [Erstellen von Tasksequenzmedien](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Gerätetreiber  
 Sie können Gerätetreiber auf Zielcomputern installieren, ohne sie in das Betriebssystemabbild einzuschließen, das bereitgestellt wird. In Configuration Manager ist ein Treiberkatalog enthalten, der Verweise zu allen Gerätetreibern enthält, die Sie in Configuration Manager importieren. Der Treiberkatalog befindet sich im Arbeitsbereich **Softwarebibliothek**. Er besteht aus zwei Knoten: **Treiber** und **Treiberpakete**. Im Knoten **Treiber** sind alle Treiber aufgelistet, die Sie in den Treiberkatalog importiert haben. Sie können diesen Knoten verwenden, um Details zu jedem importierten Treiber zu ermitteln, um die Zugehörigkeit eines Treibers zu Treiberpaketen oder Startabbildern zu ändern, um einen Treiber zu aktivieren bzw. zu deaktivieren usw. Weitere Informationen finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> Speichern und Wiederherstellen des Benutzerzustands  
 Beim Bereitstellen von Betriebssystemen können Sie den Benutzerzustand des Zielcomputers speichern, das Betriebssystem bereitstellen und den Benutzerzustand danach wiederherstellen. So gehen Sie normalerweise vor, wenn Sie das Betriebssystem auf einem Configuration Manager-Clientcomputer installieren.  

 Die Benutzerzustandsinformationen werden mithilfe von Tasksequenzen erfasst und wiederhergestellt. Wenn die Benutzerzustandsinformationen erfasst sind, können sie auf folgende Arten gespeichert werden:  

- Sie können die Benutzerzustandsdaten remote speichern, indem Sie einen Zustandsmigrationspunkt konfigurieren. Die Daten werden von der Erfassungstasksequenz an den Zustandsmigrationspunkt gesendet. Nach der Bereitstellung des Betriebssystems werden die Daten von der Wiederherstellungstasksequenz abgerufen, und der Benutzerzustand wird auf dem Zielcomputer wiederhergestellt.  

- Sie können die Benutzerzustandsdaten lokal an einem bestimmten Speicherort speichern. In diesem Szenario werden die Benutzerdaten von der Erfassungstasksequenz an einen bestimmten Speicherort auf dem Zielcomputer kopiert. Nach der Bereitstellung des Betriebssystems werden die Daten durch die Wiederherstellungstasksequenz von diesem Speicherort abgerufen.  

- Sie können Hardlinks angeben, die verwendet werden können, um die Benutzerdaten am ursprünglichen Speicherort wiederherzustellen. In diesem Szenario verbleiben die Benutzerdaten auf dem Laufwerk, wenn das alte Betriebssystem entfernt wird. Nach der Bereitstellung des Betriebssystems werden die Benutzerzustandsdaten von der Wiederherstellungstasksequenz mithilfe der Hardlinks am ursprünglichen Speicherort wiederhergestellt.  

  Weitere Informationen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Bereitstellen auf unbekannten Computern  
 Sie können Betriebssysteme auf Computern bereitstellen, die nicht von Configuration Manager verwaltet werden. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge. Solche Computer werden als unbekannte Computer bezeichnet. Zu unbekannten Computern gehören die folgenden:  

- Computer, auf denen kein Configuration Manager-Client installiert ist  

- Computer, die nicht in Configuration Manager importiert wurden  

- Computer, die von Configuration Manager nicht ermittelt wurden  

  Weitere Informationen finden Sie unter [Prepare for unknown computer deployments (Vorbereiten auf Bereitstellungen für unbekannte Computer)](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> Zuordnen von Benutzern zu Computern  
 Bei der Bereitstellung eines Betriebssystems können Sie Benutzer Zielcomputern zuordnen, um Aktionen im Zusammenhang mit der Affinität zwischen Benutzer und Gerät zu unterstützen. Wenn Sie dem Zielcomputer einen Benutzer zuordnen, kann der Administrator zu einem späteren Zeitpunkt Aktionen – beispielsweise Bereitstellen einer Anwendung auf dem Computer eines bestimmten Benutzers – auf jedem Computer ausführen, dem dieser Benutzer zugeordnet ist. Wenn Sie jedoch ein Betriebssystem bereitstellen, können Sie es nicht auf dem Computer eines bestimmten Benutzers bereitstellen. Weitere Informationen finden Sie unter [Zuordnen von Benutzern zu einem Zielcomputer](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> Verwenden von Tasksequenzen zum Automatisieren von Schritten  
 Sie können Tasksequenzen erstellen, um eine Vielzahl von Tasks in Ihrer Configuration Manager-Umgebung auszuführen. Die Aktionen der Tasksequenz werden in den einzelnen Schritten der Sequenz definiert. Bei der Ausführung der Tasksequenz werden die Aktionen der einzelnen Schritte auf Befehlszeilenebene ohne Benutzereingriff ausgeführt. Sie können Tasksequenzen für Folgendes verwenden:  

-   [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Erstellen einer Tasksequenz zum Erfassen und Wiederherstellen eines Benutzerzustands](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Erstellen einer benutzerdefinierten Tasksequenz](../deploy-use/create-a-custom-task-sequence.md)  
