---
title: Sicherheit und Datenschutz von Sammlungen
titleSuffix: Configuration Manager
description: Informieren Sie sich über die bewährten Sicherheits- und Datenschutzmethoden für Sammlungen in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695528"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Sicherheit und Datenschutz bei Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält bewährte Sicherheitsmethoden und Datenschutzinformationen für Sammlungen in Configuration Manager.  

 Es gibt keine speziellen Informationen zum Datenschutz für die Sammlungen in Configuration Manager. Sammlungen sind Container für Ressourcen, z. B. Benutzer und Geräte. Die Sammlungsmitgliedschaft hängt oft von den Informationen ab, die Configuration Manager während des Standardbetriebs sammelt. Mithilfe von Ressourceninformationen, die bei einer Ermittlung oder Inventur gesammelt wurden, kann beispielsweise eine Sammlung so konfiguriert werden, dass die Geräte ermittelt werden, die mit den angegebenen Kriterien übereinstimmen. Sammlungen können auch auf den aktuellen Statusinformationen für Clientverwaltungsvorgänge basieren, z. B. das Bereitstellen von Software und das Überprüfen auf Kompatibilität. Zusätzlich zu diesen abfragebasierten Sammlungen können von Administratoren Ressourcen zu Sammlungen hinzugefügt werden.  

 Weitere Informationen zu Sammlungen finden Sie unter [Einführung in Sammlungen](../../../../core/clients/manage/collections/introduction-to-collections.md). Weitere Informationen zu allen bewährten Sicherheitsmethoden und Datenschutzinformationen für Configuration Manager-Vorgänge, die zum Konfigurieren einer Sammlungsmitgliedschaft verwendet werden können, finden Sie unter [Bewährte Sicherheitsmethoden und Datenschutzinformationen für Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Bewährte Sicherheitsmethoden für Sammlungen  
 Verwenden Sie die folgende bewährte Sicherheitsmethode für Sammlungen.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Wenn Sie eine Sammlung mithilfe einer MOF-Datei (Managed Object Format) exportieren oder importieren, die an einem Netzwerkspeicherort gespeichert ist, schützen Sie den Speicherort und den Netzwerkkanal.|Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.<br /><br /> Verwenden Sie SMB-Signaturen (Server Message Block) bzw. Internetprotokollsicherheit (IPsec) zwischen dem Netzwerkspeicherort und dem Standortserver, um potenzielle Angreifer an der Manipulation der exportierten Sammlungsdaten zu hindern. Verwenden Sie IPsec zum Verschlüsseln der Daten im Netzwerk, um die Offenlegung von Informationen zu verhindern.|  

### <a name="security-issues-for-collections"></a>Sicherheitsprobleme bei Sammlungen  
 Sammlungen bergen die folgenden Sicherheitsprobleme:  

-   Wenn Sie Sammlungsvariablen verwenden, können lokale Administratoren potenziell vertrauliche Informationen lesen.  

     Sammlungsvariablen können verwendet werden, wenn Sie ein Betriebssystem bereitstellen.  
