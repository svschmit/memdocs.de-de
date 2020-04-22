---
title: Clientintegrität mit Co-Verwaltung
titleSuffix: Configuration Manager
description: Verwalten der Sichtbarkeit von Configuration Manager-Clientintegrität über Intune im Azure-Portal
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690828"
---
# <a name="client-health-with-co-management"></a>Clientintegrität mit Co-Verwaltung

Die Integrität Ihres Netzwerks hängt direkt mit der Integrität der Geräte zusammen, die sich in das und aus dem Netzwerk bewegen. Intune kann mit einem nicht integren Client selbst dann kommunizieren, wenn er sich nicht in Ihrem Netzwerk befindet. Nutzen Sie die Co-Verwaltung, um diese Funktion mit der Fähigkeit von Configuration Manager zu kombinieren, 98 % der bekannten integren Clients zurückzumelden. Dann können Sie in Echtzeit alle Clients erkennen, auswerten und Sichtbarkeit schaffen. Intune fügt auch die Unterstützung hinzu, die für Complianceupgrades auf allen verbundenen Clients erforderlich ist.

Im folgenden Video erläutern und zeigen Senior Program Manager Rob York und Product Marketing Manager Locky Ainley die Integrität der Clients mit Co-Verwaltung:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Vorteile

Die Auswertung der Integrität von Clients besitzt höchste Priorität. In System Center 2012 Configuration Manager wurde **CCMeval** hinzugefügt. Dieses Hilfsprogramm ist für den Configuration Manager-Client extern. Es bietet Überwachung der Clientintegrität und automatische Bereinigung. Diese Berichterstellung basiert jedoch darauf, dass sich ein Gerät physisch oder virtuell in Ihrem internen Netzwerk befindet. Co-Verwaltung unterstützt Sie dabei, dieses Problem zu lösen.

Mit Co-Verwaltung kann Intune den Integritätszustand des Clients melden. Sie liefert Zeitstempelinformationen für die Gültigkeit der Daten. Diese Informationen zeigen Ihnen, ob Ihre Geräte integer sind, eine Verbindung herstellen können, Apps installieren oder ein Update auf die erforderlichen Betriebssystembuilds durchführen können. 

Eine ausführliche Übersicht über dieses Feature finden Sie in diesem Video zu [Neuerungen in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) aus einer Sitzung der Veranstaltung Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Wenn Configuration Manager als Gerätestatus angibt, dass der Client installiert ist, dies aber nicht der Fall ist, kann Intune weitere Informationen bereitstellen, ohne eine Verbindung mit dem Client herstellen zu müssen. Die Informationen zur Geräteintegrität in Intune sind leicht verständlich. Wenn der Status anders als **Fehlerfrei** ist, werden Empfehlungen und nächste Schritte für die Problembehandelung und Fehlerbehebung genannt.

> [!Note]  
> Die folgenden Vorteile sind für eine zukünftige Version geplant:
> - Configuration Manager wird zusätzliche Funktionen in CCMeval integrieren.  
> - Es wird einfacher sein, potenziell fehlerhafte Computer sowohl in Configuration Manager als auch in Intune zu identifizieren.  
> - Sie können die Daten zur Clientintegrität in Intune gruppieren.  



## <a name="value-proposition"></a>Leistungsversprechen

Mit diesem Feature verfügen Sie jetzt über eine externe Datenquelle mit Intune. Sie ermöglicht es Ihnen, die nächsten Schritte bei der Problembehandlung einer Vielzahl von Clientproblemen festzulegen. Jetzt müssen Sie keine zusätzlichen Berichte mehr erstellen oder andere Tools verwenden, um Clientdaten zurückzuziehen.

Wenn Sie über integre Clients verfügen, haben Sie die Patchcompliance problemlos aktualisiert. Bessere Patchcompliance bedeutet bessere Sicherheit.



## <a name="configure"></a>Konfigurieren

Verwenden Sie die folgenden Schritte, um erste Schritte mit dieser Funktion auszuführen:

- Aktualisieren der Geräte auf Windows 10, Version 1709 oder höher  

- [Aktivieren der Co-Verwaltung](how-to-enable.md)  
    - Sie müssen keine Workloads zu Intune verschieben.  

- Aktualisieren des Configuration Manager-Standorts und der Clients auf *Version 1806* oder höher  


### <a name="review-configuration-manager-client-health-in-intune"></a>Überprüfen der Configuration Manager-Clientintegrität in Intune

1. Melden Sie sich beim [Azure-Portals](https://portal.azure.com/)angemeldet sind.  

2. Wählen Sie **Alle Dienste** > **Intune**. Intune befindet sich im Abschnitt **Monitoring + Management**.  

3. Nachdem Sie den Bereich **Microsoft Intune** geöffnet haben, navigieren Sie im Menü unter **Hilfe und Support** zur Seite **Problembehandlung**.  

4. Verwenden Sie die Option **Benutzer auswählen**, suchen Sie das jeweilige Gerät in der Liste **Geräte**, und wählen sie es aus, um die Geräteseite zu öffnen.  

5. Informationen zur Co-Verwaltung werden am unteren Rand der Geräteseite angezeigt. Diese Informationen umfassen die folgenden Felder für die Clientintegrität:  
    - **Zustand des Configuration Manager-Agents**  
    - **Letzte Eincheckzeit des Configuration Manager-Agents**  

> [!Tip]  
> Intune-registrierte Geräte stellen drei Mal täglich (etwa alle acht Stunden) eine Verbindung mit dem Clouddienst her. 
