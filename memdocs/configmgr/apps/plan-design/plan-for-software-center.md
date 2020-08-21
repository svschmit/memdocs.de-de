---
title: Planen für Software Center
titleSuffix: Configuration Manager
description: Legen Sie fest, wie Sie Software Center konfigurieren und mit den Markeninformationen Ihrer Organisation versehen möchten, damit Benutzer mit Configuration Manager interagieren können.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b32fc2de3c945ff2292f119a10d84d982d08677
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127357"
---
# <a name="plan-for-software-center"></a>Planen für Software Center

*Gilt für: Configuration Manager (Current Branch)*

Benutzer können im Softwarecenter Einstellungen ändern, nach Anwendungen suchen und diese installieren. Wenn Sie den Konfigurations-Manager-Client auf einem Windows-Gerät installieren, wird auch das Softwarecenter automatisch installiert.

Weitere Informationen zu allen Funktionen finden Sie im [Benutzerleitfaden für das Softwarecenter](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Konfigurieren des Softwarecenters  

Aktualisieren Sie Ihren Configuration Manager-Standort und die Clients auf Version 1906 oder höher, um von den neuesten Verbesserungen im Softwarecenter zu profitieren.

> [!IMPORTANT]
> Diese schrittweise erfolgenden Verbesserungen am Softwarecenter und am Verwaltungspunkt zielen darauf ab, die Anwendungskatalogrollen auslaufen zu lassen.
>
> - Die Silverlight-Benutzeroberfläche wird ab Current Branch-Version 1806 nicht unterstützt.
> - Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren.
> - Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.

- Die Clienteinstellung **Neues Softwarecenter verwenden** in der Gruppe **Computer-Agent** ist standardmäßig aktiviert. Die vorherige Version des Softwarecenters wird nicht mehr unterstützt. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

- Die Sichtbarkeit des Anwendungskatalog-Websitelinks auf der Softwarecenter-Registerkarte **Installationsstatus** kann angegeben werden. Weitere Informationen finden Sie in den Clienteinstellungen des [Softwarecenters](../../core/clients/deploy/about-client-settings.md#software-center).

- Ab Version 1906 können Sie dem Softwarecenter bis zu fünf benutzerdefinierte Registerkarten hinzufügen. Weitere Informationen finden Sie unter [Softwarecenter-Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

- Benutzer können die Affinität zwischen Benutzer und Gerät im Softwarecenter konfigurieren. Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!IMPORTANT]
> Wenn Sie neue Configuration Manager-Features nutzen möchten, müssen Sie zunächst die Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

### <a name="software-center-and-user-available-applications"></a>Softwarecenter und für Benutzer verfügbare Anwendungen

- Es werden keine Anwendungskatalogrollen benötigt, um für Benutzer verfügbare Anwendungen im Softwarecenter anzuzeigen. Dieses Verhalten hilft Ihnen, die erforderliche Serverinfrastruktur zu reduzieren, um Anwendungen schneller für Benutzer bereitzustellen. Das Softwarecenter verlässt sich auf den Verwaltungspunkt, um diese Informationen abzurufen. Dadurch können größere Umgebungen besser skaliert werden, indem sie [Begrenzungsgruppen](../../core/servers/deploy/configure/boundary-groups.md#management-points) zugewiesen werden.<!--1358309-->

- Benutzer können auf Geräten, die in Azure Active Directory eingebunden sind, nach verfügbaren Anwendungen suchen und diese darauf installieren. Ab Version 2006 können sie für Benutzer verfügbare Apps auf internetbasierten, in die Domäne eingebundenen Geräten erhalten. Weitere Informationen finden Sie unter [Bereitstellen von für Benutzer verfügbaren Anwendungen](../deploy-use/deploy-applications.md#deploy-user-available-applications).

- Ab Version 1906 kommuniziert das Softwarecenter mit einem Verwaltungspunkt für Apps, die Benutzern als verfügbar angezeigt werden sollen. Der Anwendungskatalog wird nicht mehr verwendet. Dadurch können Sie den Anwendungskatalog leichter aus dem Standort entfernen.

- Zuvor wurde der erste Verwaltungspunkt aus der Liste mit den verfügbaren Servern verwendet. Ab Version 1906 wird der gleiche Verwaltungspunkt genutzt, den auch der Client verwendet. Dadurch kann das Softwarecenter den gleichen Verwaltungspunkt des zugewiesenen primären Standorts verwenden wie der Client.

## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a> Ersetzen von Popupbenachrichtigungen durch ein Dialogfeld

<!--3555947-->
In einigen Fällen werden Benutzern Windows-Popupbenachrichtigungen über einen Neustart oder eine erforderliche Bereitstellung nicht angezeigt. So haben sie nicht die Möglichkeit, eine erneute Erinnerung anzufordern. Dieses Verhalten kann zu Problemen für den Benutzer führen, wenn der Client einen Stichtag erreicht.

Wenn [Softwareänderungen erforderlich sind](#software-changes-are-required) oder Bereitstellungen [einen Neustart erfordern](#restart-required), haben Sie ab Version 1902 die Möglichkeit, ein nachdrücklicheres Dialogfeld zu verwenden.

### <a name="software-changes-are-required"></a>Softwareupdates erforderlich

Wenn Sie [eine Anwendung](../deploy-use/deploy-applications.md) wie erforderlich mit einem Stichtag in der Zukunft bereitstellen, wählen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Benutzerfreundlichkeit** die folgenden Optionen für Benutzerbenachrichtigungen aus:

- **In Softwarecenter anzeigen und alle Benachrichtigungen anzeigen**
- **Wenn Softwareänderungen erforderlich sind, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen**

Durch die Konfiguration dieser Bereitstellungseinstellung ändert sich die Benutzeroberfläche für dieses Szenario.

Zuerst wurde diese Popupbenachrichtigung angezeigt:

![Popupbenachrichtigung, dass Softwareänderungen erforderlich sind](media/3555947-required-toast.png)  

Jetzt wird das folgende Dialogfenster angezeigt:

![Dialogfenster für die erforderlichen Softwareänderungen](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Neustart erforderlich

Aktivieren Sie in der Gruppe der Clienteinstellungen [Computerneustart](../../core/clients/deploy/about-client-settings.md#computer-restart) die folgende Option: **Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen**  

Durch die Konfiguration dieser Clienteinstellung ändert sich die Benutzeroberfläche für alle erforderlichen Bereitstellungen folgender Arten, die einen Neustart erfordern:

- [Anwendung](../deploy-use/deploy-applications.md)
- [Tasksequenz](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Softwareupdate](../../sum/deploy-use/deploy-software-updates.md)

Zuerst wurde diese Popupbenachrichtigung angezeigt:

![Popupbenachrichtigung, dass ein Neustart erforderlich ist](media/3555947-restart-toast.png)  

Jetzt wird das folgende Dialogfenster angezeigt:

![Dialogfenster für den Neustart des Computers](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> In Configuration Manager 1902 ersetzt das Dialogfeld unter bestimmten Umständen keine Popupbenachrichtigungen. Installieren Sie zur Behebung dieses Problems das [Updaterollup für Configuration Manager Version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="brand-software-center"></a>Marken-Softwarecenter

Ändern Sie das Erscheinungsbild des Softwarecenters, um die Brandinganforderungen Ihres Unternehmens zu erfüllen. Mit dieser Konfiguration lässt sich das Vertrauen der Benutzer in das Softwarecenter verbessern.

### <a name="configure-software-center-branding"></a>Konfigurieren des Brandings für das Softwarecenter

<!-- 1351224 -->
Passen Sie das Erscheinungsbild des Softwarecenters an, indem Sie die Brandingelemente Ihrer Organisation hinzufügen und die Sichtbarkeit von Registerkarten bestimmen.

Weitere Informationen finden Sie in den folgenden Artikeln:

- Clienteinstellungen für das [Softwarecenter](../../core/clients/deploy/about-client-settings.md#software-center)  
- [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Brandingprioritäten

Configuration Manager verwendet ein benutzerdefiniertes Branding für Softwarecenter gemäß den folgenden Prioritäten:  

1. Clienteinstellungen für das **Softwarecenter**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#software-center).  

2. Clienteinstellung **Organisationsname** in der Gruppe **Computer-Agent**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#computer-agent).  

#### <a name="application-catalog-branding-priorities"></a>Brandingprioritäten im Anwendungskatalog

> [!IMPORTANT]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  

Wenn Sie den Anwendungskatalog verwenden, gilt für das Branding Folgendes:  

1. Clienteinstellungen für das **Softwarecenter**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#software-center).  

2. Der *Organisationsname* und die *Farbe*, die Sie in den Eigenschaften des Anwendungskatalog-Websitepunkts angeben. Weitere Informationen finden Sie unter [Konfigurationsoptionen für den Anwendungskatalog-Websitepunkt](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).  

3. Clienteinstellung **Organisationsname** in der Gruppe **Computer-Agent**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#computer-agent).  

## <a name="see-also"></a>Weitere Informationen

- [Benutzerleitfaden des Softwarecenters](../../core/understand/software-center.md)
- [Planen und Konfigurieren der Anwendungsverwaltung](plan-for-and-configure-application-management.md)
