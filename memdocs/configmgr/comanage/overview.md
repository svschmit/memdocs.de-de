---
title: Co-Verwaltung für Windows 10-Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows 10-Geräte mithilfe von Configuration Manager und Microsoft Intune gleichzeitig verwalten können.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/01/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: f9e1809447f8d8ea8f6e0382575b71bfdec71fac
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695051"
---
# <a name="what-is-co-management"></a>Was ist Co-Verwaltung?

<!-- 1350871 -->
Die Co-Verwaltung ist eine der primären Möglichkeiten zum Anfügen Ihrer vorhandenen Configuration Manager-Bereitstellung an die Microsoft 365-Cloud. Damit können weitere cloudgestützte Funktionen wie bedingten Zugriff entsperren.

Co-Verwaltung ermöglicht Ihnen die gleichzeitige Verwaltung von Windows 10-Geräten mithilfe von Configuration Manager und Microsoft Intune. Mit ihr können Sie Ihre vorhandenen Bereitstellungen in Configuration Manager mit der Cloud verknüpfen, indem Sie neue Funktionen hinzufügen. Durch die Verwendung von Co-Verwaltung haben Sie die Flexibilität, die Technologielösung zu nutzen, die für Ihr Unternehmen am besten geeignet ist.

Wenn ein Windows 10-Gerät über den Configuration Manager-Client verfügt und bei Intune angemeldet ist, können Sie die Vorteile beider Dienste nutzen. Sie steuern, für welche Workloads (sofern vorhanden) die Verantwortung von Configuration Manager auf Intune übergeht. Configuration Manager verwaltet weiterhin alle anderen Workloads (einschließlich der Workloads, die Sie nicht an Intune übergeben) und alle anderen Funktionen von Configuration Manager, die die Co-Verwaltung nicht unterstützt.

Sie können auch eine Workload mit einer separaten Sammlung von Geräten als Pilotversuch steuern. Mit einem Pilotversuch können Sie die Intune-Funktionalität mit einer Teilmenge von Geräten testen, bevor Sie sie für eine größere Gruppe verwenden.

![Übersichtsdiagramm zur Co-Verwaltung](media/co-management-overview.svg)

[Diagramm in voller Größe anzeigen](media/co-management-overview.svg)

