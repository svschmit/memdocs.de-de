---
title: Sicherheit und Datenschutz für die Migration
titleSuffix: Configuration Manager
description: Hier finden Sie bewährte Sicherheitsmethoden und Datenschutzinformationen für die Migration zur Configuration Manager (Current Branch)-Umgebung.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ba1f41af778602fb95d268c071b5f0d1dde158c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693388"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Sicherheit und Datenschutz für die Migration zu Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

In diesem Thema finden Sie bewährte Sicherheitsmethoden und Datenschutzinformationen für die Migration zur Configuration Manager (Current Branch)-Umgebung.  

## <a name="security-best-practices-for-migration"></a>Bewährte Sicherheitsmethoden für die Migration  
 Wenden Sie die folgende bewährte Sicherheitsmethode bei der Migration an.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Verwenden Sie statt eines Benutzerkontos das Computerkonto für SMS-Anbieterkonto und SQL Server-Konto des Quellstandorts.|Wenn Sie zur Migration ein Benutzerkonto verwenden müssen, entfernen Sie nach Abschluss der Migration die Kontodetails.|  
|Verwenden Sie IPsec, wenn Sie Inhalte von einem Verteilungspunkt an einem Quellstandort zu einem Verteilungspunkt Ihres Zielstandorts migrieren.|Auf die migrierten Inhalte wird zwar ein Hashwert angewendet, um Manipulationen festzustellen, doch wenn die Daten während der Übertragung geändert werden, kann die Migration nicht ausgeführt werden.|  
|Überwachen Sie die Administratoren, die Migrationsaufträge erstellen können, und beschränken Sie ihre Anzahl.|Die Integrität der Zielhierarchiedatenbank hängt von der Integrität der Daten ab, die der Administrator für den Import aus der Quellhierarchie auswählt. Außerdem kann dieser Administrator alle Daten der Quellhierarchie lesen.|  

### <a name="security-issues-for-migration"></a>Sicherheitsprobleme bei der Migration  
Die Migration birgt folgende Sicherheitsprobleme:  

-   Clients, für die der Zugriff auf einen Quellstandort gesperrt ist, können ggf. der Zielhierarchie zugewiesen werden, bevor ihr Clientdatensatz migriert wird.  

     Obwohl Configuration Manager den Status „Gesperrt“ eines Clients bei der Migration beibehält, kann der Client der Zielhierarchie zugewiesen werden, wenn die Zuweisung erfolgt, bevor die Migration des Clientdatensatzes abgeschlossen ist.  

-   Überwachungsmeldungen werden nicht migriert.  

Wenn Sie Daten von einem Quellstandort zu einem Zielstandort migrieren, gehen alle Überwachungsinformationen der Quellhierarchie verloren.  

## <a name="privacy-information-for-migration"></a>Datenschutzinformationen zur Migration  
 Bei der Migration werden Informationen in den Standortdatenbanken ermittelt, die Sie in einer Quellinfrastruktur identifizieren, und in der Datenbank der Zielhierarchie gespeichert. Welche Informationen von Configuration Manager für einen Quellstandort oder eine Quellhierarchie ermittelt werden können, richtet sich nach den Features, die in der Quellumgebung aktiviert wurden. Außerdem ist dies von den Verwaltungsvorgängen abhängig, die in der Quellumgebung ausgeführt wurden.  

 Weitere Informationen zu Sicherheit und Datenschutz finden Sie unter folgenden Themen:  

-   Weitere Informationen zum Configuration Manager 2007-Datenschutz finden Sie unter [Sicherheit und Datenschutz für Configuration Manager 2007](https://go.microsoft.com/fwlink/p/?LinkId=216450) in der Configuration Manager 2007-Dokumentationsbibliothek.  

-   Weitere Informationen zum System Center 2012 Configuration Manager-Datenschutz finden Sie unter [Sicherheit und Datenschutz für System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) in der System Center 2012 Configuration Manager-Dokumentationsbibliothek.  

-   Weitere Informationen zum Configuration Manager-Datenschutz finden Sie unter [Sicherheit und Datenschutz für Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Sie können einige oder alle unterstützten Daten von einem Quellstandort zu einer Zielhierarchie migrieren.  

Die Migration ist in der Standardeinstellung nicht aktiviert und erfordert mehrere Konfigurationsschritte. Es werden keine Migrationsinformationen an Microsoft gesendet.  

Berücksichtigen Sie Ihre Datenschutzanforderungen, bevor Sie Daten aus einer Quellhierarchie migrieren.  
