---
title: Veraltet für Standortserver
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu den Produkten und Betriebssystemen, die von Configuration Manager für Standortserver nicht mehr unterstützt werden.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702568"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Entfernte und veraltete Elemente für Configuration Manager-Standortserver

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden Produkte und Betriebssysteme beschrieben, deren Support für Configuration Manager-Standortserver eingestellt wurde oder die bei einem zukünftigen Update entfernt werden (veraltet sind). Dies dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf die Verwendung von Configuration Manager auswirken können.  

Die hier angegebenen Informationen können sich im Laufe der Zeit ändern. Möglicherweise wird nicht jedes veraltete Feature, Produkt oder Betriebssystem hier aufgeführt.  

## <a name="server-os"></a>Serverbetriebssystem  

|Betriebssysteme|Erste Ankündigung als veraltetes Feature|Support entfernt|
|-|-|-|
|Windows Server 2008 R2 mit SP1|10. Juli 2015| Version 1702|
|Windows Server 2008 mit SP2|10. Juli 2015|Version 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server-Versionen|Erste Ankündigung als veraltetes Feature|Support entfernt|
|-|-|-|
|SQL Server 2008 R2:|10. Juli 2015|Version 1702|
|SQL Server 2008|10. Juli 2015|Version 1511|

Wenn Sie ein Upgrade für Ihre Version von SQL Server durchführen müssen, werden folgende Methoden in der Reihenfolge ihrer Komplexität empfohlen:

1. [Direktes Upgrade von SQL Server](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (empfohlen).  

2. Installieren Sie auf einem neuen Computer eine neue Version von SQL Server. [Verwenden Sie anschließend die Option zur Datenbankverschiebung](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) im Configuration Manager-Setup, um Ihren Standortserver auf den neuen Computer mit SQL Server zu verweisen.  

3. Verwenden Sie [Sicherung und Wiederherstellung](../../../servers/manage/backup-and-recovery.md).  

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Entfernte und veraltete Elemente](removed-and-deprecated.md)  

- [Microsoft-Support-Lifecycle-Richtlinien](https://support.microsoft.com/lifecycle)  

- [Support für die Current Branch-Versionen von Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)  
