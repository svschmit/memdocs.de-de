---
title: Features der Vorabversion
titleSuffix: Configuration Manager
description: Features des Vorabrelease sind Features, die in Current Branch enthalten sind, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703538"
---
# <a name="pre-release-features-in-configuration-manager"></a>Features des Vorabrelease in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Features des Vorabrelease sind Features, die in Current Branch enthalten sind, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Diese Features werden zwar vollständig unterstützt, sie befinden sich aber noch im Stadium der aktiven Entwicklung. Es können so lange Änderungen an ihnen vorgenommen werden, bis sie nicht mehr der Vorabversionskategorie angehören.

## <a name="give-consent"></a>Zustimmungserteilung  

Bevor Sie ein Features des Vorabrelease verwenden, müssen Sie der Verwendung dieser Features zustimmen. Sie müssen nur einer Aktion pro Hierarchie zustimmen. Dies kann nicht rückgängig gemacht werden. Sie können bis zu Ihrer Zustimmung keine neuen Features des Vorabrelease aktivieren, die in Updates enthalten sind. Wenn Sie ein Features des Vorabrelease einmal aktiviert haben, können Sie dieses nicht wieder deaktivieren.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Klicken Sie im Menüband auf **Hierarchieeinstellungen**.  

3. Aktivieren Sie auf der Registerkarte **Allgemein** der Eigenschaften von Hierarchieeinstellungen die Option **Consent to use pre-release features** (Verwendung von Features des Vorabrelease). Klicken Sie auf **OK**.  

## <a name="enable-pre-release-features"></a>Aktivieren der Features des Vorabreleases

Wenn Sie ein Update installieren, das Features des Vorabrelease enthält, werden diese Features im Assistenten für Updates und Wartung zusammen mit den regulären Funktionen angezeigt, die im Update enthalten sind.

### <a name="if-you-have-given-consent"></a>Zustimmungserteilung erfolgt

Aktivieren Sie im Assistenten für Updates und Wartung Features des Vorabrelease Wählen Sie dazu die Features des Vorabrelease so aus, wie Sie jedes andere Feature auswählen würden.

Alternativ können Sie auch warten und die Features des Vorabrelease später über den Knoten **Features** unter **Updates und Wartung** im Arbeitsbereich **Verwaltung** aktivieren. Wählen Sie ein Feature aus, und klicken Sie anschließend im Menüband auf **Aktivieren**. Diese Option kann erst verwendet werden, wenn Sie zugestimmt haben.

### <a name="if-you-havent-given-consent"></a>Zustimmungserteilung nicht erfolgt

Die Features des Vorabrelease werden zwar im Assistenten für Updates und Wartung angezeigt, können aber nicht aktiviert werden. Nachdem das Update installiert wurde, werden diese Features im Knoten **Features** angezeigt. Allerdings können Sie sie erst aktivieren, wenn Sie zugestimmt haben.

> [!IMPORTANT]  
> In einer Hierarchie mit mehreren Standorten können Sie nur optionale Features oder Features der Vorabversion vom Standort der zentralen Verwaltung aus aktivieren. Dieses Verhalten stellt sicher, dass keine Konflikte in der Hierarchie auftreten. <!--507197-->  
>
> Wenn Sie an einem eigenständigen primären Standort Ihre Zustimmung erteilt haben und die Hierarchie durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie am Standort der zentralen Verwaltung erneut Ihre Zustimmung geben.  

Wenn Sie ein Feature der Vorabversion aktivieren, muss der Hierarchie-Manager von Configuration Manager (HMAN) die Änderung verarbeiten, bevor Sie das Feature nutzen können. Die Verarbeitung der Änderungen erfolgt oft sofort. Je nach Verarbeitungszyklus des HMAN kann es bis zu 30 Minuten dauern, bis die Verarbeitung abgeschlossen ist. Starten Sie die Konsole nach Abschluss der Änderungen neu, bevor Sie das Feature verwenden.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a>Liste der Features des Vorabreleases

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Komponente          | Als Vorabversion hinzugefügt | Als vollständiges Feature hinzugefügt |
|------------------|----------------------|-------------------------|
| [Orchestrierungsgruppen](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Version 2002 | ![Noch nicht](media/red_x.png) |
| [Tasksequenz-Bereitstellungstyp](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Version 2002 | ![Noch nicht](media/red_x.png) |
| [Entfernen des Standorts der zentralen Verwaltung](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Version 2002 | ![Noch nicht](media/red_x.png) |
| [Debugger für Tasksequenzen](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Version 1906 | ![Noch nicht](media/red_x.png) |
| [Anwendungsgruppen](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Version 1906 | ![Noch nicht](media/red_x.png) |
| [Azure Active Directory-Benutzergruppenermittlung](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Version 1906 | Version 2002 |
| [Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Version 1906| Version 2002 |
| [Eigenständige Verwendung von CMPivot](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Version 1906 | Version 2002 |
| [Verwaltungsdienst für SMS-Anbieter](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Version 1810 | Version 1906 |
| [Erweitertes HTTP-Standortsystem](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Version 1806 | Version 1810 |
| [Client-Apps für gemeinsam verwaltete Geräte](../../../comanage/workloads.md#client-apps) <br/> (zuvor bekannt als *Mobile Apps für gemeinsam verwaltete Geräte*) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Version 1806 | Version 2002 |
| [Paketkonvertierungs-Manager](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Version 1806 | Version 1810 |
| [Bereitstellung in Phasen](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Version 1802 | Version 1806 |
| [Verwaltung der Windows Defender-Anwendungssteuerung](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Version 1702 | Version 1906 |
| [Warten einer clusterfähigen Sammlung (Servergruppen)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Version 1602 | ![Noch nicht](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> Weitere Informationen zu nicht vorab veröffentlichten Features, die Sie zunächst aktivieren müssen, finden Sie unter [Aktivieren optionaler Features von Updates](install-in-console-updates.md#bkmk_options).  
>
> Weitere Informationen zu Features, die nur im Technical Preview-Branch verfügbar sind, finden Sie unter [Technical Preview](../../get-started/technical-preview.md).  
