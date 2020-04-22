---
title: Sicherheit und Datenschutz für die Energieverwaltung
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu Sicherheit und Datenschutz für die Energieverwaltung in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696508"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Sicherheit und Datenschutz für die Energieverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Abschnitt enthält Informationen zu Sicherheit und Datenschutz für die Energieverwaltung in Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Bewährte Sicherheitsmethoden für die Energieverwaltung  
 Für die Energieverwaltung sind keine bewährten Sicherheitsmethoden vorhanden.  

## <a name="privacy-information-for-power-management"></a>Informationen zum Datenschutz für die Energieverwaltung  
 Power Management verwendet Features, die in Windows den Energieverbrauch überwachen und zum Anwenden von energieeinstellungen auf Computern während der Geschäftszeiten und Geschäftszeiten integriert sind. Configuration Manager sammelt Informationen zum Energieverbrauch von Computern, beispielsweise auch zu den Computernutzungszeiten von Benutzern. Obwohl von Configuration Manager nur der Energieverbrauch einer Sammlung und nicht jedes Computers überwacht wird, ist es möglich, eine Sammlung mit nur einem Computer zu überwachen. Die Energieverwaltung ist standardmäßig nicht aktiviert und muss von einem Administrator konfiguriert werden.  

 Die Informationen zum Energieverbrauch werden in der Configuration Manager-Datenbank gespeichert und nicht an Microsoft gesendet. Ausführliche Informationen werden 31 Tage in der Datenbank gespeichert, zusammengefasste Informationen 13 Monate. Das Löschintervall kann nicht konfiguriert werden.  

 Berücksichtigen Sie beim Konfigurieren der Energieverwaltung Ihre Datenschutzanforderungen.  
