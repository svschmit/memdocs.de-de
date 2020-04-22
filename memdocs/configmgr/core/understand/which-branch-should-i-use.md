---
title: Welcher Branch sollte verwendet werden?
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Unterschiede zwischen den verfügbaren Branches von Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a505296fe51aae996d429fe7da2033d3a787ff
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706668"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Welcher Branch von Configuration Manager soll verwendet werden?

*Gilt für: Configuration Manager (Current Branch und Technical Preview Branch) und System Center Configuration Manager (Long-Term Servicing Branch)*

Es gibt drei in Configuration Manager verfügbare Branches:

- Current Branch
- Long Term Servicing Branch
- Technical Preview-Branch

Mithilfe dieses Artikels können Sie den geeigneten Branch auswählen.

> [!TIP]  
> Alle Standorte in einer Hierarchie müssen den gleichen Branch ausführen. Eine Hierarchie mit verschiedenen Branches an unterschiedlichen Standorten wird nicht unterstützt.

## <a name="current-branch"></a>Current Branch

Dieser Branch ist für die Verwendung in einer Produktionsumgebung lizenziert. Verwenden Sie diesen Branch, um die neuesten Features und Funktionen abzurufen. Wenn Sie eine der folgenden Lizenzen besitzen, können Sie diesen Branch verwenden:  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Entsprechende Abonnementrechte  

Weitere Informationen zu Software Assurance und Lizenzierungsoptionen finden Sie unter [Lizenzierung und Branches für Configuration Manager](learn-more-editions.md) und [Häufig gestellte Fragen zu Branches und Lizenzierung von Configuration Manager](product-and-licensing-faq.md).

Microsoft plant mehrere jährliche Updatereleases für die Current Branch-Versionen von Configuration Manager. Jede Updateversion wird dabei 18 Monate lang ab dem Datum der allgemeinen Verfügbarkeit unterstützt. Technischer Support wird für den gesamten Supportzeitraum geboten. Unsere Supportstruktur ist jedoch dynamisch und folgt zwei unterschiedlichen Wartungsphasen, die von der Verfügbarkeit der neuesten Current Branch-Version abhängig sind. Weitere Informationen finden Sie unter [Unterstützung für die Current Branch-Versionen von Configuration Manager](../servers/manage/current-branch-versions-supported.md). Die Updates auf neuere Versionen sind als konsoleninterne Updates verfügbar.

