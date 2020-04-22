---
title: Aktualisieren von Linux- und UNIX-Clients
titleSuffix: Configuration Manager
description: Upgraden Sie einen Client auf einem Linux- oder UNIX-Server in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696818"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Aktualisieren von Clients für Linux- und UNIX-Server in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr. 
> 
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Sie können die Version des Clients für Linux und UNIX auf einem Computer auf eine neuere Clientversion aktualisieren, ohne vorher den aktuellen Client zu deinstallieren. Dazu installieren Sie das Installationspaket des neuen Clients auf dem Computer, wobei Sie die Befehlszeileneigenschaft **-keepdb** verwenden. Bei der Installation des Client für Linux und UNIX werden die vorhandenen Clientdaten mit den neuen Clientdateien überschrieben. Die Befehlszeileneigenschaft **-keepdb** bewirkt aber, dass beim Installationsprozess der eindeutige Bezeichner (GUID), die lokale Datenbank mit Informationen und der Zertifikatspeicher des Clients beibehalten werden. Diese Informationen werden dann für die Installation des neuen Clients verwendet.  

 Angenommen, Sie haben einen RHEL5-x64-Computer, auf dem der Client aus der ursprünglichen Version des Configuration Manager-Clients für Linux und UNIX ausgeführt wird. Um diesen Client auf die Clientversion des kumulativen Updates 1 zu aktualisieren, führen Sie das **install**-Skript manuell aus, um das entsprechende Clientpaket aus dem kumulativen Update 1 zu installieren, wobei Sie den Befehlszeilenschalter **-keepdb** hinzufügen. Informationen finden Sie in der folgenden Beispielbefehlszeile:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Verwenden einer Softwarebereitstellung, um den Client auf Linux- und UNIX-Servern zu aktualisieren  
 Sie können eine Softwarebereitstellung verwenden, um den Client für Linux und UNIX auf eine neue Clientversion zu aktualisieren. Allerdings kann der Konfigurations-Manager-Client das Installationsskript nicht direkt ausführen, um den neuen Client zu installieren, denn bei der Installation eines neuen Clients muss zunächst der aktuelle Client deinstalliert werden. Durch diese Aktion würde der Konfigurations-Manager-Clientprozess, der das Installationsskript ausführt, beendet, bevor mit der Installation des neuen Clients begonnen wird. Damit Sie den neuen Client erfolgreich mit einer Softwarebereitstellung installieren können, müssen Sie die Installation so planen, dass sie zu einem späteren Zeitpunkt gestartet und über die zum Betriebssystem gehörenden Planungsfunktionen ausgeführt wird.  

 Verwenden Sie eine Softwarebereitstellung, um zuerst die Dateien für das neue Clientinstallationspaket auf den Clientcomputer zu kopieren. Dann können Sie ein Skript bereitstellen und ausführen, um den Clientinstallationsprozess zu planen. In dem Skript wird der zum Betriebssystem gehörende **at**-Befehl verwendet, um den Start des Skripts zu verzögern. Dies hat zur Folge, dass das Ausführen des Skripts vom Betriebssystem des Clients und nicht vom Konfigurations-Manager-Client auf dem Computer verwaltet wird. Durch dieses Verhalten wird es der Befehlszeile, die durch das Skript aufgerufen wurde, ermöglicht, zunächst den Konfigurations-Manager-Client zu deinstallieren und anschließend den neuen Client zu installieren. Somit wird das Aktualisieren des Clients auf dem Linux- oder UNIX-Computer abgeschlossen. Nach Abschluss des Upgrades wird der aktualisierte Client weiterhin von Configuration Manager verwaltet.  

 Gehen Sie wie folgt vor, um eine Softwarebereitstellung zu konfigurieren, mit der der Client für Linux und UNIX aktualisiert wird. In den folgenden Schritten und Beispielen wird ein RHEL5-x64-Computer, auf dem die erste Version des Clients ausgeführt wird, auf die Clientversion des kumulativen Updates 1 aktualisiert.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>So verwenden Sie eine Softwarebereitstellung, um den Client auf Linux- und UNIX-Servern zu aktualisieren  

1. Kopieren Sie das neue Clientinstallationspaket auf den Computer, auf dem der Konfigurations-Manager-Client ausgeführt wird, den Sie upgraden möchten.  

    Beispielsweise könnten Sie das Clientinstallationspaket und das Installationsskript für das kumulative Update 1 im folgenden Ordner auf dem Clientcomputer ablegen: **/tmp/PATCH**  

2. Erstellen Sie ein Skript, um das Upgrade des Konfigurations-Manager-Clients zu verwalten. Legen Sie dann eine Kopie des Skripts im selben Ordner auf dem Clientcomputer ab wie die Clientinstallationsdateien aus Schritt 1.  

    Für das Skript ist kein bestimmter Name erforderlich. Es muss aber Befehlszeilen enthalten, die es ermöglichen, die Clientinstallationsdateien aus einem lokalen Ordner auf dem Clientcomputer zu verwenden und das Installationspaket zu installieren, indem die **-keepdb**-Befehlszeileneigenschaft verwendet wird. Sie verwenden die **-keepdb**-Befehlszeileneigenschaft, damit der eindeutige Bezeichner des aktuellen Clients erhalten bleibt, sodass er vom neu installierten Client verwendet werden kann.  

    Erstellen Sie z.B. ein Skript namens **upgrade.sh**, das die folgenden Zeilen enthält:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Kopieren Sie es dann in den Ordner **/Tmp/PATCH** auf dem Clientcomputer.

3. Implementieren Sie die Softwarebereitstellung so, dass für jeden Client der integrierte **at** -Befehl verwendet wird, um das Skript **upgrade.sh** auszuführen, wobei dieses nach einer kurzen Verzögerung gestartet wird.  

    Verwenden Sie beispielsweise die folgende Befehlszeile, um das Skript auszuführen: **at -f /tmp/upgrade.sh -m now + 5 minutes**  

   Nachdem der Client das Ausführen des Skripts **upgrade.sh** erfolgreich geplant hat, sendet der Client eine Statusmeldung, in der mitgeteilt wird, dass die Softwarebereitstellung erfolgreich abgeschlossen wurde. Allerdings wird die tatsächlichen Clientinstallation dann nach der Verzögerung durch den Computer verwaltet. Überprüfen Sie nach Abschluss der Clientaktualisierung die Installation, indem Sie sich die Datei **/var/opt/microsoft/scxcm.log** auf dem Clientcomputer ansehen. Überprüfen Sie, ob der Client installiert wurde und mit dem Standort kommuniziert, indem Sie die Details für den betreffenden Client unter dem Knoten **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole anzeigen.  
