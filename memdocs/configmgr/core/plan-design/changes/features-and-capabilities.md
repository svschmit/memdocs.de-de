---
title: Features und Funktionen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die primären Verwaltungsfunktionen von Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706398"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Features und Funktionen von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel fasst die wichtigsten Verwaltungsfunktionen von Configuration Manager zusammen. Für jede Funktion gelten individuelle Voraussetzungen, und die Art und Weise, wie Sie jede einzelne Funktion verwenden, kann sich auf den Entwurf und die Implementierung Ihrer Configuration Manager-Hierarchie auswirken. Wenn Sie beispielsweise Softwareupdates auf Geräten in Ihrer Hierarchie bereitstellen möchten, benötigen Sie einen Softwareupdatepunkt der Standortsystemrolle.  

Weitere Informationen zum Planen und Installieren von Configuration Manager zur Unterstützung dieser Verwaltungsfunktionen in Ihrer Umgebung finden Sie unter [Vorbereiten auf Configuration Manager](../get-ready.md).  

## <a name="co-management"></a>Co-Verwaltung

Die Co-Verwaltung ist eine der primären Möglichkeiten zum Anfügen Ihrer vorhandenen Configuration Manager-Bereitstellung an die Microsoft 365-Cloud. Dies ermöglicht Ihnen die gleichzeitige Verwaltung von Windows 10-Geräten mithilfe von Configuration Manager und Microsoft Intune. Mit der Co-Verwaltung können Sie Ihre vorhandenen Bereitstellungen in Configuration Manager mit der Cloud verknüpfen, indem Sie neue Funktionen wie bedingten Zugriff hinzufügen. Weitere Informationen finden Sie unter [Was ist die Co-Verwaltung?](../../../comanage/overview.md)

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics ist ein cloudbasierter Dienst, der in Configuration Manager integriert ist. Der Dienst bietet Einblicke und Informationen, mit denen Sie fundiertere Entscheidungen zur Updatebereitschaft Ihrer Windows-Clients treffen können. Er kombiniert Daten aus Ihrer Organisation mit Daten, die von Millionen von mit Microsoft-Clouddiensten verbunden Geräten aggregiert wurden. Weitere Informationen finden Sie unter [Was ist Desktop Analytics?](../../../desktop-analytics/overview.md)

## <a name="cloud-attached-management"></a>Cloudgestützte Verwaltung

