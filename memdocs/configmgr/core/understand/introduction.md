---
title: Was ist Configuration Manager?
titleSuffix: Configuration Manager
description: Lernen Sie die Grundlagen von Microsoft Endpoint Configuration Manager kennen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99e02c190e02a5e017fe2c3f41682ad1624b6051
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699346"
---
# <a name="what-is-configuration-manager"></a>Was ist Configuration Manager?

*Gilt für: Configuration Manager (Current Branch)*

Ab Version 1910 ist Configuration Manager Bestandteil von Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager ist eine integrierte Lösung für die Verwaltung all Ihrer Geräte. Microsoft vereint damit Configuration Manager und Intune ohne komplexe Migration und mit vereinfachter Lizenzierung. Nutzen Sie weiterhin ihre bestehenden Investitionen in Configuration Manager, und profitieren Sie von der Leistungsfähigkeit der Microsoft-Cloud nach Ihren Vorgaben.

Die folgenden Microsoft-Verwaltungslösungen sind nun unter dem Namen **Microsoft Endpoint Manager** vereint:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Weitere Features in der [Verwaltungskonsole für die Geräteverwaltung](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Weitere Informationen finden Sie unter [Microsoft Endpoint Configuration Manager FAQ](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Einführung

Verwenden Sie Configuration Manager als Unterstützung für folgende Systemverwaltungsaktivitäten:

- Steigern der IT-Produktivität und -Effizienz durch weniger manuelle Aufgaben und Fokussierung auf wertschöpfende Projekte  
- Maximieren des Nutzens von Hardware- und Softwareinvestitionen  
- Steigern der Benutzerproduktivität durch die richtige Software zum richtigen Zeitpunkt  

Configuration Manager unterstützt Sie wie folgt bei der Bereitstellung effizienterer IT-Dienste:

- Sichern und skalierbare Bereitstellung der Anwendungen, der Softwareupdates und der Betriebssysteme
- Echtzeitaktionen auf verwalteten Geräten
- Cloudgestützte Analyse und Verwaltung für lokale und internetbasierte Geräte
- Verwaltung von Konformitätseinstellungen  
- Umfassende Verwaltung von Servern, Desktops und Laptops

Configuration Manager erweitert Technologien und Lösungen von Microsoft und arbeitet reibungslos mit diesen zusammen. Configuration Manager arbeitet z.B. mit folgenden Komponenten zusammen:  

- Microsoft Intune zur gemeinsamen Verwaltung zahlreicher Plattformen für mobile Geräte
- Microsoft Azure zum Hosten von Clouddiensten zur Erweiterung der Verwaltungsdienste
- Windows Server Update Services (WSUS) zur Verwaltung von Softwareupdates
- Zertifikatdienste
- Exchange Server und Exchange Online
- Gruppenrichtlinie
- DNS
- Windows Automated Deployment Kit (Windows ADK) und Migrationstool für den Benutzerstatus (USMT)
- Windows-Bereitstellungsdienste (Windows Deployment Services, WDS)
- Remotedesktop und Remoteunterstützung

Configuration Manager verwendet auch:  

- Active Directory Domain Services für die Sicherheit, Dienstidentifizierung und Konfiguration sowie zur Ermittlung von Benutzern und Geräten, die Sie verwalten möchten  
- Microsoft SQL Server als verteilte Änderungsmanagementdatenbank. Durch die Integration in SQL Server Reporting Services (SSRS) werden Berichte zur Überwachung und Nachverfolgung von Verwaltungsaktivitäten erstellt.  
- Standortsystemrollen, die Verwaltungsfunktionen erweitern und die Webdienste von Internetinformationsdiensten (Information Services, IIS) verwenden.
- Übermittlungsoptimierung, Windows Low Extra Delay Background Transport (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache und andere Peerchachingtechnologien zur Unterstützung bei der Verwaltung von Inhalt in Ihren Netzwerken und zwischen Ihren Geräten

Damit Sie Configuration Manager in einer Produktionsumgebung erfolgreich verwenden können, müssen Sie einen detaillierten Plan aufstellen und die Verwaltungsfunktionen sorgfältig testen. Configuration Manager ist eine leistungsfähige Verwaltungsanwendung, die sich potenziell auf jeden Computer in Ihrer Organisation auswirken kann. Durch eine Bereitstellung und Verwaltung von Configuration Manager bei sorgfältiger Planung und Berücksichtigung Ihrer Unternehmensanforderungen können Sie mithilfe von Configuration Manager Ihren Verwaltungsaufwand und die Gesamtbetriebskosten beträchtlich senken.  

## <a name="user-interfaces"></a>Benutzeroberflächen

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Die Configuration Manager-Konsole

Nach der Installation von Configuration Manager, verwenden Sie die Configuration Manager-Konsole, um Standorte und Clients zu konfigurieren und Verwaltungstasks auszuführen und zu überwachen. Diese Konsole ist die zentrale Verwaltungsschnittstelle, über die Sie mehrere Standorte verwalten können.  

Sie können die Configuration Manager-Konsole auf zusätzlichen Computern installieren, mithilfe der rollenbasierten Verwaltung in Configuration Manager den Zugriff beschränken und die Elemente begrenzen, die Administratoren angezeigt werden.  

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> Softwarecenter

**Softwarecenter** ist eine Anwendung, die installiert wird, wenn Sie den Configuration Manager-Client auf einem Windows-Gerät installieren. Benutzer verwenden das Softwarecenter, um Software anzufordern und zu installieren, die Sie bereitstellen. Mithilfe des Softwarecenters können Benutzer folgende Aktionen ausführen:  

- Suchen nach und Installieren von Anwendungen, Softwareupdates und neuen Betriebssystemversionen
- Anzeigen ihres Softwareanforderungsverlaufs
- Anzeigen der Gerätekonformität anhand der Richtlinien Ihrer Organisation

Sie können auch benutzerdefinierte Registerkarten im Softwarecenter anzeigen, um zusätzliche Geschäftsanforderungen zu erfüllen.

Weitere Informationen finden Sie im [Benutzerleitfaden für Softwarecenter](software-center.md).

## <a name="next-steps"></a>Nächste Schritte

Machen Sie sich vor der Installation von Configuration Manager mit einigen grundlegenden Konzepten und Begriffen vertraut:

- Wenn Sie mit System Center 2012 Configuration Manager vertraut sind, beginnen Sie mit [Änderungen von System Center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Einen grundlegenden technischen Überblick über Configuration Manager finden Sie unter [Grundlagen von System Center Configuration Manager](fundamentals.md).

Wenn Sie mit den grundlegenden Konzepten vertraut sind, finden Sie in der Dokumentationsbibliothek hilfreiche Informationen zur erfolgreichen Bereitstellung und Verwendung von Configuration Manager. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Features und Funktionen von Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Wählen einer Geräteverwaltungslösung](../plan-design/choose-a-device-management-solution.md)  
- [Bewerten von Configuration Manager durch Erstellen Ihrer eigenen Laborumgebung](../get-started/set-up-your-lab.md)
- [Suchen nach Hilfe für die Verwendung von Configuration Manager](find-help.md)