> [!Note]  
> Wenn Sie Windows 10-Geräte gleichzeitig mit Configuration Manager und Microsoft Intune verwalten, wird diese Konfiguration als *Co-Verwaltung* bezeichnet. Wenn Sie Geräte mit Configuration Manager verwalten und sich bei einem MDM-Drittanbieterdienst registrieren, wird diese Konfiguration als *Koexistenz* bezeichnet. Zwei Verwaltungsstellen für ein einzelnes Gerät können eine Herausforderung darstellen, wenn zwischen den beiden Stellen keine ordnungsgemäße Orchestrierung besteht. Bei der Co-Verwaltung gleichen Configuration Manager und Intune die [Workloads](#workloads) aus, um sicherzustellen, dass keine Konflikte auftreten. Diese Interaktion ist bei Drittanbietern nicht vorhanden, sodass es Einschränkungen bei den Verwaltungsfunktionen der Koexistenz gibt. Weitere Informationen finden Sie unter [Koexistenz von Drittanbieter-MDM-Instanzen mit Configuration Manager](coexistence.md).

## <a name="paths-to-co-management"></a>Pfade zur Co-Verwaltung

Es gibt zwei Möglichkeiten, die Co-Verwaltung zu realisieren:  

- **Vorhandene Configuration Manager-Clients**: Sie verfügen über Windows 10-Geräte, die bereits Configuration Manager-Clients sind. Sie richten Hybrid-Azure AD ein und registrieren sie bei Intune.  

- **Neue internetbasierte Geräte**: Sie verfügen über neue Windows 10-Geräte, die in Azure AD eingebunden werden und sich automatisch bei Intune registrieren. Sie installieren den Configuration Manager-Client, um einen Co-Verwaltungsstatus zu erreichen.  

Weitere Informationen zu den Pfaden finden Sie unter [Pfade für Co-Verwaltung](quickstart-paths.md).

## <a name="benefits"></a>Vorteile

Wenn Sie vorhandene Configuration Manager-Clients in der Co-Verwaltung registrieren, erzielen Sie die folgende unmittelbare Wertsteigerung:  

- Bedingter Zugriff mit Gerätekonformität  

- Intune-basierte Remoteaktionen, z.B. Neustart, Remotesteuerung oder Zurücksetzung auf Werkseinstellungen

- Zentralisierte Sichtbarkeit der Geräteintegrität  

- Verknüpfen von Benutzern, Geräten und Apps mit Azure Active Directory (Azure AD)  

- Moderne Bereitstellung mit Windows Autopilot  

- Remoteaktionen

Weitere Informationen zu dieser unmittelbaren Wertschöpfung aus der Co-Verwaltung finden Sie in der Schnellstartserie zur [Cloudverbindung mit Co-Verwaltung](quickstarts.md).

Co-Verwaltung ermöglicht Ihnen auch die Orchestrierung für mehrere Workloads mit Intune. Weitere Informationen finden Sie im Abschnitt [Workloads](#workloads).

## <a name="prerequisites"></a>Voraussetzungen

Für Co-Verwaltung gelten diese Voraussetzungen in den folgenden Bereichen:

- [Lizenzierung](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Berechtigungen und Rollen](#permissions-and-roles)  

### <a name="licensing"></a>Lizenzierung

- Azure AD Premium

    > [!Note]  
    > Ein Enterprise Mobility + Security-Abonnement (EMS) umfasst Azure Active Directory Premium und Microsoft Intune.

- Mindestens eine Intune-Lizenz für Sie als Administrator für den Zugriff auf das Intune-Portal.

    > [!Tip]
    > Stellen Sie sicher, dass Sie dem Konto, mit dem Sie sich bei Ihrem Mandanten anmelden, eine Intune-Lizenz zuweisen. Andernfalls schlägt die Anmeldung mit der Fehlermeldung „Benutzer nicht erkannt“ fehl.
    >
    > Sie müssen nicht mehr einzelne Intune- oder EMS-Lizenzen kaufen und Ihren Benutzern zuweisen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zum Produkt und zur Lizenzierung](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="configuration-manager"></a>Configuration Manager

Co-Verwaltung erfordert Configuration Manager Version 1710 oder höher.

Ab Version 1806 von Configuration Manager können Sie mehrere Instanzen von Configuration Manager mit einem einzelnen Intune-Mandanten verbinden. <!--1357944-->  

Die Aktivierung von Co-Verwaltung selbst erfordert nicht, dass Sie Azure AD an Ihrem Standort integrieren. Für das [Szenario mit dem zweiten Pfad](#paths-to-co-management) benötigen internetbasierte Configuration Manager-Clients das [Cloudverwaltungsgateway](../core/clients/manage/cmg/plan-cloud-management-gateway.md) (Cloud Management Gateway, CMG). Das Cloudverwaltungsgateway erfordert, dass der Standort [in Azure AD für die Cloudverwaltung integriert](../core/servers/deploy/configure/azure-services-wizard.md) ist.

### <a name="azure-ad"></a>Azure AD

- Windows 10-Geräte müssen mit Azure AD verbunden sein. Sie können einem der folgenden Typen angehören:  

  - [In Hybrid-Azure AD eingebunden](/azure/active-directory/devices/concept-azure-ad-join-hybrid), wenn das Gerät mit Ihrer lokalen Active Directory-Instanz verknüpft und für Azure Active Directory registriert ist.

  - [In Azure AD eingebunden](/azure/active-directory/devices/azureadjoin-plan) (ausschließlich). (Dieser Typ wird manchmal auch als „in die Clouddomäne eingebunden“ bezeichnet.)<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Einrichten von Intune](/intune/setup-steps)  

- [Aktivieren der automatischen Registrierung von Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Upgrade der Geräte auf Windows 10, Version 1709 oder höher. Weitere Informationen finden Sie unter [Verwenden von Windows-as-a-Service)](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Co-Verwaltung wird von Windows 10 Mobile-Geräten nicht unterstützt.

### <a name="permissions-and-roles"></a>Berechtigungen und Rollen

<!--SCCMDocs issue #667-->
| Aktion | Erforderliche Rolle |
|----|----|
| Einrichten eines Cloudverwaltungsgateways in Configuration Manager | Azure **Abonnement-Manager** |
| Erstellen von Azure AD-Apps aus Configuration Manager | **Globaler Administrator** für Azure AD |
| Importieren von Apps in Configuration Manager | **Hauptadministrator** für Configuration Manager<br>Keine weiteren Azure-Rollen erforderlich |
| Aktivieren der Co-Verwaltung in Configuration Manager | Azure AD-Benutzer<br>**Hauptadministrator** für Configuration Manager mit **allen** Bereichsberechtigungen.<!--SCCMDoc issue 626--> |

Weitere Informationen über Azure-Rollen finden Sie unter [Grundlegendes zu verschiedenen Rollen](/azure/role-based-access-control/rbac-and-directory-admin-roles).

Weitere Informationen zu Configuration Manager-Rollen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../core/understand/fundamentals-of-role-based-administration.md).

## <a name="workloads"></a>Workloads

Sie müssen die Workloads nicht wechseln, oder Sie können sie einzeln ausführen, wenn Sie bereit sind. Configuration Manager verwaltet weiterhin alle anderen Workloads (einschließlich der Workloads, die Sie nicht an Intune übergeben) und alle anderen Funktionen von Configuration Manager, die die Co-Verwaltung nicht unterstützt.

Co-Verwaltung unterstützt die folgenden Workloads:

- Kompatibilitätsrichtlinien  

- Windows Update-Richtlinien  

- Ressourcenzugriffsrichtlinien  

- Endpoint Protection  

- Gerätekonfiguration  

- Office-Klick-und-Los-Apps  

- Client-Apps  

Weitere Informationen finden Sie unter [Workloads](workloads.md).

## <a name="monitor-co-management"></a>Überwachen der Co-Verwaltung

Mithilfe des Dashboards für die Co-Verwaltung können Sie die Computer überprüfen, die in Ihrer Umgebung gemeinsam verwaltet werden. Mithilfe der Diagramme können Geräte identifiziert werden, bei denen möglicherweise ein Eingriff erforderlich ist.

![Screenshot des Dashboards für die Co-Verwaltung](media/co-management-dashboard.png)

Weitere Informationen finden Sie unter [Überwachen der Co-Verwaltung](how-to-monitor.md).

## <a name="next-steps"></a>Nächste Schritte

- [Weitere Informationen zur unmittelbaren Wertschöpfung und zu den ersten Schritten mit der Co-Verwaltung](quickstarts.md)  

- [Tutorial: Aktivieren der Co-Verwaltung für vorhandene Configuration Manager-Clients](tutorial-co-manage-clients.md)