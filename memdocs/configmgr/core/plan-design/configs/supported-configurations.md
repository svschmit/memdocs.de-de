---
title: Unterstützte Konfigurationen
titleSuffix: Configuration Manager
description: Identifizieren Sie wichtige Konfigurationen und Anforderungen, damit Sie eine funktionierende Bereitstellung von Configuration Manager planen, bereitstellen und verwalten können.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66770ea14c3ae53bad8e6df61b54c7c5e2d2aaa0
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904572"
---
# <a name="supported-configurations-for-configuration-manager"></a>Unterstützte Konfigurationen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Als lokale Lösung verwendet Configuration Manager Ihre Server, Clients, Netzwerkkonfigurationen und zusätzliche Produkte wie Microsoft Intune, SQL Server und Azure.

Die Informationen in diesem und den folgenden Themen sind entscheidend, um wichtige Konfigurationen, Anforderungen und Einschränkungen zu identifizieren, damit Sie eine funktionierende Bereitstellung von Configuration Manager planen, bereitstellen und verwalten können.  Diese Informationen sind für die Infrastruktur von Configuration Manager-Standorten, Hierarchien und verwalteten Geräten spezifisch.

Wenn eine Configuration Manager-Funktion spezifischere Konfigurationen erfordert, werden diese Informationen in die funktionsspezifische Dokumentation aufgenommen und ergänzen diese allgemeineren Konfigurationsdetails.  

 Die in den folgenden Abschnitten beschriebenen Produkte und Technologien werden von Configuration Manager unterstützt. Die Tatsache, dass diese Produkte und Technologien hier beschrieben werden, bedeutet jedoch nicht, dass damit der Support über den Support Lifecycle der jeweiligen Produkte hinaus erweitert wurde. Produkte, deren Supportlebenszyklus abgelaufen ist, werden für die Verwendung mit Configuration Manager nicht mehr unterstützt. Dies umfasst alle Produkte, die durch das Programm [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) abgedeckt sind. Weitere Informationen zum Microsoft Support Lifecycle finden Sie auf der Website [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). Weitere Informationen zu Extended Security Updates in Configuration Manager finden Sie unter [Unterstützte Betriebssystemversionen für Clients und Geräte für Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]  
>  Informationen zur Microsoft Support Lifecycle-Richtlinie finden Sie auf der Website mit häufig gestellten Fragen zur Microsoft Support Lifecycle-Richtlinie unter [Microsoft Support Lifecycle-Richtlinie – Häufig gestellte Fragen (FAQs)](https://support.microsoft.com/lifecycle).  

 Darüber hinaus werden Produkte und Produktversionen, die in den folgenden Themen nicht aufgeführt sind, nicht von Configuration Manager unterstützt, außer dies wurde im [Blog für Enterprise Mobility und Security](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity) angekündigt.  Der Inhalt in diesem Blog wird von Zeit zu Zeit einer Aktualisierung an dieser Stelle der Dokumentation vorangestellt.


-  [Size and scale numbers (Anpassen und Skalieren von Zahlen)](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Erfahren Sie, wie viele Standorte, Standortsystemrollen pro Standort sowie Clients oder Geräte in verschiedenen Hierarchieentwürfen für Configuration Manager unterstützt werden.

-  [Voraussetzungen für Standorte und Standortsysteme](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Erfahren Sie mehr über Konfigurationen, die auf einem Windows Server zur Unterstützung der verschiedenen Standorttypen und Standortsystemrollen erforderlich sind.

-  [Unterstützte Betriebssysteme für Standortsystemserver](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Erfahren Sie, welche Betriebssysteme Sie als Standortserver oder Standortsystemserver verwenden können.

-  [Unterstützte Betriebssysteme für Clients und Geräte](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Erfahren Sie, welche Betriebssysteme Sie mit Configuration Manager verwalten können, einschließlich Windows, Windows Embedded, Linux und UNIX, Mac und mobile Geräte.

-  [Unterstützte Betriebssysteme für die Konsole](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Erfahren Sie, welche Betriebssysteme die Configuration Manager-Konsole als Zugriffspunkt zum Verwalten der Bereitstellung hosten können.  

-  [Unterstützung für SQL Server-Versionen](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Erfahren Sie, welche Versionen von SQL Server die Standortdatenbank und Berichtsdatenbank hosten und welche erforderlichen Konfigurationen und optionalen Konfigurationen Sie verwenden können.

-  [Optionen für hohe Verfügbarkeit](../../servers/deploy/configure/high-availability-options.md)  
Erfahren Sie mehr über die Optionen, die Sie bei der Entwicklung Ihrer Umgebung implementieren können, um einen hoch verfügbaren Dienst für Ihre Configuration Manager-Bereitstellung aufrechtzuerhalten.

-  [Empfohlene Hardware](../../../core/plan-design/configs/recommended-hardware.md)  
Erfahren Sie mehr über Richtlinien, die Ihnen helfen, die richtige Hardware und die richtigen Konfigurationen zum Hosten Ihrer Configuration Manager-Standorte und wichtigen Dienste zu identifizieren.

-  [Unterstützung für Active Directory-Domänen](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Erfahren Sie mehr über die unterstützten Active Directory-Domänenkonfigurationen, die Configuration Manager erfordert und unterstützt.

-  [Unterstützung für Windows-Features und Netzwerke](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Erfahren Sie mehr über unterstützte Windows-Technologien (wie z.B. BranchCache und Datendeduplizierung) und Einschränkungen für die Verwendung mit Configuration Manager.

-  [Unterstützung für Virtualisierungsumgebungen](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Erfahren Sie mehr über die Verwendung unterstützter Technologien virtueller Computer.
