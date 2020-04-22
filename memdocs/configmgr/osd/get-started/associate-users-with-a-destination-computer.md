---
title: Zuordnen von Benutzern zu Computern
titleSuffix: Configuration Manager
description: Konfigurieren Sie Configuration Manager, um Benutzer beim Bereitstellen von Betriebssystemen zu Zielcomputern zuzuordnen.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709008"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Zuordnen von Benutzern zu einem Zielcomputer in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie Configuration Manager verwenden, um Betriebssysteme bereitzustellen, können Sie dem Zielcomputer Benutzer zuordnen. Diese Option funktioniert unabhängig davon, ob ein oder mehrere Benutzer die primären Benutzer des Zielcomputers sind.  

Von der Affinität zwischen Benutzer und Gerät wird die benutzerzentrierte Verwaltung unterstützt, wenn Sie Anwendungen bereitstellen. Wenn Sie dem Zielcomputer, auf dem ein Betriebssystem installiert werden soll, einen Benutzer zuordnen, können Sie diesem Benutzer zu einem späteren Zeitpunkt Anwendungen bereitstellen, die dann automatisch auf dem Zielcomputer installiert werden. Sie können zwar Unterstützung für die Affinität zwischen Benutzer und Gerät bei der Betriebssystembereitstellung konfigurieren, jedoch nicht das Betriebssystem mithilfe einer solchen Affinität bereitstellen.  

Weitere Informationen zur Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Es gibt mehrere Methoden, mit denen Sie die Affinität zwischen Benutzer und Gerät in Ihre Betriebssystembereitstellungen integrieren können. Sie können die Affinität zwischen Benutzer und Gerät in PXE-Bereitstellungen, in Bereitstellungen mit startbaren Medien sowie in Bereitstellungen mit vorab bereitgestellten Medien integrieren.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Erstellen Sie eine Tasksequenz, welche die Variable **SMSTSAssignUsersMode** enthält.

Fügen Sie die Variable **SMSTSAssignUsersMode** dem Anfang Ihrer Tasksequenz hinzu, indem Sie den Schritt [Tasksequenzvariable festlegen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) verwenden. Mit dieser Variable geben Sie an, wie die Benutzerinformationen von der Tasksequenz verarbeitet werden.

Weitere Informationen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Erstellen eines Prestart-Befehls, von dem Benutzerinformationen gesammelt werden

Beim Prestart-Befehl kann es sich um ein VBScript mit einem Eingabefeld handeln. Es kann sich auch um eine HTML-Anwendung (HTA) handeln, die die eingegebenen Benutzerdaten überprüft. 

Von diesem Prestart-Befehl muss die Variable **SMSTSUDAUsers** festgelegt werden, die beim Ausführen der Tasksequenz verwendet wird. Diese Variable kann auf einem Computer, einer Sammlung oder einer Tasksequenzvariable festgelegt werden.

Weitere Informationen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Konfigurieren der Zuordnung von Benutzer und Zielcomputer durch Medien und Verteilungspunkte

Der Verteilungspunkt bzw. das Medium unterstützt die Zuordnung von Benutzern zum Zielcomputer, auf dem das Betriebssystem bereitgestellt wird. Verwenden Sie eine der folgenden Methoden: 

- [Konfigurieren eines Verteilungspunkts zum Akzeptieren von PXE-Startanforderungen](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Erstellen von startbaren Medien](../deploy-use/create-bootable-media.md)  
- [Erstellen von vorab bereitgestellten Medien](../deploy-use/create-prestaged-media.md)  


In der Konfiguration zur Unterstützung der Affinität zwischen Benutzer und Gerät ist keine Methode zur Überprüfung der Benutzeridentität enthalten. Dieses Verhalten ist wichtig, wenn ein Techniker den Computer bereitstellt und anstelle des Benutzers die Informationen eingibt. Sie können nicht nur festlegen, wie die Tasksequenz Benutzerinformationen verarbeitet, sondern mithilfe der Konfiguration dieser Optionen an dem Verteilungspunkt und den Medien können Sie auch die Bereitstellungen begrenzen, die durch einen PXE-Start oder von einem bestimmten Mediumtyp gestartet werden.
