---
title: Aktualisieren und Außerkraftsetzen von Anwendungen
titleSuffix: Configuration Manager
description: Überarbeiten, Ablösen oder Deinstallieren bereitgestellter Anwendungen mithilfe von Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7770f1db0e311186a908890dc339401ed3cbeb4b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689888"
---
# <a name="update-and-retire-applications-with-configuration-manager"></a>Aktualisieren und Außerkraftsetzen von Anwendungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Nach einiger Zeit möchten Sie wahrscheinlich Änderungen an einer Anwendung vornehmen, eine Anwendung deinstallieren oder eine bereits bereitgestellte Anwendung durch eine neue Anwendung ersetzen. Configuration Manager bietet Ihnen diese Funktionen zum Aktualisieren und Deinstallieren von Anwendungen:  

- **Überarbeiten von Anwendungen**. Wenn Sie Änderungen an einer Anwendung vornehmen, pflegt Configuration Manager den Verlauf der Änderungen. Sie können jederzeit zu einer früheren Version der Anwendung zurückkehren. Außerdem können Sie die Eigenschaften anzeigen, eine ältere Revision einer Anwendung wiederherstellen oder eine ältere Revision löschen.  

  Weitere Informationen finden Sie unter [Anwendungsrevisionen](revise-and-supersede-applications.md#application-revisions).  

- **Ablösen von Anwendungen**. Sie können vorhandene Anwendungen mithilfe einer Ablösungsbeziehung aktualisieren oder ersetzen. Wenn Sie eine Anwendung ablösen, können Sie einen neuen Bereitstellungstyp als Ersatz für den Bereitstellungstyp der abgelösten Anwendung angeben. Sie können auch festlegen, ob vor dem Installieren der ablösenden Anwendung ein Upgrade der abzulösenden Anwendung ausgeführt oder die abzulösende Anwendung deinstalliert werden soll.  

  Weitere Informationen finden Sie unter [Anwendungsablösung](revise-and-supersede-applications.md#application-supersedence).  

- **Deinstallieren von Anwendungen**. Dank Configuration Manager ist das Deinstallieren von Anwendungen einfach. Dies kann im Hintergrund ausgeführt werden, ohne dass der Anwendungs- oder Gerätebenutzer eingreifen muss.  

  Weitere Informationen finden Sie unter [Deinstallieren von Anwendungen](uninstall-applications.md).  
