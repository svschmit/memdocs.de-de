---
title: Koexistenz von Drittanbieter-MDM-Instanzen
titleSuffix: Configuration Manager
description: Informationen zur Verwendung eines MDM-Drittanbieterdiensts mit Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 055d79c56417135e2b08a31bc05a3ca30b5fd581
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695102"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Koexistenz von Drittanbieter-MDM-Instanzen mit Configuration Manager

Wenn Sie Windows 10-Geräte gleichzeitig mit Configuration Manager und Microsoft Intune verwalten, wird diese Funktionalität als [Co-Verwaltung](overview.md) bezeichnet. Wenn Sie Geräte mit Configuration Manager verwalten und sich bei einem MDM-Drittanbieterdienst registrieren, wird diese Funktionalität als *Koexistenz* bezeichnet. Zwei Verwaltungsstellen für ein einzelnes Gerät können eine Herausforderung darstellen, wenn zwischen den beiden Stellen keine ordnungsgemäße Orchestrierung besteht. Bei der Co-Verwaltung gleichen Configuration Manager und Intune die [Workloads](workloads.md) aus, um sicherzustellen, dass keine Konflikte auftreten. Diese Interaktion ist bei Drittanbietern nicht vorhanden, sodass es Einschränkungen bei den Verwaltungsfunktionen der Koexistenz gibt.

Der Configuration Manager-Client kann mit einem MDM-Drittanbieterdienst auf einem Gerät mit Windows 10, Version 1709 und höher, gleichzeitig vorhanden sein, das in Azure Active Directory eingebunden ist. Das Gerät kann einem der folgenden Typen angehören:

- [In Azure AD eingebunden](/azure/active-directory/devices/azureadjoin-plan) (ausschließlich). (Dieser Typ wird manchmal auch als „in die Clouddomäne eingebunden“ bezeichnet.)  

- [Hybrid und in die Domäne eingebunden](/azure/active-directory/devices/hybrid-azuread-join-plan), wobei das Gerät mit Ihrer lokalen Active Directory-Instanz verknüpft und bei Azure Active Directory registriert ist.  

> [!Note]  
> [Private Geräte](/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) werden nicht unterstützt.  

Wenn der Configuration Manager-Client erkennt, dass auch ein MDM-Drittanbieterdienst das Gerät verwaltet, deaktiviert er automatisch bestimmte Workloads in Configuration Manager. Dieses Verhalten ermöglicht es dem MDM-Dienst, diese Funktionen zu übernehmen. Es verhindert auch Einstellungskonflikte auf dem Client, die sich negativ auf das Gerät und die Benutzerfreundlichkeit auswirken könnten. Die folgenden Workloads in Configuration Manager werden in diesem Fall deaktiviert:

- Ressourcenzugriffsrichtlinien für VPN-, WLAN, E-Mail- und Zertifikateinstellungen
- Anwendungsverwaltung, einschließlich Legacypaketen
- Überprüfung auf Softwareupdates und deren Installation
- Endpoint Protection, die Windows Defender-Suite mit Antischadsoftware-Schutzfunktionen
- Compliance-Richtlinie für bedingten Zugriff
- Gerätekonfiguration
- Office-Klick-und-Los-Verwaltung

Der Configuration Manager-Client vermeidet Konflikte mit der Verwaltungsstelle des Drittanbieters, indem die folgenden schreibgeschützten Vorgänge fortgesetzt werden:

- Hardware- und Softwareinventur
- Asset Intelligence
- Softwaremessung
- Energieverwaltungsberichte

Weitere Informationen zu den Vorteilen der Co-Verwaltung mit Configuration Manager und Intune finden Sie unter [Vorteile](overview.md#benefits).