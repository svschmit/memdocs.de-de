---
title: Änderungen im Vergleich zu Version 2012
titleSuffix: Configuration Manager
description: Identifizieren Sie die Änderungen und neuen Funktionen in Configuration Manager im Vergleich zu System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704438"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>Änderungen im Vergleich mit System Center 2012 Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In Configuration Manager Current Branch werden wichtige Änderungen von System Center 2012 Configuration Manager eingeführt. In diesem Artikel werden die wichtigsten Änderungen und neue Funktionen in der ursprünglichen Baselineversion 1511 von Configuration Manager (Current Branch) beschrieben. Informationen zu Änderungen, die in den letzten Updates für Configuration Manager eingeführt wurden, finden Sie unter [Neuigkeiten zu inkrementellen Versionen von Configuration Manager](whats-new-incremental-versions.md).

> [!NOTE]
> Ab Version 1910 ist Configuration Manager Bestandteil von Microsoft Endpoint Manager. Weitere Informationen finden Sie unter [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

Das Release vom Dezember 2015 (Version 1511) von Configuration Manager war die erste Veröffentlichung von Configuration Manager von Microsoft. Er wird in der Regel als Configuration Manager (Current Branch) bezeichnet. *Current Branch* bedeutet, dass diese Version inkrementelle Updates des Produkts unterstützt. Sie bietet auch die Möglichkeit, zwischen diesem Release und früheren Releases von Configuration Manager zu unterscheiden.  

Configuration Manager (Current Branch):  

- Im Produktnamen wird, anders als bei früheren Versionen wie Configuration Manager 2007 oder System Center 2012 Configuration Manager, kein Jahr und keine Produkt-ID verwendet.  

- Inkrementelle produktinterne Updates, sogenannte Updateversionen werden unterstützt. Das erste Release war Version 1511. Spätere Versionen wie Version 1910 werden mehrmals im Jahr als konsoleninterne Updates veröffentlicht.  

- Wird mithilfe einer Baselineversion installiert. Während 1511 die ursprüngliche Baselineversion war, werden neue Baselineversionen wie z. B. 2002 ebenfalls von Zeit zu Zeit veröffentlicht. Baselineversionen können zur Installation eines neuen Configuration Manager-Standorts und einer neuen Hierarchie oder zum Upgrade von einer unterstützten Version von System Center 2012 Configuration Manager verwendet werden.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a> Konsoleninterne Updates

Configuration Manager verwendet eine konsoleninterne Wartungsmethode namens **Updates und Wartung**, mit der Sie empfohlene Updates leicht finden und installieren können.  

Einige Versionen stehen nur als Updates für vorhandene Standorte innerhalb der Configuration Manager-Konsole zur Verfügung. Sie können diese Updates nicht für die Installation eines neuen Configuration Manager-Standorts verwenden. So steht beispielsweise das Update 1910 nur über die Configuration Manager-Konsole zur Verfügung. Es wird verwendet, um einen Standort zu aktualisieren, der bereits eine unterstützte Version von Configuration Manager ausführt.

Eine Updateversion wird in regelmäßigen Abständen auch als neue *Baselineversion* veröffentlicht. Beispielsweise ist die Updateversion 2002 auch eine Baseline. Verwenden Sie eine Baselineversion, um einen neuen Standort oder eine neue Hierarchie zu installieren. Beginnen Sie nicht mit einer älteren Baselineversion wie z. B. 1802, mit der Sie dann viele Upgrades bis hin zur aktuellsten Version durchführen müssen. Verwenden Sie immer die neueste Baseline.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Updates für Configuration Manager](../../servers/manage/updates.md)
- [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a> Dienstverbindungspunkt  

Configuration Manager (Current Branch) enthält eine neue Standortsystemrolle, den **Dienstverbindungspunkt**:  

- Ein Kontaktpunkt für viele cloudfähige Features

- Lädt Updates für Ihren Standort herunter

- Lädt Diagnose- und Nutzungsdaten zu Ihrem Standort in die Microsoft-Cloud hoch

Diese Standortsystemrolle unterstützt sowohl Online- als auch Offline-Betriebsmodi. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a> Diagnose- und Nutzungsdaten

Configuration Manager sammelt Diagnose- und Nutzungsdaten zu Ihren Standorten und Ihrer Infrastruktur. Der Dienstverbindungspunkt sammelt diese Informationen und übermittelt sie an den Microsoft-Clouddienst. Configuration Manager erfordert, dass diese Daten Updates herunterladen, die für Ihre Umgebung gelten. Wenn Sie den Dienstverbindungspunkt einrichten, können Sie Folgendes angeben: Die Ebene der Daten, die gesammelt werden, und ob diese Daten automatisch (online) oder manuell (offline) übermittelt werden.

Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> Veraltete Funktionalität  

Einige Features, wie z.B. native [Unterstützung für Computer, die auf Intel AMT (Active Management Technology) basieren](#bkmk_AMT), wurden aus der Configuration Manager-Konsole entfernt. Andere Features, wie der Netzwerkzugriffsschutz, wurden vollständig entfernt. Darüber hinaus werden einige ältere Microsoft-Produkte wie Windows Vista, Windows Server 2008 und SQL Server 2008 nicht mehr unterstützt.  

Eine Liste der veralteten Features finden Sie unter [Entfernte und veraltete Elemente](deprecated/removed-and-deprecated.md).  

Details zu unterstützten Produkte, Betriebssystemen und Konfigurationen finden Sie unter [Unterstützte Konfigurationen](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Unterstützung für Intel Active Management Technology (AMT)  

Mit Configuration Manager Current Branch wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt. AMT-basierte Computer werden weiterhin vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Microsoft Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html) verwenden. Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

Das Entfernen integrierter AMT für Configuration Manager umfasst die Out-of-Band-Verwaltung. Die Standortsystemrolle des Out-of-Band-Verwaltungspunkts ist nicht mehr verfügbar.  

> [!Note]
> Diese Änderung hat keine Auswirkung auf die Out-Band-Verwaltung in System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Änderungen an der Funktionalität

In den folgenden Abschnitten werden einige der wesentlichen Änderungen in den Funktionsbereichen zwischen System Center 2012 R2 Configuration Manager und Version 1511 von Configuration Manager (Current Branch) zusammengefasst. Weitere Informationen zu neueren Funktionsänderungen finden Sie unter [Neuigkeiten zu inkrementellen Versionen](whats-new-incremental-versions.md).

### <a name="client-deployment"></a>Clientbereitstellung  

Configuration Manager führt ein neues Feature ein, mit dem neue Versionen des Configuration Manager-Clients getestet werden können, bevor der Rest des Standorts mit der neuen Software aktualisiert wird. Sie können eine Präproduktionssammlung einrichten, in der ein neuer Client als Pilot getestet wird. Sobald Sie mit der neuen Clientsoftware in der Präproduktion zufrieden sind, können Sie den Client heraufstufen, um den Rest des Standorts automatisch mit der neuen Version zu aktualisieren.  

Weitere Informationen zum Testen von Clients finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung](../../clients/manage/upgrade/test-client-upgrades.md).  

### <a name="os-deployment"></a>Bereitstellung des Betriebssystems  

Beachten Sie die folgenden Änderungen an der Betriebssystembereitstellung:

- Im Tasksequenzerstellungs-Assistenten ist ein neuer Tasksequenztyp verfügbar: **Ein Betriebssystem mithilfe eines Aktualisierungspakets aktualisieren**. Er erstellt die Schritte für das Upgrade von Computern von Windows 7 oder Windows 8.1 auf Windows 10. Weitere Informationen finden Sie unter [Aktualisieren von Windows auf die neueste Version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Der Windows PE-Peercache ist jetzt verfügbar, wenn Sie Betriebssysteme bereitstellen. Computer, auf denen eine Tasksequenz zum Bereitstellen eines Betriebssystems ausgeführt wird, können mithilfe des Windows PE-Peercaches Inhalte von einer Peercachequelle abrufen, anstatt sie von einem Verteilungspunkt herunterzuladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist. Weitere Informationen finden Sie unter [Vorbereiten des Windows PE-Peercache zum Reduzieren des WAN-Datenverkehrs](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- Sie können nun den Zustand von Windows as a Service in Ihrer Umgebung anzeigen. Sie können auch Wartungspläne erstellen, um Bereitstellungsringe zu bilden und sicherzustellen, dass Windows 10 Current Branch-Computer bei Veröffentlichung neuer Builds auf dem neuesten Stand gehalten werden. Zusätzlich können Sie auch Warnungen anzeigen, wenn der Support für den Build für Windows 10-Clients sich dem Ende nähert. Weitere Informationen finden Sie unter [Manage Windows as a service (Verwalten von Windows as a Service)](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### <a name="application-management"></a>Anwendungsverwaltung  

Beachten Sie die folgenden Änderungen der Anwendungsverwaltung:

- Configuration Manager ermöglicht Ihnen das Bereitstellen von UWP-Apps (Universelle Windows-Plattform) für Geräte mit Windows 10 und höher. Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../../apps/get-started/creating-windows-applications.md).  

- Das Softwarecenter weist einen neuen, modernen Look auf. Für Benutzer verfügbare Apps, die bisher nur im Anwendungskatalog angezeigt wurden, werden jetzt im Softwarecenter auf der Registerkarte „Anwendungen“ angezeigt. Durch dieses Verhalten sind diese Bereitstellungen leichter auffindbar, und Benutzer müssen nicht auf den separaten Anwendungskatalog verweisen. Außerdem ist kein Browser mit Silverlight-Unterstützung mehr erforderlich. Weitere Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

- Mit dem neuen Anwendungstyp „Windows Installer über MDM“ können Sie Windows Installer-basierte Apps auf registrierten PCs unter Windows 10 erstellen und bereitstellen. Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../../apps/get-started/creating-windows-applications.md).  

- Um in Configuration Manager 2012 einen Link zu einer App im Windows Store anzugeben, können Sie entweder den Link direkt angeben oder zu einem Remotecomputer navigieren, auf dem die App installiert ist. In Configuration Manager Current Branch können Sie weiterhin den Link direkt eingeben. Doch anstatt zu einem Referenzcomputer zu navigieren, können Sie den Store direkt in der Configuration Manager-Konsole nach der App durchsuchen.  

### <a name="software-updates"></a>Softwareupdates  

Beachten Sie die folgenden Änderungen von Softwareupdates:

- Configuration Manager kann jetzt den Unterschied zwischen Methoden der Softwareupdateverwaltung für Computer erkennen. Insbesondere kann jetzt zwischen einem Windows 10-Computer, der eine Verbindung mit Windows Update for Business (WUfB) herstellt, und einem Computer, der mit WSUS verbunden ist, unterschieden werden. Das **UseWUServer**-Attribut ist neu und gibt an, ob der Computer mit WUfB verwaltet wird. Sie können diese Einstellung in einer Sammlung verwenden, um diese Computer aus der Verwaltung von Softwareupdates zu entfernen. Weitere Informationen finden Sie unter [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- Jetzt können Sie den WSUS-Bereinigungstask von der Configuration Manager-Konsole aus planen und ausführen. Wenn Sie in den Eigenschaften von **Softwareupdatepunkt-Komponente** die Ausführung der WSUS-Bereinigungsaufgabe auswählen, wird sie bei der nächsten Softwareupdatesynchronisierung ausgeführt. Die abgelaufenen Softwareupdates werden auf dem WSUS-Server auf den Status „Abgelehnt“ festgelegt, und der Windows Update-Agent auf Computern durchsucht diese Softwareupdates daraufhin nicht mehr. Weitere Informationen finden Sie unter [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

Beachten Sie die folgenden Änderungen von Konformitätseinstellungen:

- Configuration Manager verbessert den Workflow zum Erstellen von Konfigurationselementen. Wenn Sie jetzt ein Konfigurationselement erstellen und unterstützte Plattformen auswählen, sind nur die für die Plattform relevanten Einstellungen verfügbar. Informationen hierzu finden Sie unter [Erste Schritte mit Konformitätseinstellungen](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- Der **Assistent zum Erstellen von Konfigurationselementen** erleichtert die Auswahl des Konfigurationselementtyps, den Sie erstellen möchten. Darüber hinaus sind neue und aktualisierte Konfigurationselemente für Folgendes verfügbar:  

    - Mit dem Configuration Manager-Client verwaltete Windows 10-Geräte  

    - Mit dem Configuration Manager-Client verwaltete Max OS X-Geräte  

    - Mit dem Configuration Manager-Client verwaltete Windows Desktop- und Servercomputer  

    - Ohne den Configuration Manager-Client verwaltete Windows 8.1- und Windows 10-Geräte  

    Weitere Informationen finden Sie unter [Erstellen von Konfigurationselementen](../../../compliance/deploy-use/create-configuration-items.md).  

- Unterstützung für die Verwaltung von Einstellungen auf Mac OS X-Computern, die mit dem Configuration Manager-Client verwaltet werden.

### <a name="on-premises-mobile-device-management"></a>Lokale Verwaltung mobiler Geräte  

Sie können nun mobile Geräte mithilfe der lokalen Configuration Manager-Infrastruktur verwalten. Alle Geräte- und Verwaltungsdaten werden lokal verarbeitet und sind nicht Teil von Microsoft Intune oder anderen Clouddiensten. Diese Art von Gerätemanagement erfordert keine Clientsoftware. Configuration Manager verwaltet Geräte mit Funktionen, die in das Gerätebetriebssystem integriert sind.  

Weitere Informationen finden Sie unter [Lokale MDM (Mobile Device Management) in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## <a name="next-steps"></a>Nächste Schritte

[Neuigkeiten zu inkrementellen Versionen](whats-new-incremental-versions.md)
