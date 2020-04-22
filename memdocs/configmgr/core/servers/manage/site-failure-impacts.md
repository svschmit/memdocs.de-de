---
title: Auswirkungen von Standortausfällen
titleSuffix: Configuration Manager
description: Grundlegendes zu den Auswirkungen verschiedener Ausfälle an einem Configuration Manager-Standort.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708568"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Auswirkungen von Standortausfällen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Der Standortserver sowie jedes der anderen Standortsysteme kann ausfallen und einen Verlust der Dienste verursachen, die normalerweise von ihm bereitgestellt werden. Wenn Sie mehrere Standortsysteme auf demselben Computer installieren und dieser Computer ausfällt, ist keiner der Dienste mehr verfügbar, die üblicherweise von diesen Standortsystemen bereitgestellt werden.

Sie sollten in Ihren Planungsprozess Grundlegendes zu den Auswirkungen eines für Ihre Organisation bereitgestellten Diensts einschließen. Da jedes Standortsystem innerhalb des Standorts eine unterschiedliche Aufgabe hat, ergeben sich je nach ausgefallenem Standortsystem unterschiedliche Auswirkungen. 

Mithilfe von [Optionen für Hochverfügbarkeit](../deploy/configure/high-availability-options.md) können Sie die Ausfälle auf einem einzelnen System verringern. Darüber hinaus sollten Sie eine Strategie zur [Sicherung und Wiederherstellung](backup-and-recovery.md) planen und üben, um die Zeitspanne zu reduzieren, in der der Dienst nicht verfügbar ist.

In den folgenden Abschnitten werden die Auswirkungen beschrieben, wenn das angegebene Standortsystem nicht betriebsbereit ist:


### <a name="site-server"></a>Standortserver

- Es ist keine Standortverwaltung möglich. Die Konsole kann nicht mit dem Standort verbunden werden.  

- Der Verwaltungspunkt erfasst Clientdaten und speichert sie zwischen, bis der Standortserver wieder online ist.  

- Benutzer können vorhandene Bereitstellungen ausführen, und Clients können Inhalte von Verteilungspunkten herunterladen.  


### <a name="site-database"></a>Standortdatenbank

- Es ist keine Standortverwaltung möglich.  

- Verfügt der Konfigurations-Manager-Client bereits über eine Richtlinienzuweisung mit neuen Richtlinien, und hat der Verwaltungspunkt den Richtlinientext zwischengespeichert, kann der Client eine Anforderung nach dem Richtlinientext erstellen und die entsprechende Antwort empfangen. Der Standort kann jedoch keine neuen Anforderungen zur Richtlinienzuweisung bedienen.  

- Clients können Bereitstellungen nur ausführen, wenn sie die Richtlinie bereits empfangen haben und die zugehörigen Quelldateien bereits lokal auf dem Client zwischengespeichert wurden.  


### <a name="management-point"></a>Verwaltungspunkt

- Obwohl Sie neue Bereitstellungen erstellen können, empfangen Clients diese erst, wenn ein Verwaltungspunkt online ist.  

- Clients können weiterhin Inventur sammeln, Softwaremessungen durchführen und Statusinformationen anzeigen. Sie speichern diese Daten lokal, bis der Verwaltungspunkt verfügbar ist.  

- Clients können Bereitstellungen nur ausführen, wenn sie die Richtlinie bereits empfangen haben und die zugehörigen Quelldateien bereits lokal auf dem Client zwischengespeichert wurden.  


### <a name="distribution-point"></a>Verteilungspunkt

- Konfigurations-Manager-Clients können Bereitstellungen nur dann ausführen, wenn die zugehörigen Quelldateien bereits lokal heruntergeladen wurden oder in einer Peerquelle verfügbar sind.

