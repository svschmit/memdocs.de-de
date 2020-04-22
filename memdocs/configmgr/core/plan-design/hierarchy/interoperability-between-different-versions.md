---
title: Interoperabilität zwischen Versionen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Konflikte zwischen verschiedenen Configuration Manager-Hierarchien im selben Netzwerk vermieden werden können.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693518"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Interoperabilität zwischen verschiedenen Versionen von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können mehrere unabhängige Hierarchien von Configuration Manager im selben Netzwerk installieren und betreiben. Da unterschiedliche Hierarchien von Configuration Manager außerhalb des Migrationsprozesses nicht zusammenarbeiten, erfordert jede Hierarchie entsprechende Konfigurationen, um Konflikte zu vermeiden. Außerdem können Sie bestimmte Konfigurationen vornehmen, damit von Ihnen verwaltete Ressourcen jeweils mit den Standortsystemen der richtigen Hierarchie interagieren können.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a> Interoperabilität zwischen Current Branch und früheren Versionen  

Standorte mit unterschiedlichen Versionen können in derselben Configuration Manager-Hierarchie nicht nebeneinander existieren. Die einzigen Ausnahmen bestehen während des Prozesses der folgenden Upgradeszenarios:

- Upgrade von System Center 2012 Configuration Manager auf Current Branch von Configuration Manager
- Upgrade von einer Current Branch-Version von Configuration Manager auf eine neuere Version mithilfe konsoleninterner Updates

Sie können einen Standort und eine Hierarchie einer Current Branch-Version von Configuration Manager zusammen mit einem vorhandenen Standort oder einer vorhandenen Hierarchie von System Center 2012 Configuration Manager bereitstellen. Treffen Sie Vorkehrungen, die verhindern, dass Clients einer der Versionen versuchen, einem Standort der jeweils anderen Version beizutreten.

Wenn beispielsweise mindestens zwei Configuration Manager-Hierarchien [überlappende Grenzen](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) haben, die dieselben Netzwerkstandorte einschließen, weisen Sie jedem neuen Client einem bestimmten Standort zu, anstatt die automatische Standortzuweisung zu verwenden. Weitere Informationen finden Sie unter [Zuweisen von Clients zu einem Standort](../../clients/deploy/assign-clients-to-a-site.md).  

Außerdem können Sie keinen Client aus System Center 2012 Configuration Manager auf einem Computer installieren, der eine Standortsystemrolle aus Current Branch von System Center hostet. Ebenso können Sie keinen Client mit Current Branch von Configuration Manager auf einem Computer installieren, der eine Standortsystemrolle aus System Center 2012 Configuration Manager hostet.  

Die folgenden Clients und Verbindungen werden nicht unterstützt:  

- System Center 2012 Configuration Manager oder frühere Computerclientversionen  

- System Center 2012 Configuration Manager oder frühere Geräteverwaltungsclients  

- Windows CE Platform Builder-Geräteverwaltungsclient (alle Versionen)  

- VPN-Verbindung für System Center Mobile Device Manager  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Überlegungen zur Clientstandortzuweisung  

Konfigurations-Manager-Clients können nur einem einzigen primären Standort zugewiesen werden. Die tatsächliche Standortzuweisung eines Clients lässt sich nicht vorhersagen, wenn alle der folgenden Bedingungen zutreffen:

- Sie verwenden die automatische Standortzuweisung, um Clients während der Clientinstallation einem Standort zuzuweisen
- Mehr als eine Begrenzungsgruppe beinhaltet dieselbe Begrenzung
- Den Begrenzungsgruppen sind unterschiedliche Standorte zugewiesen

Wenn sich die Grenzen mehrerer Configuration Manager-Standorte und -Hierarchien überlappen, werden Clients möglicherweise nicht dem von Ihnen erwarteten Standort oder sogar gar keinem Standort zugewiesen.  

