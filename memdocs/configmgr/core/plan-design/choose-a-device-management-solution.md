---
title: Wählen einer Geräteverwaltungslösung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Lösungen von Microsoft zum Verwalten von Computern, Servern und Geräten.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702268"
---
# <a name="choose-a-device-management-solution"></a>Wählen einer Geräteverwaltungslösung

Microsoft bietet verschiedene Lösungen für die Verwaltung von PCs, Servern und Geräten. Diese Lösungen stehen lokal, cloudbasiert sowie als Kombination dieser beiden Optionen zur Verfügung. Wählen Sie die Lösung aus, die sich für die Geschäftsanforderungen Ihrer Organisation am besten eignet. Treffen Sie Ihre Entscheidung abhängig von den zu verwaltenden Geräteplattformen und den benötigen Verwaltungsfunktionalitäten.

## <a name="overview"></a>Overview

Es gibt verschiedene Microsoft-Lösungen, die jeweils für unterschiedliche Szenarien geeignet sind. Sie müssen sich nicht auf eine Lösung beschränken.

- In kleinen Organisationen ist ein Tool wie das Windows Admin Center möglicherweise die beste Wahl.
- Etwa 75 % aller IT-Organisationen verwenden Configuration Manager für die Verwaltung ihrer Geräte.
- Microsoft Azure bietet verschiedene Lösungen sowohl in der Cloud als auch lokal mit Azure Stack, die primär auf die Serververwaltung abzielen.
- Microsoft Intune ermöglicht die Cloudverwaltung von Clients.
- Sie können Configuration Manager und Intune in einer Co-Verwaltungslösung kombinieren.

Mit der folgenden Tabelle können Sie diese Verwaltungstechnologien miteinander vergleichen:

|  | Nur Cloud | An die Cloud angefügt | Lokal | getrennt |
|---------|---------|---------|---------|---------|
| **Hyper-V-Host** | Nicht verfügbar | – Azure Stack<br/> – Windows Admin Center<br/> – Virtual Machine Manager | – Azure Stack<br/> – Windows Admin Center<br/> – Virtual Machine Manager | – Azure Stack<br/> – Windows Admin Center<br/> – Virtual Machine Manager |
| **Windows Server** | – Azure-Verwaltung<br/> – Configuration Manager | – Azure-Verwaltung<br/> – Configuration Manager | – Azure-Verwaltung<br/> – Configuration Manager | Configuration Manager |
| **Linux-Server** | – Azure-Verwaltung | – Azure-Verwaltung | – Azure-Verwaltung |  |
| **Windows 10** | – Intune<br/> – Configuration Manager | – Intune<br/> – Configuration Manager | – Intune<br/> – Configuration Manager | Configuration Manager |
| **Windows 7 oder 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | Nicht verfügbar | Nicht verfügbar | Nicht verfügbar |

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Was ist Azure Stack?](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [Was ist das Windows Admin Center?](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [Was ist Virtual Machine Manager?](https://docs.microsoft.com/system-center/vmm/overview)
- [Azure-Verwaltungsprodukte](https://docs.microsoft.com/azure/)
- [Was ist Windows Virtual Desktop?](https://docs.microsoft.com/azure/virtual-desktop/overview)

Weitere Informationen zu Lösungen mit Configuration Manager und Intune finden Sie im nächsten Abschnitt.

## <a name="client-management"></a>Clientverwaltung

In diesem Abschnitt werden die folgenden vier Lösungen für die Clientverwaltung verglichen:

- [Konfigurations-Manager-Client](#bkmk_sccm)
- [Lokale MDM mit Configuration Manager](#bkmk_opmdm)
- [Co-Verwaltung mit Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Sie können diese Lösungen eigenständig oder in Kombination miteinander verwenden. Verwenden Sie beispielsweise die clientbasierte Verwaltungslösung für die Verwaltung der Computer und Server in Ihrer Organisation und zusätzlich die Co-Verwaltung für die Verwaltung von internetbasierten Laptops. Durch diese Kombination können Sie alle Anforderungen der Geräteverwaltung abdecken.  

Unter den folgenden beiden Links finden Sie zwei Tabellen, in denen die Verwaltungslösungen anhand der entsprechenden Faktoren miteinander verglichen werden:

- [Vergleich anhand der unterstützten Plattformen](#bkmk_comp1)
- [Vergleich anhand der Verwaltungsfunktion](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a>Konfigurations-Manager-Client  

Für diese Option ist die Installation des Konfigurations-Manager-Clients auf Geräten erforderlich. Er stellt die meisten Features für die Verwaltung von Computern, Servern und anderen Geräten in Ihrer Umgebung bereit.

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationsmethoden](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Lokale Verwaltung mobiler Geräte  

Diese Option nutzt die in Windows 10 integrierten Geräteverwaltungsfunktionen. Die lokale mobile Geräteverwaltung (Mobile Data Management, MDM) bietet zwar nicht den vollen Funktionsumfang der clientbasierten Verwaltung, ist aber eine schlankere Verwaltungslösung. Sie verwendet lokale Configuration Manager-Ressourcen zum Verwalten von Geräten.  

Weitere Informationen finden Sie unter [Lokale MDM (Mobile Device Management) in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a>Co-Verwaltung mit Microsoft Intune

Die Co-Verwaltung ist eine der primären Möglichkeiten zum Anfügen Ihrer vorhandenen Configuration Manager-Bereitstellung an die Microsoft 365-Cloud. Dies ermöglicht Ihnen die gleichzeitige Verwaltung von Windows 10-Geräten mithilfe von Configuration Manager und Microsoft Intune. Mit der Co-Verwaltung können Sie Ihre vorhandenen Bereitstellungen in Configuration Manager mit der Cloud verknüpfen, indem Sie neue Funktionen hinzufügen.

Weitere Informationen finden Sie unter [What is co-management? (Was ist die Co-Verwaltung?)](../../comanage/overview.md).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a>Microsoft Exchange  

Diese Option verwendet den Exchange Server-Connector zum Verbinden mehrerer Exchange-Server mit Configuration Manager. Hiermit wird die Verwaltung von Geräten zentralisiert, die eine Verbindung mit Exchange ActiveSync herstellen können. Sie können Exchange-Features für die mobile Geräteverwaltung über die Configuration Manager-Konsole konfigurieren. Zu den Beispielfeatures gehören die Remotegerätezurücksetzung und die Steuerung der Einstellungen mehrerer Exchange-Server.

Weitere Informationen finden Sie unter [Verwalten von Mobilgeräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a>Vergleich der Lösungen anhand der unterstützten Plattformen  

|Plattform|Configuration Manager-Client|Lokale Verwaltung mobiler Geräte|Configuration Manager mit Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Ja| Ja |
|iOS| | |Ja| Ja |
|Mac OS X|Ja| |Ja| Ja |
|Windows-10|Ja|Ja|Ja| Ja |
|Windows 10 Mobile| |Ja|Ja| Ja |
|Windows (frühere Versionen)|Ja| |Ja|  |
|Windows Server|Ja| |Ja|  |
|Windows Embedded|Ja| | |  |

Eine vollständige Liste der unterstützten Plattformen finden Sie in den folgenden Artikeln:

- [Unterstützte Betriebssysteme für Clients und Geräte für Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Von Intune unterstützte Konfigurationen](https://docs.microsoft.com/intune/supported-devices-browsers)

Für die Verwaltung von mobilen Android-, iOS- und Windows 10-Geräten wird die Verwendung von Intune empfohlen. Weitere Informationen finden Sie unter [Was ist Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune).

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a>Vergleich der Lösungen anhand der Verwaltungsfunktion  

|Verwaltungsfunktion|Configuration Manager-Client|Lokale Verwaltung mobiler Geräte|Configuration Manager mit Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Zertifikatbasierte gegenseitige Authentifizierung|Ja|Ja| |
|Clientinstallation|Ja| | |
|Support über das Internet|Ja| | |
|-Ermittlung|Ja| |Ja|
|Hardwareinventur|Ja|Ja|Ja|
|Softwareinventur|Ja| |Ja|
|Einstellungen|Ja|Ja|Ja|
|Softwarebereitstellung|Ja|Ja| |
|Softwareupdateverwaltung|Ja| | |
|Bereitstellung des Betriebssystems|Ja| | |
|Blockieren von Configuration Manager aus|Ja|Ja| |
|Unter Quarantäne Stellen und Blockieren von Exchange Server (und Configuration Manager) aus| | |Ja|
|Remotezurücksetzung| |Ja|Ja|
