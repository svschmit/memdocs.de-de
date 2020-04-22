---
title: Installieren von Anwendungen auf einem Gerät
titleSuffix: Configuration Manager
description: Installieren Sie eine Anwendung mit Configuration Manager sofort auf einem Gerät ohne Sammlung.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689448"
---
# <a name="install-applications-for-a-device"></a>Installieren von Anwendungen auf einem Gerät

<!--4402180-->

Ab Version 1906 können Sie über die Configuration Manager-Konsole Anwendungen auf einem Gerät in Echtzeit installieren. Dieses Feature kann dazu beitragen, den Bedarf an getrennten Sammlungen für jede Anwendung zu reduzieren.

## <a name="prerequisites"></a>Voraussetzungen

- Aktivieren Sie das [optionale Feature](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Anwendungsanforderungen für Benutzer pro Gerät genehmigen**.  

- [Stellen Sie die Anwendung für eine Gerätesammlung als ](deploy-applications.md)Verfügbar *bereit.*  

    - Wählen Sie auf der Seite **Bereitstellungseinstellungen** des Bereitstellungs-Assistenten die folgende Option aus: **Ein Administrator muss eine Anforderung für diese Anwendung auf dem Gerät genehmigen**.  

        > [!Note]  
        > Mit diesen Bereitstellungseinstellungen wird keine Richtlinie an den Client gesendet. Die App wird im Softwarecenter nicht als verfügbar angezeigt, und Benutzer können die App nicht mit dieser Bereitstellung installieren. Nachdem Sie diese Aktion zur Installation der App verwendet haben, kann der Benutzer sie ausführen und ihren Installationsstatus im Softwarecenter einsehen.

- Ihr Benutzerkonto benötigt die folgenden Berechtigungen:

    - **Anwendung:** Lesen, Genehmigen

    - **Sammlung:** Lesen, Ressource lesen, Ressource ändern, Gesammelte Datei anzeigen

    Die integrierte Rolle **Anwendungsadministrator** verfügt beispielsweise über diese Berechtigungen.

> [!TIP]
> Warten Sie in einer Hierarchie, bis die Anwendungs- und Bereitstellungsinformationen an dem primären Standort repliziert werden, dem der Zielclient zugewiesen ist.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Prozess

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Geräte** aus. Wählen Sie das Zielgerät und dann auf dem Menüband die Aktion **Anwendung installieren** aus.

1. Wählen Sie in der Liste eine oder mehrere Anwendungen aus. In der Liste werden nur Anwendungen angezeigt, die Sie bereits mit den erforderlichen Einstellungen bereitgestellt haben.

Dadurch wird die Installation der ausgewählten vorab bereitgestellten Anwendungen auf dem Gerät ausgelöst.

Um den Status der Genehmigungsanforderung anzuzeigen, navigieren Sie zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungsanforderungen** aus.

Überwachen Sie die App-Installation wie gewohnt im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung**.


## <a name="see-also"></a>Weitere Informationen:

[Approve applications (Genehmigen von Anwendungen)](app-approval.md)