Clients mit Current Branch von Configuration Manager überprüfen die Version eines Standorts bevor sie eine Standortzuweisung durchführen. Wenn sich die Standortgrenzen überschneiden, können einem Standort mit einer älteren Version keine Clients zugewiesen werden. Ältere System Center 2012 Configuration Manager-Clients werden jedoch unter Umständen fälschlicherweise einem aktuelleren Standort mit Current Branch von Configuration Manager zugewiesen.  

Damit Clients nicht irrtümlich einem falschen Standort zugewiesen werden, wenn zwei Hierarchien überlappende Grenzen haben, konfigurieren Sie die Clientinstallationsparameter so, dass Clients einem bestimmten Standort zugewiesen werden.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> Configuration Manager-Einschränkungen in einer Hierarchie mit unterschiedlichen Versionen  

Wenn Sie für eine Hierarchie mit Current Branch von Configuration Manager ein Upgrade durchführen, gibt es Zeiten, zu denen verschiedene Standorte verschiedene Versionsstände haben. Sie führen beispielsweise zuerst ein Upgrade auf den Standort der zentralen Verwaltung aus. Aufgrund der Wartungsfenster des Standorts führen Sie das Upgrade für den primären Standort erst zu einem späteren Zeitpunkt aus.  

Wenn in verschiedenen Standorten einer einzelnen Hierarchie unterschiedliche Versionen ausgeführt werden, stehen einige Funktionen nicht zur Verfügung. Dieses Verhalten kann sich darauf auswirken, wie Sie Configuration Manager-Objekte in der Configuration Manager-Konsole verwalten und welche Funktionen für Clients verfügbar sind. Normalerweise sind Funktionen aus neueren Configuration Manager-Versionen für Standorte oder Clients mit einer niedrigeren Service Pack-Version nicht verfügbar.  

### <a name="network-access-account"></a>Netzwerkzugriffskonto

Sie upgraden den Standort der zentralen Verwaltung auf Current Branch von Configuration Manager. Die Details zum Netzwerkzugriffskonto werden in einer Configuration Manager-Konsole angezeigt, die mit dem aktualisierten Standort verknüpft ist. Es werden keine Kontoinformationen von Standorten angezeigt, die noch System Center 2012 Configuration Manager ausführen.

Nachdem der primäre Standort auf dieselbe Version wie der Standort der zentralen Verwaltung aktualisiert wurde, werden die Kontodetails in der Konsole angezeigt.

Dasselbe Verhalten gilt, wenn Updates zwischen Versionen von Configuration Manager durchgeführt werden.

### <a name="boot-images-for-os-deployment"></a>Startimages für die Betriebssystembereitstellung

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>Beim Upgrade von System Center 2012 Configuration Manager auf Current Branch von Configuration Manager

