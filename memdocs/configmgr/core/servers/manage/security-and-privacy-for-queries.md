---
title: Sicherheit und Datenschutz für Abfragen
titleSuffix: Configuration Manager
description: Verstehen Sie die bewährten Methoden für Sicherheit und Datenschutz beim Abfragen von Informationen aus der Standortdatenbank.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695698"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Sicherheit und Datenschutz bei Abfragen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In Configuration Manager können Sie Informationen aus der Standortdatenbank auf Basis der von Ihnen angegebenen Kriterien abrufen. Die Informationen zur Standortdatenbank werden von Configuration Manager während des Standardbetriebs gesammelt. Wenn Sie beispielsweise Informationen verwenden, die während der Suche oder der Inventur gesammelt wurden, können Sie eine Abfrage zum Identifizieren von Geräten konfigurieren, die bestimmte Kriterien erfüllen.  

 Weitere Informationen zu Abfragen finden Sie unter [Einführung in Abfragen in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Weitere Informationen zu bewährten Sicherheitsmethoden und Datenschutzinformationen zu Configuration Manager-Vorgängen, bei denen Informationen gesammelt werden, die Sie mithilfe von Abfragen abrufen können, finden Sie unter [Sicherheit und Datenschutz für Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Bewährte Sicherheitsmethoden für Abfragen

 Verwenden Sie die folgende bewährte Sicherheitsmethode für Abfragen.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Wenn Sie eine Abfrage exportieren oder importieren, die an einem Netzwerkspeicherort gespeichert ist, schützen Sie den Speicherort und den Netzwerkkanal.|Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.<br /><br /> Verwenden Sie zwischen Netzwerkspeicherort und Standortserver SMB-Signaturen (Server Message Block) bzw. IPsec (Internet Protocol-Sicherheit), um potenzielle Angreifer an der Manipulation der Abfragedaten vor dem Import zu hindern.|  

## <a name="next-steps"></a>Nächste Schritte
  
[Sicherheit und Datenschutz für Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
