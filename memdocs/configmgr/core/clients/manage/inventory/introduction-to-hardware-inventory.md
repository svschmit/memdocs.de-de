---
title: 'Hardwareinventur '
titleSuffix: Configuration Manager
description: Erhalten Sie eine Einführung in die Hardwareinventur in Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695408"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Einführung in die Hardwareinventur in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sammeln Sie mit der Hardwareinventur in Configuration Manager Informationen zur Hardwarekonfiguration der Clientgeräte in Ihrer Organisation. Zum Sammeln der Hardwareinventur müssen Sie in den Clienteinstellungen die Einstellung **Hardwareinventur auf Clients aktivieren** aktivieren.  

 Wenn der Client nach Aktivieren der Hardwareinventur einen Hardwareinventurzyklus ausführt, sendet der Client die Informationen an einen Verwaltungspunkt am Standort des Clients. Der Verwaltungspunkt leitet diese Inventurinformationen an den Configuration Manager-Standortserver weiter, auf dem die Inventurinformationen in der Standortdatenbank gespeichert werden. Die Hardwareinventur wird auf Clients gemäß dem Zeitplan ausgeführt, den Sie in den Clienteinstellungen festlegen.  
## <a name="view-hardware-inventory"></a>Anzeigen der Hardwareinventur 

 Sie können die von Configuration Manager gesammelten Hardwareinventurdaten unter Zuhilfenahme mehrerer Methoden wie z.B. der folgenden anzeigen:  

- [Erstellen von Abfragen, bei denen Geräte zurückgegeben werden, die auf einer bestimmten Hardwarekonfiguration basieren](../../../../core/servers/manage/introduction-to-queries.md)  

- [Erstellen von abfragebasierten Sammlungen, die auf einer bestimmten Hardwarekonfiguration basieren](../../../../core/clients/manage/collections/introduction-to-collections.md) Mitgliedschaften abfragebasierter Sammlungen werden automatisch nach einem Zeitplan aktualisiert. Für zahlreiche Tasks, zu denen auch die Softwarebereitstellung zählt, können Sie Sammlungen verwenden.

- [Ausführen von Berichten, in denen spezifische Details zu Hardwarekonfigurationen in Ihrer Organisation angezeigt werden](../../../servers/manage/introduction-to-reporting.md)

- Anzeigen von detaillierten Hardwareinventurinformationen, die von Clientgeräten gesammelt wurden, im [Ressourcen-Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

Beim Ausführen der Hardwareinventur auf einem Clientgerät wird vom Client als Erstes immer das vollständige Inventar als Inventurdaten zurückgegeben. Alle nachfolgenden Inventurdaten stellen lediglich das Deltainventar dar. Vom Standortserver werden die Deltainventurinformationen in der empfangenen Reihenfolge verarbeitet. Falls Deltainformationen für einen Client fehlen, werden zusätzliche Deltainformationen vom Standortserver zurückgewiesen, und der Client erhält die Anweisung für einen vollständigen Inventurzyklus.  

 Configuration Manager bietet eingeschränkte Unterstützung für Dual-Boot-Computer. Eine Ermittlung von Dual-Boot-Computern ist zwar in Configuration Manager möglich, es werden jedoch nur die Inventurinformationen des Betriebssystems zurückgegeben, das zum Zeitpunkt der Ausführung des Inventurzyklus aktiv ist.  

> [!NOTE]  
>  Informationen zur Verwendung der Hardwareinventur bei Clients, auf denen Linux und UNIX ausgeführt werden, finden Sie unter [Hardwareinventur für Linux und UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Erweitern der Konfigurations-Manager-Hardwareinventur  
 Neben der integrierten Hardwareinventur in Configuration Manager können Sie die Hardwareinventur auch durch eine der folgenden Methoden erweitern, um weitere Informationen zu sammeln:  

- Sie können Inventurklassen für die Hardwareinventur über die Configuration Manager-Konsole aktivieren, deaktivieren, hinzufügen und entfernen.  
- Verwenden Sie NOIDMIF-Dateien zum Sammeln von Informationen zu Clientgeräten, die nicht von Configuration Manager inventarisiert werden können. Möglicherweise möchten z. B. Gerät Asset Informationen sammeln, die nur als Etikett auf dem Gerät vorhanden ist. NOIDMIF-Inventur wird automatisch das Clientgerät, dem er entnommen wurde zugeordnet.  
- Verwenden Sie IDMIF-Dateien zum Sammeln von Informationen zu Ressourcen, die keinem Configuration Manager-Client zugeordnet sind, z.B. Projektoren, Fotokopierer und Netzwerkdrucker.


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Verwendung dieser Methoden zum Erweitern der Hardwareinventur für Configuration Manager finden Sie unter [Konfigurieren der Hardwareinventur](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