Wenn für den Standort der obersten Ebene einer Hierarchie ein Upgrade auf Current Branch von Configuration Manager ausgeführt wird, werden die Standardstartimages automatisch auf Startimages aktualisiert, die auf Windows Assessment und Deployment Kit 10 (Windows ADK) basieren. Verwenden Sie diese Startimages nur für Bereitstellungen für Clients an Standorten mit Current Branch von Configuration Manager. Weitere Informationen finden Sie unter [Planen der Interoperabilität der Betriebssystembereitstellung](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Beim Upgrade zwischen Current Branch-Versionen von Configuration Manager

Solange neue Versionen von Configuration Manager nicht die aktuell verwendete Windows ADK-Version aktualisieren, gibt es keine Auswirkungen auf die Startimages.

### <a name="new-task-sequence-steps"></a>Neue Tasksequenzschritte

Wenn Sie eine Tasksequenz mit einem Schritt erstellen, der in einer Version von Configuration Manager eingeführt wurde und in einer früheren Version nicht verfügbar ist, können die folgenden Problemen auftreten:

- Es tritt ein Fehler auf, wenn Sie versuchen, die Tasksequenz von einem Standort aus zu bearbeiten, auf dem eine vorherige Version von Configuration Manager ausgeführt wird.

- Die Tasksequenz kann nicht auf einem Computer ausgeführt werden, auf dem eine vorherige Version des Configuration Manager-Clients ausgeführt wird.

### <a name="client-to-down-level-management-point-communications"></a>Kommunikation von Clients mit Verwaltungspunkten mit niedrigeren Versionen

Ein Configuration Manager-Client, der mit einem Verwaltungspunkt eines Standorts mit einer niedrigeren Version als der Version des Clients kommuniziert, kann nur die Funktionen nutzen, die von der niedrigeren Version von Configuration Manager unterstützt werden. Wenn Sie beispielsweise Inhalte eines kürzlich aktualisierten Standorts mit Current Branch von Configuration Manager auf einem Client bereitstellen, der mit einem Verwaltungspunkt kommuniziert, der noch nicht auf diese Version aktualisiert wurde, kann dieser Client die neuen Funktionen der neuesten Version nicht verwenden.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Paket- und Tasksequenzbereitstellungen für Legacyclients

<!-- SCCMDocs-pr issue #3493 -->

Ab der Version 1902 können Sie ein Paket oder eine Tasksequenz nicht für einen Client der Version 5.7730 oder älter bereitstellen. Dies können Sie umgehen, indem Sie den Client auf eine neuere Version aktualisieren.

## <a name="software-updates"></a>Softwareupdates

### <a name="orchestration-groups"></a>Orchestrierungsgruppen

In Version 2002 eingeführte Orchestrierungsgruppen können nicht in einer Hierarchie mit gemischten Versionen verwendet werden. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Interoperabilität für die Configuration Manager-Konsole  

Dieser Abschnitt enthält Informationen zur Verwendung der Configuration Manager-Konsole in einer Umgebung mit gemischten Configuration Manager-Versionen.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>Eine Umgebung mit System Center 2012 Configuration Manager und Current Branch von Configuration Manager

Zum Verwalten eines Configuration Manager-Standorts muss auf der Konsole und am Standort, mit dem die Konsole verbunden ist, dieselbe Configuration Manager-Version ausgeführt werden. So kann beispielsweise nicht eine System Center 2012 Configuration Manager-Konsole zum Verwalten eines Standorts mit Current Branch von Configuration Manager und umgekehrt verwendet werden.

Die parallele Installation der System Center 2012 Configuration Manager-Konsole und der Current Branch-Konsole von Configuration Manager auf einem Computer wird nicht unterstützt.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Eine Umgebung mit mehreren Versionen von Configuration Manager

Current Branch von Configuration Manager unterstützt keine Installation von mehreren Configuration Manager-Konsolen auf einem Computer. Wenn Sie mehrere, zu unterschiedlichen Configuration Manager-Versionen gehörende Konsolen verwenden möchten, müssen Sie diese auf unterschiedlichen Computern installieren.

Bei laufender Aktualisierung von Standorten in einer Hierarchie auf eine neue Version können Sie eine Konsole mit einem Standort verbinden, auf dem eine neuere Version ausgeführt wird, und Informationen zu anderen Standorten in dieser Hierarchie anzeigen. Diese Konfiguration wird jedoch nicht empfohlen. Es besteht die Möglichkeit, dass die Unterschiede zwischen der Konsolenversion und der Configuration Manager-Standortversion zu Datenproblemen führen. Einige der in der neuesten Produktversion verfügbaren Features sind in der Konsole nicht verfügbar.

Das Verwalten eines Standorts bei Verwendung einer Konsole mit einer Version, die nicht mit der Standortversion übereinstimmt, wird nicht unterstützt. Dies kann dazu führen, dass Daten verloren gehen und dass Ihre Website gefährdet wird. Es wird z.B. nicht unterstützt, eine Konsole der Version 1610 zu verwenden, um einen Standort zu verwalten, der Version 1606 ausführt.