Verwenden Sie Features wie Cloud Management Gateway, cloudbasierte Verteilungspunkte und Azure Active Directory, um internetbasierte Clients zu verwalten.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Verwalten von Clients im Internet](../../clients/manage/manage-clients-internet.md)
- [Vorbereitung auf Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Azure-Dienste](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Verwaltung in Echtzeit

Verwenden Sie CMPivot, um eine sofortige Abfrage von Onlinegeräten durchzuführen, und filtern und gruppieren Sie die Daten, um umfassendere Erkenntnisse zu gewinnen. Verwenden Sie auch die Configuration Manager-Konsole, um Windows PowerShell-Skripts zu verwalten und auf Clients bereitzustellen. Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md) und [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Anwendungsverwaltung

Diese Funktion unterstützt Sie bei der Erstellung, Verwaltung, Bereitstellung und Überwachung von Anwendungen auf mehreren verschiedenen Geräten, die Sie verwalten. Stellen Sie Office 365 über die Configuration Manager-Konsole bereit, aktualisieren und verwalten Sie Office 365 auch darüber. Darüber hinaus ist Configuration Manager in den Microsoft Store für Unternehmen und Bildungseinrichtungen integriert, um cloudbasierte Anwendungen bereitzustellen. Weitere Informationen finden Sie unter [Einführung in die Anwendungsverwaltung](../../../apps/understand/introduction-to-application-management.md).

## <a name="os-deployment"></a>Bereitstellung des Betriebssystems

Stellen Sie ein direktes Upgrade von Windows 10 bereit, oder erfassen und stellen Sie Betriebssystemimages bereit. Bei der Bereitstellung von Images können PXE-, Multicast- oder startbare Medien verwendet werden. Die Bereitstellung kann auch dabei helfen, vorhandene Geräte mit Windows AutoPilot neu bereitzustellen. Weitere Informationen finden Sie unter [Einführung in die Bereitstellung des Betriebssystems](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Softwareupdates

Verwalten, überwachen und stellen Sie Softwareupdates in der Organisation bereit. Integrieren Sie diese in die Windows Update-Übermittlungsoptimierung und andere Peercachingtechnologien, um die Netzwerkverwendung zu kontrollieren. Weitere Informationen finden Sie unter [Einführung in Softwareupdates](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Zugriff auf Unternehmensressourcen

Hiermit wird Ihnen ermöglicht, Benutzern in Ihrer Organisation Zugriff auf Daten und Anwendungen von Remotespeicherorten zu gewähren. Diese Funktion enthält WLAN-, VPN-, E-Mail- und Zertifikatsprofile. Weitere Informationen finden Sie unter [Schützen der Daten und der Standortinfrastruktur](../../../protect/understand/protect-data-and-site-infrastructure.md).

## <a name="compliance-settings"></a>Kompatibilitätseinstellungen

Diese helfen Ihnen bei der Bewertung, Verfolgung und Behebung der Konfigurationskonformität von Client-Geräten in Ihrer Organisation. Darüber hinaus können Sie Konformitätseinstellungen verwenden, um eine Reihe von Features und Sicherheitseinstellungen auf Geräten zu konfigurieren, die Sie verwalten. Weitere Informationen finden Sie unter [Sicherstellen der Gerätekonformität](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Endpoint Protection

Zu dieser Funktion gehören Verwaltungsfunktionen für Sicherheit, Antischadsoftware und Windows-Firewall für Computer in Ihrer Organisation. Dieser Bereich umfasst die Verwaltung und Integration mit den folgenden aufgelisteten Funktionen von Windows Defender:

- Windows Defender Antivirus
- Microsoft Defender Advanced Threat Protection
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Windows Defender Application Control
- Windows Defender Firewall

Weitere Informationen finden Sie unter [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Inventarisierung

Diese hilft Ihnen dabei, Ressourcen zu identifizieren und zu überwachen.

### <a name="hardware-inventory"></a>Hardwareinventur

Mit dieser Funktion werden detaillierte Informationen zur Hardware der Geräte in Ihrer Organisation gesammelt. Weitere Informationen finden Sie unter [Einführung in die Hardwareinventur](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Softwareinventur

Mit dieser Funktion werden Informationen zu den auf Clientcomputern Ihrer Organisation gespeicherten Dateien gesammelt und entsprechende Berichte erstellt. Weitere Informationen finden Sie unter [Einführung in die Softwareinventur](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Asset Intelligence

Zu dieser Funktion gehören Tools zum Sammeln von Inventurdaten und zur Überwachung von Softwarelizenzen in Ihrer Organisation. Weitere Informationen finden Sie unter [Einführung in Asset Intelligence in Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

## <a name="on-premises-mobile-device-management"></a>Lokale Verwaltung mobiler Geräte

Hiermit werden Geräte durch die lokale Configuration Manager-Infrastruktur registriert und verwaltet, bei der die Verwaltungsfunktionen in die Geräteplattformen integriert sind. (Bei der typischen Verwaltung wird ein separat installierter Configuration Manager-Client verwendet.) Derzeit wird die Verwaltung von Windows 10 Enterprise- und Windows 10 Mobile-Geräten durch diese Funktion unterstützt. Weitere Informationen finden Sie unter [Lokale MDM (Mobile Device Management) in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="power-management"></a>Energieverwaltung

Verwalten und überwachen Sie den Stromverbrauch von Clientcomputern in Ihrer Organisation. Konfigurieren Sie Energiesparpläne, und verwenden Sie Wake-on-LAN, um die Wartung außerhalb der Geschäftszeiten durchzuführen. Weitere Informationen finden Sie unter [Einführung in die Energieverwaltung](../../clients/manage/power/introduction-to-power-management.md).  

## <a name="remote-control"></a>Remotesteuerung

Stellt Tools zur Remoteverwaltung von Clientcomputern über die Configuration Manager-Konsole bereit. Weitere Informationen finden Sie unter [Einführung in die Remotesteuerung](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Berichterstellung

Verwenden Sie die erweiterten Berichterstellungsfunktionen von SQL Server Reporting Services über die Configuration Manager-Konsole. Diese Funktion stellt Hunderte von Standardberichten bereit. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../servers/manage/introduction-to-reporting.md).  

## <a name="software-metering"></a>Softwaremessung

Überwachen und sammeln Sie Softwarenutzungsdaten von Configuration Manager-Clients. Anhand dieser Daten können Sie bestimmen, ob nach der Installation Software verwendet wird. Weitere Informationen finden Sie unter [Monitor app usage with software metering (Überwachen der App-Nutzung mit der Softwaremessung)](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
