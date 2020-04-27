---
title: Herunterladen der Definitionen von Microsoft
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Schadsoftwaredefinitionen für Endpoint Protection aus Microsoft Updates für Configuration Manager herunterladen.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697238"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Aktivieren der Endpoint Protection-Schadsoftwaredefinitionen zum Herunterladen über Microsoft Update

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie das Herunterladen von Definitionsupdates von Microsoft Update auswählen, prüfen die Clients die Microsoft Update-Website in dem Intervall, das im Dialogfeld für die Richtlinie für Antischadsoftware im Abschnitt **Security Intelligence-Updates** definiert ist.

 Diese Methode kann nützlich sein, wenn der Client nicht mit dem Configuration Manager-Standort verbunden ist, oder wenn die Benutzer in der Lage sein sollen, Definitionsupdates einzuleiten.

> [!IMPORTANT]
> - Clients müssen auf Microsoft Update im Internet zugreifen können, um diese Methode zum Herunterladen von Definitionsupdates nutzen zu können.
> - Der Abschnitt **Definitionsupdates** wurde ab Configuration Manager Version 1902 in **Security Intelligence-Updates** umbenannt.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Verwenden des Microsoft Center zum Schutz vor Schadsoftware zum Herunterladen von Definitionen
 Sie können Clients zum Herunterladen von Definitionsupdates aus dem Microsoft Center zum Schutz vor Schadsoftware konfigurieren. Diese Option wird von Endpoint Protection-Clients zum Herunterladen von Definitionsupdates verwendet, wenn das Herunterladen von Updates aus einer anderen Quelle nicht möglich war. Diese Updatemethode ist nützlich, wenn ein Problem mit Ihrer Configuration Manager-Infrastruktur besteht, durch das die Bereitstellung von Updates verhindert wird.

> [!IMPORTANT]
>  Clients müssen auf Microsoft Update im Internet zugreifen können, um diese Methode zum Herunterladen von Definitionsupdates nutzen zu können.
> 
> 
> [!div class="button"]
> [Nächster Schritt >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Zurück >](endpoint-configure-alerts.md)
