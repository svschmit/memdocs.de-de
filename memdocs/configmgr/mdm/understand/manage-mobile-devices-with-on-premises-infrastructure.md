---
title: Lokale Verwaltung mobiler Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724674"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Lokale Verwaltung mobiler Geräte (MDM) in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) ist eine Geräte Verwaltungs Lösung, die von den integrierten Verwaltungsfunktionen von Windows abhängig ist. Dieses Feature basiert auf dem Open Mobile Alliance (OMA) Device Management (DM)-Standard. Es verwendet die Configuration Manager Infrastruktur Ihres Unternehmens, um die Geräte zu verwalten und zu warten. Ihre Organisation erfordert Microsoft InTune Lizenzen, um dieses Feature verwenden zu können, erfordert aber keine cloudverbindung. In Configuration Manager werden alle Daten zu Ihren Geräten in der lokalen Standortdatenbank gespeichert.

Die lokale Verwaltung mobiler Geräte unterscheidet sich von Microsoft InTune, das auch auf integrierten OMA DM-Funktionen basiert. Alle Verwaltungsfunktionen in InTune werden über Clouddienste bereitgestellt. Die lokale Verwaltung mobiler Geräte unterscheidet sich auch von der Client basierten Verwaltungs Lösung, die traditionell von Configuration Manager angeboten wird. Es basiert auf einer ähnlichen Infrastruktur, verwendet jedoch keine separat installierte Client Software auf den Geräten, die Sie verwaltet.  

## <a name="comparison"></a>Vergleich

In den folgenden Abschnitten werden die vor-und Nachteile der lokalen MDM im Vergleich zur herkömmlichen Client basierten Verwaltung aufgelistet:  

### <a name="advantages"></a>Vorteile

- **Vereinfachte Infrastruktur**: weniger Standortsystem Rollen sind erforderlich.

- **Einfacher zu**verwalten: da Verwaltungsfunktionen auf dem Betriebssystem des Geräts integriert sind, sind neue Versionen des Configuration Manager Clients nicht erforderlich, wenn neue Verwaltungsfunktionen für den Standort eingeführt werden.

- **Lokal**:-die gesamte Verwaltung und die Daten werden lokal aufbewahrt.

### <a name="disadvantages"></a>Nachteile

**Weniger Client Verwaltungsfunktionen**: keine Orchestrierung, Software Messung, Integration von Drittanbietern, Task Sequenzierung oder Software Center Unterstützung.

- **Eingeschränkte Geräte Unterstützung**: die lokale MDM unterstützt nicht so viele Betriebssystemversionen wie der Configuration Manager Client. Weitere Informationen finden Sie unter [Unterstützte Betriebssystemversionen für Clients und Geräte](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="next-step"></a>Nächster Schritt

Informieren Sie sich darüber, was beim Einrichten der Configuration Manager Infrastruktur und der Planung der Geräteregistrierung bei der lokalen Verwaltung von MDM zu beachten ist.

> [!div class="nextstepaction"]
> [Planen für die lokale Verwaltung mobiler Geräte (MDM)](../plan-design/plan-on-premises-mdm.md)  
