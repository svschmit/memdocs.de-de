---
title: Bewährte Methoden für Softwareupdates
titleSuffix: Configuration Manager
description: Verwenden Sie diese bewährten Methoden für Softwareupdates in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: eb9a675970abb581a793208c73506e1e94cc6f63
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906689"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Bewährte Methoden für Softwareupdates in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält bewährte Methoden für Softwareupdates in Configuration Manager. Diese sind nach den bewährten Methoden für die Erstinstallation und den laufenden Betrieb sortiert.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> Bewährte Methoden für die Installation  

Verwenden Sie die folgenden bewährten Methoden für die Installation von Softwareupdates in Configuration Manager.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> Verwenden einer freigegebenen WSUS-Datenbank für Softwareupdatepunkte  

Wenn Sie an einem primären Standort mehrere Softwareupdatepunkte installieren, sollten Sie für jeden Softwareupdatepunkt einer Active Directory-Gesamtstruktur die gleiche WSUS-Datenbank verwenden. Durch die Nutzung der gleichen Datenbank können Sie die Auswirkungen auf die Client- und Netzwerkleistung, die sich beim Wechsel eines Clients zu einem neuen Softwareupdatepunkt ergeben können, erheblich abmildern, aber nicht vollständig vermeiden. Wenn ein Client zu einem neuen Softwareupdatepunkt wechselt, der eine Datenbank gemeinsam mit dem alten Softwareupdatepunkt nutzt, wird weiterhin eine Deltaüberprüfung ausgeführt. Diese Überprüfung ist jedoch weit weniger umfangreich als bei einem WSUS-Server mit eigener Datenbank. Weitere Informationen zum Wechseln von Softwareupdatepunkten finden Sie unter [Wechseln des Softwareupdatepunkts](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Geben Sie bei Verwendung einer freigegebenen WSUS-Datenbank für Softwareupdatepunkte auch die lokalen WSUS-Inhaltsordner frei.  

Weitere Informationen zur Freigabe der WSUS-Datenbank finden Sie, in englischer Sprache, in den folgenden Blogbeiträgen:  

- [How to implement a shared SUSDB for Configuration Manager software update points](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103) (Implementieren einer freigegebenen SUSDB für Configuration Manager-Softwareupdatepunkte)  

- [Considerations for multiple WSUS instances sharing a content database when using System Center Configuration Manager](https://docs.microsoft.com/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb) (Überlegungen zu mehreren WSUS-Instanzen, die bei der Verwendung von Configuration Manager eine Inhaltsdatenbank gemeinsam nutzen)


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> Konfigurieren eines der Systeme für die Verwendung einer benannten Instanz und das andere für die Verwendung der Standardinstanz, wenn SQL Server sowohl von Configuration Manager als auch von WSUS verwendet wird  

Wenn die Configuration Manager- und WSUS-Datenbanken dieselbe Instanz von SQL Server verwenden, lässt sich die Ressourcennutzung zwischen den beiden Anwendungen nur schwer bestimmen. Verwenden Sie verschiedene SQL Server-Instanzen für Configuration Manager und WSUS. Durch diese Konfiguration können Sie Ressourcennutzungsprobleme, die mit der jeweiligen Anwendung möglicherweise auftreten, einfacher diagnostizieren und behandeln.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> Angeben der Einstellung „Updates lokal speichern“  

Wählen Sie beim Installieren von WSUS die Einstellung **Updates lokal speichern** aus. Durch diese Einstellung lädt WSUS die Lizenzbedingungen herunter, die Softwareupdates zugeordnet sind. Die Bedingungen werden während des Synchronisierungsprozesses heruntergeladen und auf der lokalen Festplatte für den WSUS-Server gespeichert. Wenn Sie diese Einstellung nicht auswählen, tritt bei Konformitätsüberprüfungen für Softwareupdates mit Lizenzbedingungen auf Clientcomputern möglicherweise ein Fehler auf. Die Komponente **WSUS-Synchronisierungs-Manager** des Softwareupdatepunkts überprüft standardmäßig alle 60 Minuten, ob diese Einstellung aktiviert ist.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> Bewährte Betriebsmethoden  

Wenden Sie die folgenden bewährten Methoden an, wenn Sie Softwareupdates verwenden:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> Begrenzen von Softwareupdates auf 1.000 pro Softwareupdatebereitstellung  

Begrenzen Sie die Anzahl von Softwareupdates in einer einzelnen Softwareupdatebereitstellung auf 1.000. Wenn Sie eine Regel für die automatische Bereitstellung erstellen, achten Sie darauf, dass die von Ihnen angegebenen Kriterien nicht zu mehr als 1.000 Softwareupdates führen. Wenn Sie Softwareupdates manuell bereitstellen, wählen Sie höchstens 1.000 Updates aus.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> Erstellen einer neuen Softwareupdategruppe bei jedem Ausführen einer ADR („Patchvorgang am Dienstag ausführen“) und für allgemeine Bereitstellungen  

Es gibt ein Limit von 1.000 Softwareupdates in einer Bereitstellung. Wenn Sie eine Regel für die automatische Bereitstellung (Automatic Deployment Rule, ADR) erstellen, geben Sie an, ob bei jedem Ausführen der Regel eine vorhandene Softwareupdategruppe verwendet oder eine neue Softwareupdategruppe erstellt werden soll. Wenn Sie bestimmte Kriterien in einer ADR angeben, die zu mehreren Softwareupdates führen, und die Regel nach einem wiederkehrenden Zeitplan ausgeführt wird, sollten Sie festlegen, dass bei jeder Ausführung der Regel eine neue Softwareupdategruppe erstellt wird. Dieses Verhalten verhindert, dass für die Bereitstellung der Grenzwert von 1.000 Softwareupdates pro Bereitstellung überschritten wird.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> Verwenden einer vorhandenen Softwareupdategruppe bei ADRs für Endpoint Protection-Definitionsupdates  

Verwenden Sie stets eine vorhandene Softwareupdategruppe, wenn Sie eine ADR verwenden, um Definitionsupdates für Endpoint Protection häufig bereitzustellen. Andernfalls erstellt die ADR im Laufe der Zeit möglicherweise Hunderte von Softwareupdategruppen. Normalerweise legen die Herausgeber von Definitionsupdates fest, dass diese ablaufen, wenn sie von vier neueren Updates abgelöst wurden. Daher enthält die Softwareupdategruppe, die von der ADR erstellt wird, niemals mehr als vier Definitionsupdates dieses Herausgebers: ein aktives und drei abgelöste.  



## <a name="see-also"></a>Weitere Informationen  
 [Planen von Softwareupdates](plan-for-software-updates.md)
