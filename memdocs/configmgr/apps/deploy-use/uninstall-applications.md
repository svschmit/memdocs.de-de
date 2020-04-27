---
title: Deinstallieren von Anwendungen
titleSuffix: Configuration Manager
description: Deinstallieren von Anwendungen mithilfe von Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075845"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Deinstallieren von Anwendungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Gehen Sie folgendermaßen vor, um eine Anwendung zu deinstallieren, die Sie zuvor bereitgestellt haben.

-   Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Inhalt** die Befehlszeile zum Deinstallieren des Bereitstellungstypinhalts an.  

-   Stellen Sie die Anwendung mit der Bereitstellungsaktion **Deinstallieren**bereit.  

> [!IMPORTANT]  
> Einige Anwendungstypen unterstützen keine Deinstallation.  

 In der folgenden Liste finden Sie weitere Informationen zum Deinstallieren von Anwendungen:  

-   Wenn Sie eine Configuration Manager-Anwendung (Configuration Manager) deinstallieren, werden abhängige Anwendungen nicht automatisch deinstalliert.  

-   Wenn Sie eine Anwendung mit der Aktion **Deinstallieren** für einen Benutzer bereitstellen und die Anwendung für alle Benutzer des Computers installiert worden war, kann bei der Deinstallation ein Fehler auftreten, wenn die Berechtigungen des entsprechenden Benutzerkontos für die Deinstallation unzureichend sind.  

-   Wenn Sie einen Benutzer oder ein Gerät aus einer Sammlung entfernen, für die eine Anwendung bereitgestellt wurde, wird die Anwendung nicht automatisch vom Gerät entfernt.  

-   Bei einer Bereitstellung mit dem Bereitstellungszweck **Deinstallieren** werden keine Anforderungsregeln überprüft. Wenn die Anwendung auf dem Computer installiert ist, auf dem die Bereitstellung ausgeführt wird, wird sie deinstalliert.  

> [!IMPORTANT]  
> Wenn Sie die Anwendung mit dem Deinstallationsvorgang bereitstellen möchten, müssen Sie zunächst alle vorhandenen Anwendungsbereitstellungen, simulierte Bereitstellungen oder Tasksequenzbereitstellungen löschen, die diese Anwendung enthalten. 

 Weitere Informationen zum Erstellen von Bereitstellungstypen finden Sie unter [Anwendungen erstellen](../../apps/deploy-use/create-applications.md).  

 Weitere Informationen zum Bereitstellen von Anwendungen finden Sie unter [Anwendungen bereitstellen](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Deinstallieren einer Anwendung  

1.  Konfigurieren Sie den Bereitstellungstyp für die Anwendung mit der Deinstallationsbefehlszeile mithilfe einer der folgenden Methoden:  

    -   Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** die Option **Informationen zu diesem Bereitstellungstyp automatisch den Installationsdateien entnehmen** aus. Wenn die Informationen in den Installationsdateien verfügbar sind, wird den Eigenschaften des Bereitstellungstyps automatisch die Deinstallationsbefehlszeile hinzugefügt.  

    -   Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Inhalt** im Feld **Deinstallationsprogramm** die Befehlszeile zum Deinstallieren der Anwendung an.  

        > [!NOTE]  
        >  Die Seite **Inhalt** wird nur angezeigt, wenn Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** die Option **Informationen zum Bereitstellungstyp manuell angeben** auswählen.  

    -   Geben Sie auf der Registerkarte **Programme** im Dialogfeld **Eigenschaften von <*Name des Bereitstellungstyps*>** im Feld **Deinstallationsprogramm** die Befehlszeile zum Deinstallieren der Anwendung an.  

2.  Stellen Sie die Anwendung bereit, und wählen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Bereitstellungseinstellungen** die Bereitstellungsaktion **Deinstallieren** aus.  

    > [!NOTE]  
    >  Wenn Sie die Bereitstellungsaktion **Deinstallieren**auswählen, wird der Bereitstellungszweck automatisch als **Erforderlich**konfiguriert.  
