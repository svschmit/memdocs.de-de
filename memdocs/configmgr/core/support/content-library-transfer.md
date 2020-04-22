---
title: Tool für die Inhaltsbibliotheksübertragung
titleSuffix: Configuration Manager
description: Verwenden Sie das Content Library Transfer-Tool, um Inhalt von einem Laufwerk auf ein anderes auf einem Configuration Manager-Verteilungspunkt zu übertragen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703438"
---
# <a name="content-library-transfer-tool"></a>Tool für die Inhaltsbibliotheksübertragung

*Gilt für: Configuration Manager (Current Branch)*

Das Content Library Transfer-Tool ist eines der [Configuration Manager-Tools](tools.md). Es überträgt Inhalt von einem Laufwerk an ein anderes. Es kann auf Verwaltungspunkten von Standortsystemen ausgeführt werden. Es unterstützt Verteilungspunkte, die mit einem Standort oder Remotestandortsystemen verbunden sind.  

Das Tool eignet sich besonders für Szenarios, in denen das Laufwerk, das die Inhaltsbibliothek hostet, voll ist. Fügen Sie als erstes ein anderes Laufwerk hinzu, auf dem genügend Speicherplatz frei ist, um die Inhaltsbibliothek zu hosten, oder ermitteln Sie ein geeignetes Laufwerk. Verwenden Sie anschließend **ContentLibraryTransfer.exe**, um Inhalt von dem alten, vollen Laufwerk auf das neue, leere Laufwerk zu übertragen.
 
Sobald der Übertragungsvorgang abgeschlossen ist, können Clientcomputer über den neuen Speicherort auf den Inhalt zugreifen.



## <a name="usage"></a>Verwendung 

Führen Sie **ContentLibraryTransfer.exe** als Benutzer mit Administratorberechtigungen auf dem Verteilungspunkt aus. 

#### <a name="syntax"></a>Syntax 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Beispiel
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Einschränkungen

- Führen Sie das Tool lokal auf dem Verteilungspunkt aus. Sie können es nicht über einen Remotecomputer ausführen.  

- Verwenden Sie es nur, wenn kein Client aktiv auf den Verteilungspunkt zugreift. Wenn Sie das Tool ausführen, während Clients auf Inhalt zugreifen, sind die Daten in der Inhaltsbibliothek auf dem Ziellaufwerk möglicherweise unvollständig. Die Datenübertragung schlägt dann möglicherweise fehl, sodass die Inhaltsbibliothek nicht mehr verwendet werden kann.  

- Verteilen Sie Inhalt nicht an den Verteilungspunkt, wenn Sie gerade das Tool ausführen. Wenn Sie das Tool ausführen, während Inhalt auf einen Verteilungspunkt geschrieben wird, sind die Daten in der Inhaltsbibliothek auf dem Ziellaufwerk möglicherweise unvollständig. Die Datenübertragung schlägt dann möglicherweise fehl, sodass die Inhaltsbibliothek nicht mehr verwendet werden kann.



## <a name="see-also"></a>Weitere Informationen:

- [Grundlegende Konzepte für das Content Management](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Die Inhaltsbibliothek](../plan-design/hierarchy/the-content-library.md)
