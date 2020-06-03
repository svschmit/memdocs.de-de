---
title: Die Entität „IntuneManagementExtension“
titleSuffix: Microsoft Intune
description: Referenzthema für die Entitätskategorie „IntuneManagementExtension“ von Entitätensammlungen in der Intune Data Warehouse-API.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: aac78143e2b1e15f7b718c70d2dc7168c00f8fd4
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165293"
---
# <a name="reference-for-intune-management-extensions"></a>Verweis für die Intune-Verwaltungserweiterungen

Die Kategorie **intuneManagementExtensions** enthält Entitäten für mobile Geräte zur Nachverfolgung von Informationen wie etwa der folgenden:

- Versionen einer IntuneManagementExtension
- Installationsstatus einer IntuneManagementExtension

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

Die Entität **intuneManagementExtensionVersion** listet alle von intuneManagementExtensions verwendeten Versionen auf.

| Eigenschaft  | Description | Beispiel |
|---------|------------|--------|
| extensionVersionKey |Eindeutiger Bezeichner für die intuneManagementExtensions-Version. | 1 |
| extensionVersion |Die vierstellige Versionsnummer |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

**intuneManagementExtensionHealthState** listet alle möglichen Status der intuneManagementExtensions auf.

| Eigenschaft  | Description | Beispiel |
|---------|------------|--------|
| extensionStateKey |Eindeutiger Bezeichner des Integritätszustands | 2 |
| extensionState |Der Integritätsstatus einer IntuneManagementExtension | Healthy |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

Die **intuneManagementExtensions** listet täglich den Integritätsstatus von intuneManagementExtension auf jedem Windows 10-Gerät auf.
Die Daten der letzten 60 Tage werden aufbewahrt. 


|      Eigenschaft       |                         Description                         | Beispiel |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Eindeutiger Datumsbezeichner                |   123   |
|      tenantKey      |              Eindeutiger Mandantenbezeichner               |   456   |
|      deviceKey      |              Eindeutiger Bezeichner des Geräts               |   789   |
| extensionVersionKey | Eindeutiger Bezeichner für die intuneManagementExtension-Version. |    1    |
|  extensionStateKey  |             Eindeutiger Bezeichner des Integritätszustands              |    2    |