Verwenden Sie [Baselinemedien](../servers/manage/updates.md#bkmk_Baselines), um Current Branch als neuen Standort zu installieren. Verwenden Sie ebenfalls Baselinemedien, um für System Center 2012 Configuration Manager mit Service Pack 2 oder System Center 2012 R2 Configuration Manager mit Service Pack 1 ein Upgrade auszuführen. Der Zugriff auf diese Medien hängt davon ab, welche Lizenzierung von Configuration Manager Ihre Organisation besitzt.

Mithilfe der Baselinemedien können Sie auch einen neuen Standort als Evaluierungsversion von Current Branch installieren. Für die Evaluierungsversion ist keine Lizenz erforderlich. Sie können die Evaluierungsversion 180 Tage lang verwenden. Diese Version unterstützt ein Upgrade auf eine lizenzierte Version von Current Branch. Wenn Sie nur eine Evaluierungsversion installieren möchten, erhalten Sie diese unter [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Verwenden Sie Baselinemedien zum Installieren von Standorten für eine neue Configuration Manager-Hierarchie. Wenn Sie bereits eine Baselineversion installiert haben, aktualisieren Sie Ihre Standorte mithilfe von konsoleninternen Updates auf eine neue Version.  
>
> Standorte, die mit konsoleninternen Updates aktualisiert werden, sind nach dem Update mit dem neuen Standort identisch, der mithilfe der Baselinemedien installiert wurde.
>
> Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Features von Current Branch

- Empfängt [konsoleninterne Updates](../servers/manage/install-in-console-updates.md), mit denen neue Features zur Verwendung verfügbar gemacht werden.
- Empfängt konsoleninterne Updates, mit denen Sicherheits- und Qualitätsfixes für vorhandene Features bereitgestellt werden.
- Unterstützt bei Bedarf Out-of-Band-Updates. Weitere Informationen finden Sie unter [Use the update registration tool (Verwenden des Tools zur Updateregistrierung)](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) oder unter [Use the hotfix installer (Verwenden des Hotfix-Installers)](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Integration in cloudbasierte Dienste
- Unterstützt die [Migration von Daten](../migration/migrate-data-between-hierarchies.md) zu und von anderen Configuration Manager-Installationen.
- Unterstützt ein Upgrade von früheren Versionen von Configuration Manager.
- Unterstützt die Installation als Evaluierungsversion, für die später ein Upgrade auf eine vollständig lizenzierte Version durchgeführt werden kann.

Microsoft empfiehlt möglichst schnell nach der Veröffentlichung ein Update auf die jeweils neueste Version durchzuführen. Sie können bis zu 18 Monate warten, bis Sie ein Update auf eine neuere Version durchführen. Sie können ein Update auch überspringen, um die neueste verfügbare Version zu installieren. Wenn Sie ein Update überspringen und die neueste Version installieren, haben Sie dennoch Zugriff auf alle Features und Verbesserungen aus früheren Versionen, da alle Versionen kumulativ sind.

Weitere Informationen finden Sie unter [Support for Current Branch versions (Unterstützung für Current Branch-Versionen)](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Current Branch Aktualisierungsoptionen

- Mit einer aktiven Software Assurance-Lizenz können Sie konsoleninterne Updates für Current Branch-Versionen installieren.  
- Es gibt keine Option zum Konvertieren von Current Branch zu einem Technical Preview-Branch. Technical Preview-Branches sind separate Installationen, für die keine Lizenz erforderlich ist.
- Es gibt keine Option zum Konvertieren von Current Branch zu Long-Term Servicing Branch (LTSB). Sie müssen zuerst Current Branch deinstallieren und anschließend LTSB neu installieren.

## <a name="long-term-servicing-branch"></a>Long Term Servicing Branch

Dieser Branch ist für die Verwendung in Produktionsumgebungen für Configuration Manager-Kunden lizenziert, die Current Branch verwenden, und bei denen die Software Assurance (SA) von Configuration Manager oder entsprechende Abonnementrechte nach dem 1. Oktober 2016 abgelaufen sind. Weitere Informationen zu Software Assurance und Lizenzierungsoptionen finden Sie unter [Lizenzierung und Branches für Configuration Manager](learn-more-editions.md) und [Häufig gestellte Fragen zu Branches und Lizenzierung von Configuration Manager](product-and-licensing-faq.md).

LTSB basiert auf Version 1606. Mit diesem Branch erhalten Sie keine konsoleninternen Updates, mit denen neue Features oder Updates für vorhandene Funktionen bereitgestellt werden. Wichtige Sicherheitsfixes werden jedoch bereitgestellt. Für die Installation von LTSB müssen Sie die [Baselinemedien](../servers/manage/updates.md#bkmk_Baselines) der Version 1606 verwenden, die Sie mit System Center 2016 erhalten. Höhere Baselineversionen unterstützen die Installation von LTSB nicht.

Verwenden Sie die [Baselinemedien](../servers/manage/updates.md#bkmk_Baselines) von Version 1606, die in System Center 2016 enthalten sind, um LTSB als neuen Standort oder als Upgrade eines unterstützten System Center Configuration Manager 2012-Standorts zu installieren. Mit den Baselinemedien können Sie einen neuen Standort installieren, an dem Long-Term Servicing Branch oder Version 1606 von Current Branch ausgeführt wird.

> [!TIP]  
> Weitere Informationen zu System Center 2016 finden Sie in der [Dokumentation zu System Center 2016](https://docs.microsoft.com/system-center/index). In dieser Dokumentation wird auch beschrieben, wie Sie System Center 2016 erhalten, eine Lösung, für die Sie einen Microsoft-Lizenzvertrag oder entsprechende Rechte benötigen.  
>  
> Wenn Sie Configuration Manager Version 1606 in Volume Licensing Service Center (VLSC) suchen möchten, wechseln Sie zur Registerkarte **Downloads and Keys** (Downloads und Schlüssel) von [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), suchen Sie nach `System Center 2016`, und wählen Sie **System Center 2016 Datacenter** oder **System Center 2016 Standard** aus.  
>  
> Sie können auch eine Evaluierungsversion von System Center 2016 erhalten, die Sie im [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview) herunterladen können.  

### <a name="features-of-the-ltsb"></a>Features von LTSB

- Empfängt konsoleninterne Updates, mit denen wichtige Sicherheitsfixes bereitgestellt werden.
- Stellt eine Installationsoption bereit, wenn der Software Assurance-Vertrag oder entsprechende Rechte für Configuration Manager abgelaufen sind.
- Unterstützt ein Upgrade (Konvertierung) auf Current Branch, wenn Sie über einen aktuellen Software Assurance-Vertrag oder entsprechende Rechte für Configuration Manager verfügen.

### <a name="ltsb-limitations"></a>LTSB-Einschränkungen

LTSB basiert auf der Current Branch-Version 1606 und weist die folgenden Einschränkungen auf:

- LTSB wird nach der allgemeinen Verfügbarkeit (Oktober 2016) 10 Jahre lang mit wichtigen Sicherheitsupdates unterstützt. Danach läuft die Unterstützung für diesen Branch ab. Weitere Informationen zum Supportlebenszyklus finden Sie unter [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/lifecycle).
- Unterstützt eine eingeschränkte feste Liste mit Server- und Clientbetriebssystemen und entsprechenden Technologien wie SQL Server-Versionen. Weitere Informationen finden Sie unter [Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager](supported-configurations-for-ltsb.md).
- Erhält keine Updates für neue Features
- Folgende Funktionen werden nicht unterstützt:
  - cloudgestützte Funktionen wie die Co-Verwaltung oder Desktop Analytics
  - Lokale Verwaltung mobiler Geräte
  - Das Windows 10-Wartungsdashboard, Wartungspläne oder den halbjährlichen Windows 10-Kanal
  - Zukünftige Releases von LTSB für Windows 10 und Windows Server
  - Asset Intelligence
  - Sämtliche Features des Vorabreleases

### <a name="ltsb-update-options"></a>LTSB-Updateoptionen

- Sie können die LTSB-Installation in eine Current Branch-Installation konvertieren. Die Konvertierung zu Current Branch wird vor oder nach Ablauf der Unterstützung für LTSB unterstützt.

  Für die Konvertierung ist ein aktiver Software Assurance-Vertrag mit Microsoft erforderlich. Weitere Informationen finden Sie in den folgenden Artikeln:

  - [Upgrade von Long-Term Servicing Branch auf Current Branch](convert-to-current-branch.md)
  - [Lizenzierung und Branches für System Center Configuration Manager](learn-more-editions.md)
  - [Baseline- und Updateversionen](../servers/manage/updates.md#bkmk_Baselines)

- Es gibt keine Option zum Konvertieren von LTSB zu einem Technical Preview-Branch. Technical Preview-Branches sind separate Installationen, für die keine Lizenz erforderlich ist.

- Für eine Evaluierungsversion von Current Branch kann kein Upgrade auf eine LTSB-Installation durchgeführt werden.

## <a name="technical-preview-branch"></a>Technical Preview-Branch

Der Technical Preview-Branch ist für die Verwendung in einer Laborumgebung gedacht. Erfahren Sie mehr über die neuesten Features, die für Configuration Manager bereitgestellt wurden, und probieren Sie diese aus. In einer Produktionsumgebung wird dies nicht unterstützt.Ein Software Assurance-Lizenzvertrag ist nicht erforderlich.

Wenn Sie einen neuen Standort installieren möchten, an dem der Technical Preview-Branch ausgeführt wird, verwenden Sie die neuesten [Baselinemedien für den Technical Preview-Branch](../get-started/technical-preview.md#bkmk_install). Nach der Installation des Technical Preview-Branches sind jeden Monat neue Versionen als konsoleninterne Updates verfügbar.

### <a name="features-of-the-technical-preview-branch"></a>Features des Technical Preview-Branches

- Basiert auf aktuellen Baselineversionen von Current Branch
- Empfängt konsoleninterne Updates, mit denen die Installation auf die neueste Version des Technical Preview-Branches aktualisiert wird
- Enthält neu entwickelte Features, für die Microsoft Ihr Feedback wünscht
- Empfängt Updates, die nur für den Technical Preview-Branch gelten

### <a name="technical-preview-limitations"></a>Technical Preview-Einschränkungen

- [Eingeschränkte Unterstützung](../get-started/technical-preview.md#bkmk_reqs), die nur einen primären Standort mit bis zu 10 Clients umfasst.  
- Sie können für diesen kein Upgrade durchführen oder zu einem Current Branch oder einer LTSB-Installation migrieren.
- Folgende Verhaltensweisen werden nicht unterstützt:
  - Migration zum Importieren oder Exportieren von Daten in oder von einer anderen Configuration Manager-Installation
  - Upgrade von einer früheren Version von Configuration Manager
  - Installieren als eine Evaluierungsversion

Features, die mit einem Technical Preview-Branch eingeführt werden, werden später häufig in Current Branch ebenfalls bereitgestellt. Jede neue Version von Technical Preview-Branch beinhaltet die Features aus früheren Technical Preview-Branches, auch wenn diese Features dann bereits in Current Branch enthalten sind.

Weitere Informationen erhalten Sie unter [Technical Preview für Configuration Manager](../get-started/technical-preview.md).

### <a name="technical-preview-update-options"></a>Technical Preview-Updateoptionen

- Für eine neue Version des Technical Preview-Branches kann jedes konsoleninterne Update installiert werden.

- Es gibt keine Option zum Konvertieren eines Technical Preview-Branches zu Current Branch oder LTSB.

## <a name="identify-your-version-and-branch"></a>Ermitteln der Version und des Branches

### <a name="version"></a>Version

Wechseln Sie oben links in der Konsole zu **Info**, um die Version Ihres Standorts zu überprüfen. Dieses Dialogfeld zeigt die **Standortversion** an. Eine Liste der Standortversionen finden Sie unter [Baseline- und Updateversionen](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Zweig

Navigieren Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und öffnen Sie **Hierarchieeinstellungen**, um den Branch Ihres Standorts zu ermitteln. Wenn die aktive Option besteht, zu Current Branch zu konvertieren, führt der Standort die LTSB-Version aus. Wenn der Standort Current Branch ausführt, wird diese Option in der Konsole deaktiviert.

Informationen zu den verschiedenen Versionen von Configuration Manager finden Sie unter [Baseline- und Updateversionen](../servers/manage/updates.md#bkmk_Baselines).
