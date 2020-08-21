---
title: Was ist mit der hybriden Verwaltung mobiler Geräte passiert?
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die veraltete hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95ac4160895394eb075589ed18a317923f317b45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695391"
---
# <a name="what-happened-to-hybrid-mdm"></a>Was ist mit der hybriden Verwaltung mobiler Geräte passiert?

*Gilt für: Configuration Manager (Current Branch)*

> [!WARNING]
> Seit dem 1. September 2019 hat Microsoft das Angebot für den Hybriden MDM-Dienst eingestellt. Alle verbleibenden Hybriden MDM-Geräte erhalten keine Richtlinien, Apps oder Sicherheitsupdates.

## <a name="remove-hybrid-mdm"></a>Hybrid-MDM entfernen

Wenn Ihr Configuration Manager-Standort über ein Microsoft Intune-Abonnement verfügt, müssen Sie es entfernen.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Cloud Services**, und markieren Sie den Knoten **Microsoft Intune-Abonnement**. Löschen Sie Ihr vorhandenes Intune-Abonnement.

1. Wählen Sie im **Assistenten zum Entfernen von Microsoft InTune Abonnements**die Option zum **entfernen Microsoft InTune Abonnements aus Configuration Manager aus**, und klicken Sie dann auf **weiter**.

1. Schließen Sie den Assistenten ab.

## <a name="deprecation-announcement"></a>Ankündigung der veralteten Veröffentlichung

Die folgende Notiz ist die ursprüngliche Ankündigung der veralteten Version:

> [!NOTE]  
> Ab dem 14. August 2018 gilt das Feature für die hybride Verwaltung mobiler Geräte als [veraltet](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Ab Dienstversion 1902 von Intune, die voraussichtlich Ende Februar 2019 veröffentlicht wird, können Kunden keine neue Hybridverbindung mehr erstellen.
> <!--Intune feature 2683117-->  
> Seit der Einführung in Azure vor über einem Jahr wurden Intune Hunderte neuer Funktionen, die von Kunden gewünscht wurden, und marktführende Dienstfunktionen hinzugefügt. Es bietet ab sofort weitaus mehr Funktionen als die Hybridverwaltung mobiler Geräte (MDM). Intune in Azure bietet eine stärker integrierte, optimierte Verwaltungsoberfläche, die auf Ihre Enterprise Mobility-Anforderungen zugeschnitten ist.
>
> Daher ziehen die meisten Kunden Intune in Azure gegenüber Hybrid-MDM vor. Die Anzahl der Kunden, die Hybrid-MDM nutzen, geht immer weiter zurück, während gleichzeitig immer mehr Kunden Migrationen in die Cloud durchführen. Aus diesem Grund stellt Microsoft am 1. September 2019 das Hybrid-MDM-Dienstangebot ein.
>
> Diese Änderung betrifft keine lokalen Configuration Manager- oder [Windows 10-Geräte für die Co-Verwaltung](../../comanage/overview.md). Wenn Sie nicht sicher sind, ob Sie hybride Verwaltung mobiler Geräte verwenden, wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung** , erweitern Sie **Cloud Services**, und wählen Sie dann **Microsoft InTune Abonnements**aus. Wenn Sie ein Microsoft Intune-Abonnement eingerichtet haben, ist Ihr Mandant für Hybrid-MDM konfiguriert.
>
> **Wie wirkt sich das auf mich aus?**
>
> - Microsoft stellt Ihnen im kommenden Jahr Support für die Nutzung von Hybrid-MDM bereit. Es werden weiterhin wichtige Fehlerbehebungen für das Feature veröffentlicht. Microsoft unterstützt vorhandene Funktionen unter neuen Betriebssystemversionen wie etwa die Registrierung unter iOS 12. Es werden jedoch keine neuen Features für Hybrid-MDM veröffentlicht.  
>
> - Wenn Sie vor Ablauf des Hybrid-MDM-Angebots nach Intune in Azure migrieren, sollte es keine Beeinträchtigung für Endbenutzer geben.  
>
> - Ab dem 1. September 2019 werden keine Richtlinien-, App- oder Sicherheitsupdates mehr für verbleibende Hybrid-MDM-Geräte bereitgestellt.  
>
> - Die Lizenzierung bleibt unverändert. Intune in Azure-Lizenzen sind im Lieferumfang von Hybrid-MDM enthalten.  
>
> - Das lokale MDM-Feature in Configuration Manager ist nicht als veraltet markiert. Ab Configuration Manager Version 1810 können Sie die lokale Verwaltung mobiler Geräte (MDM) ohne InTune-Verbindung verwenden. Weitere Informationen finden Sie unter [eine InTune-Verbindung ist für neue lokale MDM-bereit Stellungen nicht mehr erforderlich](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - Das Feature für den lokalen bedingten Zugriff von Configuration Manager ist auch mit der Hybriden Verwaltung mobiler Geräte (MDM) veraltet. Wenn Sie den bedingten Zugriff auf Geräten verwenden, die mit dem Configuration Manager-Client verwaltet werden, stellen Sie sicher, dass Sie vor der Migration geschützt sind.
>     1. Einrichten von Richtlinien für den bedingten Zugriff in Azure
>     2. Einrichten von Konformitäts Richtlinien im InTune-Portal
>     3. Abschließen der Hybrid Migration und Festlegen der MDM-Autorität auf InTune
>     4. Aktivieren der Co-Verwaltung
>     5. Verschieben der Arbeitsauslastung der Konformitäts Richtlinien für die Co-Verwaltung in InTune
>
>     Weitere Informationen finden Sie unter [Bedingter Zugriff mit Co-Verwaltung](../../comanage/quickstart-conditional-access.md).
>
> **Was muss ich als Vorbereitung auf diese Änderung tun?**
>
> - Beginnen Sie mit der Planung Ihrer Migration für MDM von der ConfigMgr-Konsole nach Azure. Viele Kunden, einschließlich der Microsoft-IT, haben diesen Prozess bereits durchlaufen. Weitere Informationen finden Sie in [dieser Microsoft-Fallstudie](https://aka.ms/Intune_MSFT).  
>
> - Wenden Sie sich an den für Sie zuständigen Partner oder an FastTrack, um weitere Unterstützung zu erhalten. [FastTrack für Microsoft 365](https://aka.ms/hybrid_fasttrack) kann Sie bei der Migration von Hybrid-MDM nach Intune in Azure unterstützen.
>
> Weitere Informationen finden Sie [im Blogbeitrag zum InTune-Support](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den unterstützten Funktionen für die Verwaltung von MDM-Geräten finden Sie in den folgenden Artikeln:

- [Was ist Microsoft InTune?](/intune/what-is-intune)
- [Was ist eine lokale MDM?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Geräteverwaltung mit Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)