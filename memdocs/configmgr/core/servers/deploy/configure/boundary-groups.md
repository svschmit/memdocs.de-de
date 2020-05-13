---
title: Konfigurieren von Begrenzungsgruppen
titleSuffix: Configuration Manager
description: Unterstützen Sie Clients bei der Suche nach Standortsystemen, indem Sie Begrenzungsgruppen für die logische Organisation zusammenhängender Netzwerkadressen verwenden, die auch als Grenzen bezeichnet werden
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce77c43f49556b3a60e36f05127f82d4d135762a
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643257"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Konfigurieren von Begrenzungsgruppen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Begrenzungsgruppen in Configuration Manager für die logische Organisation zusammenhängender Netzwerkadressen ([Grenzen](boundaries.md)), um die Verwaltung Ihrer Infrastruktur zu erleichtern. Weisen Sie Begrenzungsgruppen Grenzen zu, bevor Sie die Begrenzungsgruppe verwenden.

Standardmäßig erstellt Configuration Manager eine Standard-Standortbegrenzungsgruppe an jedem Standort.

Ordnen Sie der Begrenzungsgruppe Grenzen (Netzwerkadressen) und Standortsystemrollen wie Verteilungspunkte zu, um Begrenzungsgruppen zu konfigurieren. Durch diese Konfiguration können Clients mit Standortsystemservern wie Verteilungspunkten verknüpft werden, die sich in der Nähe der Clients auf dem Netzwerk befinden.

Wenn Sie die Verfügbarkeit der Server für einen größeren Bereich von Netzwerkadressen erhöhen möchten, müssen Sie mehreren Begrenzungsgruppen dieselbe Grenze und denselben Server zuweisen.

Client verwenden eine Begrenzungsgruppe für Folgendes:  

- Automatische Standortzuweisung  
- um einen Standortsystemserver zu finden, der einen Dienst bereitstellen kann, darunter z.B.:

  - Verteilungspunkte für Inhaltsstandorte  
  - Softwareupdatepunkte  
  - Zustandsmigrationspunkte  

    > [!NOTE]
    > Bei Zustandsmigrationspunkten werden keine Fallbackbeziehungen verwendet. Weitere Informationen finden Sie unter [Fallback](#fallback).

  - Bevorzugte Verwaltungspunkte  

    > [!NOTE]  
    > Wenn Sie bevorzugte Verwaltungspunkte verwenden, aktivieren Sie diese Option für die Hierarchie und nicht in der Konfiguration der Begrenzungsgruppe. Weitere Informationen finden Sie unter [So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Cloudverwaltungsgateway (ab Version 1902)

## <a name="boundary-groups-and-relationships"></a>Begrenzungsgruppen und Beziehungen

Für jede Begrenzungsgruppe in Ihrer Hierarchie können Sie folgende Zuweisungen vornehmen:

- Eine oder mehrere Grenzen. Bei der **aktuellen** Begrenzungsgruppe eines Clients handelt es sich um eine Netzwerkadresse, die als Grenze definiert ist, die einer bestimmten Begrenzungsgruppe zugewiesen ist. Ein Client kann mehr als eine aktuelle Begrenzungsgruppe aufweisen.  

- Eine oder mehrere Standortsystemrollen. Clients können immer Rollen verwenden, die mit der aktuellen Begrenzungsgruppe verknüpft sind. Je nach zusätzlichen Konfigurationen haben sie die Möglichkeit, Rollen in zusätzlichen Begrenzungsgruppen zu verwenden.  

Für jede von Ihnen erstellte Begrenzungsgruppe können Sie einen unidirektionalen Link zu einer anderen Begrenzungsgruppe konfigurieren. Dieser Link wird als **Beziehung** bezeichnet. Die Begrenzungsgruppen, mit denen Sie verknüpfen, heißen **Nachbarbegrenzungsgruppen**. Eine Begrenzungsgruppe kann mehrere Beziehungen haben, jeweils mit bestimmten Nachbarbegrenzungsgruppen.

Wenn ein Client in seiner aktuellen Begrenzungsgruppe kein verfügbares Standortsystem ausfindig machen kann, wird mit der Konfiguration jeder Beziehung festgelegt, wann mit der Suche nach einer verfügbaren benachbarten Begrenzungsgruppe begonnen werden kann. Diese Suche in zusätzlichen Gruppen wird als **Fallback** bezeichnet.

Weitere Informationen finden Sie in den folgenden Anleitungen:  

- [Erstellen einer Begrenzungsgruppe](boundary-group-procedures.md#bkmk_create)  
- [Konfigurieren einer Begrenzungsgruppe](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a> Anzeigen von Begrenzungsgruppen für Geräte

<!--6521835-->

Ab Version 2002 können Sie die Begrenzungsgruppen für spezifische Geräte anzeigen, um das Identifizieren und Behandeln von Problemen beim Geräteverhalten mit Begrenzungsgruppen zu erleichtern. Fügen Sie der Listenansicht im Knoten **Geräte** oder wenn Sie die Mitglieder einer **Gerätesammlung** anzeigen die neue Spalte **Begrenzungsgruppen** hinzu.

- Wenn sich ein Gerät in mehr als einer Begrenzungsgruppe befindet, handelt es sich bei dem Wert um eine durch Trennzeichen getrennte Liste von Begrenzungsgruppennamen.

- Die Daten werden aktualisiert, wenn der Client eine Standortanforderung an den Standort übermittelt, oder maximal alle 24 Stunden.

- Wenn ein Client Roaming durchführt und kein Mitglied einer Begrenzungsgruppe ist, ist der Wert leer.

> [!NOTE]
> Bei diesen Informationen handelt es sich um Standortdaten, die nur an primären Standorten verfügbar sind. Ihnen wird kein Wert für diese Spalte angezeigt, wenn Sie eine Verbindung zwischen Configuration Manager und dem Standort der zentralen Verwaltung herstellen.

## <a name="fallback"></a>Fallback

Wenn Clients in ihrer aktuellen Begrenzungsgruppe kein verfügbares Standortsystem finden können, sollten Sie zur Vermeidung von Problemen für das Fallbackverhalten die Beziehung zwischen Begrenzungsgruppen definieren. Durch Fallback kann ein Client seine Suche auf zusätzliche Begrenzungsgruppen erweitern, um ein verfügbares Standortsystem zu finden.

Beziehungen werden auf der Registerkarte **Beziehungen** in den Eigenschaften der Begrenzungsgruppe. Wenn Sie eine Beziehung konfigurieren, definieren Sie eine Verknüpfung mit einer Nachbarbegrenzungsgruppe. Konfigurieren Sie für jeden unterstützten Typ von Standortsystemrollen unabhängige Fallbackeinstellungen für die jeweilige benachbarte Begrenzungsgruppe. Weitere Informationen finden Sie unter [Konfigurieren des Fallbackverhaltens](boundary-group-procedures.md#bkmk_bg-fallback).

Wenn Sie beispielsweise eine Beziehung mit einer bestimmten Begrenzungsgruppe konfigurieren, können Sie festlegen, dass das Fallback für Verteilungspunkte nach 20 Minuten erfolgt. Der Standardwert ist 120 Minuten. Ein ausführlicheres Beispiel finden Sie unter [Beispiel für das Verwenden von Begrenzungsgruppen](#example-of-using-boundary-groups).

Wenn ein Client in seiner aktuellen Begrenzungsgruppe keine verfügbare Standortsystemrolle finden kann, verwendet er die Fallbackzeit in Minuten. Diese Fallbackzeit bestimmt, wann der Client mit der Suche nach einem verfügbaren Standortsystem beginnt, das mit der benachbarten Begrenzungsgruppe verknüpft ist.  

Wenn ein Client kein verfügbares Standortsystem finden kann, beginnt er, Speicherorte in benachbarten Begrenzungsgruppen zu durchsuchen. Durch dieses Verhalten wird der Pool verfügbarer Standortsysteme vergrößert. Die Konfiguration von Begrenzungsgruppen und den zugehörigen Beziehungen definiert die Clientverwendung dieser Pools mit verfügbaren Standortsystemen.

- Eine Begrenzungsgruppe kann mehr als eine Beziehung haben. Mit dieser Konfiguration können Sie den Fallback für alle Standortsystemtypen für unterschiedliche Nachbarn konfigurieren, der nach unterschiedlich langen Zeitspannen erfolgen soll.  

- Ziel des Fallbacks eines Clients kann nur eine Begrenzungsgruppe sein, die ein direkter Nachbar der aktuellen Begrenzungsgruppe ist.  

- Wenn ein Client Mitglied mehrerer Begrenzungsgruppen ist, wird die aktuelle Begrenzungsgruppe als die Gesamtheit aller seiner Begrenzungsgruppen definiert. Anschließend erfolgt ein Fallback dieses Clients auf einen Nachbarn einer beliebigen dieser ursprünglichen Begrenzungsgruppen.  

> [!NOTE]
> Bei der Rolle „Zustandsmigrationspunkt“ werden keine Fallbackbeziehungen verwendet. Wenn Sie auf demselben Standortsystemserver sowohl die Rolle „Zustandsmigrationspunkt“ als auch die Rolle „Verteilungspunkt“ hinzufügen, konfigurieren Sie kein Fallback in der Begrenzungsgruppe dieses Servers. Wenn Sie ein Fallback der Begrenzungsgruppe für den Verteilungspunkt benötigen, fügen Sie die Rolle „Zustandsmigrationspunkt“ auf einem anderen Standortsystemserver hinzu.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>Die standardmäßige Standortbegrenzungsgruppe

Sie können Ihre eigene Begrenzungsgruppen erstellen. Jeder Standort verfügt über eine Standard-Standortbegrenzungsgruppe, die von Configuration Manager erstellt wird. Diese Gruppe heißt **Default-Site-Boundary-Group&lt;sitecode>** . Die Gruppe des Standorts ABC hieße z.B. **Default-Site-Boundary-Group&lt;ABC>** .

Für jede von Ihnen erstellte Begrenzungsgruppe erstellt Configuration Manager automatisch einen implizierten Link zu jeder Standard-Standortbegrenzungsgruppe in der Hierarchie.  

- Der implizierte Link ist eine Standardoption für ein Fallback von der aktuellen Begrenzungsgruppe zur Standardbegrenzungsgruppe des Standorts. Die Standardfallbackzeit ist 120 Minuten.  

- Bei Clients, die sich nicht in einer mit einer anderen Begrenzungsgruppe verknüpften Grenze befinden: Verwenden Sie die standardmäßige Standortbegrenzungsgruppe des zugewiesenen Standorts, um gültige Standortsystemrollen zu ermitteln.  

So verwalten Sie das Fallback auf die Standard-Standortbegrenzungsgruppe:  

- Öffnen Sie die Einstellungen der standardmäßigen Standortbegrenzungsgruppe, und ändern Sie die Werte auf der Registerkarte **Standardverhalten**. Die Änderungen, die Sie hier vornehmen, gelten für *alle* implizierten Links zu dieser Begrenzungsgruppe. Diese Standardeinstellungen können außer Kraft gesetzt werden, indem Sie von einer anderen Begrenzungsgruppe einen expliziten Link zu dieser standardmäßigen Standortbegrenzungsgruppe konfigurieren.  

- Öffnen Sie die Eigenschaften einer benutzerdefinierten Begrenzungsgruppe. Ändern Sie die Werte für den expliziten Link in eine standardmäßige Standortbegrenzungsgruppe. Wenn Sie eine neue Zeit (in Minuten) für das Fallback oder das Blockieren des Fallbacks festlegen, wirkt sich diese Änderung nur auf den von Ihnen konfigurierten Link aus. Durch die Konfiguration des expliziten Links werden die Einstellungen auf der Registerkarte **Standardverhalten** der standardmäßigen Standortbegrenzungsgruppe überschrieben.  

## <a name="site-assignment"></a>Standortzuweisung  

Sie können jede Begrenzungsgruppe mit einem zugewiesenen Standort für Clients konfigurieren.  

- Ein neu installierter Client, der die automatische Standortzuweisung verwendet, tritt dem zugewiesenen Standort einer Begrenzungsgruppe bei, die die aktuelle Netzwerkadresse des Clients enthält.  

- Nach Zuweisung zu einem Standort ändert sich die Standortzuweisung eines Clients nicht, wenn sich seine Netzwerkadresse ändert. Angenommen, ein Client wechselt zu einer neuen Netzwerkadresse. Diese Adresse ist eine Grenze in einer Begrenzungsgruppe mit anderer Standortzuweisung. Der dem Client zugewiesene Standort ändert sich nicht.  

- Wenn mithilfe der Active Directory-Systemermittlung eine neue Ressource ermittelt wird, wertet der Standort die Netzwerkinformationen für diese Ressource anhand der Grenzen in Begrenzungsgruppen aus. Dabei wird die neue Ressource einem zugewiesenen Standort zur Verwendung bei einer Clientpushinstallation zugeordnet.  

- Wenn eine Grenze zu mehreren Begrenzungsgruppen gehört, denen verschiedene Standorte zugewiesen sind, wählen Clients einen dieser Standorte nach dem Zufallsprinzip aus.  

- Änderungen am zugewiesenen Standort einer Begrenzungsgruppe betreffen nur neue Standortzuweisungsaktionen. Clients, die bereits zuvor einem Standort zugewiesen wurden, bewerten ihre Standortzuweisung nicht basierend auf Änderungen an der Konfiguration einer Begrenzungsgruppe (oder ihrer eigenen Netzwerkadresse) neu.  

Weitere Informationen zur Standortzuweisung für Clients finden Sie unter [Verwenden der automatischen Standortzuweisung für Computer](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Weitere Informationen zum Konfigurieren der Standortzuweisung finden Sie unter den folgenden Verfahren:

- [Konfigurieren der Standortzuweisung und Auswählen von Standortsystemservern](boundary-group-procedures.md#bkmk_references)
- [Konfigurieren eines Fallbackstandorts für die automatische Standortzuweisung](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Verteilungspunkte

Wenn ein Client den Speicherort eines Verteilungspunkts anfordert, sendet Configuration Manager dem Client eine Liste der Standortsysteme. Diese Standortsysteme weisen den entsprechenden Typ auf, der mit den einzelnen Begrenzungsgruppen verknüpft ist, welche die aktuelle Netzwerkadresse des Clients enthalten:

- **Während der Softwareverteilung** fordern Clients einen Speicherort für Bereitstellungsinhalte in einer gültigen Inhaltsquelle an. Bei diesem Speicherort kann es sich um einen Verteilungspunkt oder eine Peercachequelle handeln.  

- **Während der Bereitstellung des Betriebssystems** fordern Clients einen Speicherort zum Senden oder Empfangen ihrer Zustandsmigrationsinformationen an.  

  - Clients erhalten Inhalt basierend auf dem Verhalten von Begrenzungsgruppen. Weitere Informationen finden Sie unter [Tasksequenzunterstützung für Begrenzungsgruppen](#bkmk_bgr-osd).  

Wenn ein Client während der Inhaltsbereitstellung Inhalte anfordert, die aus einer Quelle in seiner aktuellen Begrenzungsgruppe nicht verfügbar sind, fordert der Client diese Inhalte weiter an. Der Client testet unterschiedliche Inhaltsquellen in seiner aktuellen Begrenzungsgruppe aus, bis der Fallbackzeitraum für eine benachbarte oder die standardmäßige Standortbegrenzungsgruppe erreicht ist. Wenn der Client immer noch keinen Inhalt gefunden hat, erweitert er seine Suche nach Inhaltsquellen auf die benachbarten Begrenzungsgruppen.

Wenn Sie den Inhalt so konfigurieren, dass er bei Bedarf verteilt wird und dieser nicht auf einem Verteilungspunkt verfügbar ist, wenn er von einem Client angefordert wird, überträgt der Standort den Inhalt an diesen Verteilungspunkt. Es besteht die Möglichkeit, dass der Client diesen Server als Inhaltsquelle findet, bevor ein Fallback zur Verwendung einer benachbarten Begrenzungsgruppe durchgeführt wird.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a> Clientinstallation

<!--1358840-->
Bei der Installation des Konfigurations-Manager-Clients kontaktiert der Ccmsetup-Vorgang den Verwaltungspunkt, um den erforderlichen Inhalt zu suchen. Der Verwaltungspunkt gibt Verteilungspunkte basierend auf der Konfiguration der Begrenzungsgruppe zurück. Wenn Sie Beziehungen für die Begrenzungsgruppe definieren, gibt der Verwaltungspunkt Verteilungspunkte in der folgenden Reihenfolge zurück:

1. Aktuelle Begrenzungsgruppe  
2. Benachbarte Begrenzungsgruppen  
3. Die Standardbegrenzungsgruppe des Standorts  

> [!Note]  
> Für den Setupvorgang des Clients wird keine Fallbackzeit verwendet. Damit Inhalte so schnell wie möglich gefunden werden, wird ein sofortiger Fallback auf die nächste Begrenzungsgruppe durchgeführt.
>
> In vorherigen Versionen von Configuration Manager wurden bei dieser Verarbeitung des Verwaltungspunkts nur Verteilungspunkte in der aktuellen Begrenzungsgruppe des Clients zurückgegeben. Wenn kein Inhalt verfügbar war, hat der Setupvorgang Inhalt vom Verwaltungspunkt heruntergeladen. Es gab keine Option für ein Fallback auf Verteilungspunkte in anderen Begrenzungsgruppen, die den erforderlichen Inhalt enthalten könnten.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a> Tasksequenzunterstützung für Begrenzungsgruppen

<!--1359025-->
Wenn ein Gerät eine Tasksequenz ausführt und Inhalt abrufen muss, verwendet es ähnlich wie der Konfigurations-Manager-Client Verhaltensweisen von Begrenzungsgruppen.

Konfigurieren Seite dieses Verhalten mit den folgenden Einstellungen auf der Seite **Verteilungspunkte** der Tasksequenzbereitstellung:

- **Remoteverteilungspunkt verwenden, wenn kein lokaler Verteilungspunkt verfügbar ist**: Für diese Bereitstellung kann die Tasksequenz auf Verteilungspunkte in einer benachbarten Begrenzungsgruppe zurückgreifen.  

- **Clients die Verwendung von Verteilungspunkten aus der Standard-Standortbegrenzungsgruppe gestatten**: Für diese Bereitstellung kann die Tasksequenz auf Verteilungspunkte in einer Begrenzungsgruppe am Standardstandort zurückgreifen.  

Stellen Sie sicher, dass die Clients auf dem neuesten Stand sind, um dieses neue Verhalten zu verwenden.

#### <a name="location-priority"></a>Priorität des Speicherorts  

Die Tasksequenz versucht Inhalt in folgender Reihenfolge abzurufen:  

1. Peercachequellen  

2. Verteilungspunkte in der *aktuellen* Begrenzungsgruppe  

3. Verteilungspunkte in *benachbarten* Begrenzungsgruppen  

    > [!Important]  
    > Aufgrund der Echtzeitverarbeitung von Tasksequenzen wird nicht auf die Failoverzeit auf eine benachbarte Begrenzungsgruppe gewartet. Die Failoverzeiten geben die Priorisierung der benachbarten Begrenzungsgruppen vor. Wenn die Tasksequenz beispielweise daran scheitert, Inhalt von einem Verteilungspunkt in der aktuellen Begrenzungsgruppe abzurufen, wird sofort versucht, Inhalt von einem Verteilungspunkt in der benachbarten Begrenzungsgruppe mit der kürzesten Failoverzeit abzurufen. Wenn dieser Vorgang fehlschlägt, wird ein Failover zu einem Verteilungspunkt in einer benachbarten Begrenzungsgruppe mit einer längeren Failoverzeit ausgeführt.  

4. Verteilungspunkte in der *standardmäßigen Standortbegrenzungsgruppe*  

Die Protokolldatei **smsts.log** für die Tasksequenz zeigt die Priorität der Speicherortquellen an, die basierend auf den Bereitstellungseigenschaften verwendet wird.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> Begrenzungsgruppenoptionen für Peerdownloads

<!--1356193, 1358749-->
Begrenzungsgruppen beinhalten die folgenden zusätzlichen Einstellungen, die Ihnen mehr Kontrolle über die Verteilung von Inhalten in Ihrer Umgebung einräumen:  

- [Peerdownloads in dieser Begrenzungsgruppe zulassen](#bkmk_bgoptions1)  

- [Bei Peerdownloads nur Peers in demselben Subnetz verwenden](#bkmk_bgoptions2)  

- [Verteilungspunkte über Peers innerhalb desselben Subnetzes vorziehen](#bkmk_bgoptions3)  

- [Cloudverteilungspunkte Verteilungspunkten vorziehen](#bkmk_bgoptions4)  

Weitere Informationen zum Konfigurieren dieser Einstellungen finden Sie im Artikel zum [Konfigurieren von Begrenzungsgruppen](boundary-group-procedures.md#bkmk_config).

Wenn sich ein Gerät in mehr als einer Begrenzungsgruppe befindet, gelten die folgenden Verhaltensweisen für diese Einstellungen:

- **Peerdownloads in dieser Begrenzungsgruppe zulassen**: Wenn diese Option in einer der Begrenzungsgruppen deaktiviert ist, verwendet der Client keine Übermittlungsoptimierung.
- **Bei Peerdownloads nur Peers in demselben Subnetz verwenden**: Wenn diese Option in einer der Begrenzungsgruppen deaktiviert ist, tritt diese Einstellung in Kraft.
- **Verteilungspunkte über Peers innerhalb desselben Subnetzes vorziehen**: Wenn diese Option in einer der Begrenzungsgruppen deaktiviert ist, tritt diese Einstellung in Kraft.
- **Cloudbasierte Quellen lokalen Quellen vorziehen**: Wenn diese Option in einer der Begrenzungsgruppen deaktiviert ist, tritt diese Einstellung in Kraft.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a> Peerdownloads in dieser Begrenzungsgruppe zulassen

Diese Einstellung ist standardmäßig aktiviert. Der Verwaltungspunkt bietet Clients eine Liste der Speicherorte für Inhalt, die Peerquellen enthält. Diese Einstellung wirkt sich auch auf die Anwendung von Gruppen-IDs für die [Übermittlungsoptimierung](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) aus.  

In zwei häufigen Szenarios sollten Sie erwägen, diese Option zu deaktivieren:  

- Wenn Sie eine Begrenzungsgruppe besitzen, die Grenzen von geografisch verstreuten Speicherorten wie einem VPN enthält. Zwei Clients können sich in der gleichen Begrenzungsgruppe befinden, da sie über VPN verbunden sind, aber an höchst unterschiedlichen Speicherorten, die zur Peerfreigabe von Inhalten nicht geeignet sind.  

- Bei Verwendung einer einzigen, großen Begrenzungsgruppe für die Standortzuweisung, die nicht auf Verteilungspunkte verweist.  

> [!IMPORTANT]
> Wenn sich ein Gerät in mehr als einer Begrenzungsgruppe befindet, stellen Sie sicher, dass diese Einstellung für alle Begrenzungsgruppen des Geräts aktiviert ist. Andernfalls verwendet der Client keine Übermittlungsoptimierung. Beispielsweise wird der Registrierungsschlüssel DOGroupID nicht festgelegt.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a> Bei Peerdownloads nur Peers in demselben Subnetz verwenden

Diese Einstellung ist abhängig von der vorherigen. Wenn Sie diese Option aktivieren, enthält der Verwaltungspunkt nur in der Inhaltsspeicherort-Liste Peerquellen, die sich im gleichen Subnetz wie der Client befinden.

Allgemeine Szenarien für die Aktivierung dieser Option:

- Ihr Begrenzungsgruppenentwurf für die Inhaltsverteilung enthält eine große Begrenzungsgruppe, die andere kleinere Begrenzungsgruppen überlappt. Mit dieser neuen Einstellung enthält die Liste der Inhaltsquellen, die der Verwaltungspunkt für Clients bereitstellt, nur Peerquellen aus demselben Subnetz.

- Sie haben eine einzelne große Begrenzungsgruppe für alle Remotebüro-Standorte. Wenn Sie diese Option aktivieren, teilen Clients nur Inhalte innerhalb des Subnetzes am Remotebüro-Standort, anstatt zu riskieren, Inhalte mit anderen Standorten zu teilen.

Ab Version 2002 können Sie je nach Konfiguration Ihres Netzwerks bestimmte Subnetze für den Abgleich ausschließen. Sie können also beispielsweise eine Grenze einschließen und ein bestimmtes VPN-Subnetz ausschließen. Configuration Manager schließt das Teredo-Standardsubnetz standardmäßig aus (`2001:0000:%`).<!--3555777-->

> [!NOTE]
> Wenn Sie in Version 2002 einen [eigenständigen primären Standort erweitern](../install/prerequisites-for-installing-sites.md#bkmk_expand), um einen Standort der zentralen Verwaltung hinzuzufügen, wird die Subnetzausschlussliste auf die Standardwerte zurückgesetzt. Zum Umgehen dieses Problems führen Sie das PowerShell-Skript nach der Standorterweiterung aus, um die Subnetzausschlussliste für den Standort der zentralen Verwaltung anzupassen.<!-- 6309068 -->

Importieren Sie die Liste der Subnetzausschlüsse als durch Trennzeichen getrennte Zeichenfolge. Verwenden Sie das Prozentzeichen (`%`) als Platzhalterzeichen. Legen Sie für den Standortserver auf der obersten Ebene die eingebettete Eigenschaft **SubnetExclusionList** für die Komponente **SMS_HIERARCHY_MANAGER** in der Klasse **SMS_SCI_Component** fest, oder lesen Sie diese. Weitere Informationen finden Sie unter [WMI-Klasse für den SMS_SCI_Component-Server](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md).

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>PowerShell-Beispielskript zum Aktualisieren der Subnetzausschlussliste

Das folgende Skript ist eine Beispielmethode zum Ändern dieses Werts. Fügen Sie Ihre Subnetze nach `2001:0000:%,172.16.16.0` an die Variable **PropertyValue** an. Dabei handelt es sich um eine durch Trennzeichen getrennte Zeichenfolge. Führen Sie dieses Skript auf dem Standortserver der obersten Ebene Ihrer Hierarchie aus.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Standardmäßig enthält Configuration Manager das Teredo-Subnetz in dieser Liste. Lesen Sie immer zuerst den vorhandenen Wert, wenn Sie die Liste ändern. Fügen Sie der Liste zusätzliche Subnetze hinzu, und legen Sie dann den neuen Wert fest.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a> Verteilungspunkte über Peers innerhalb desselben Subnetzes vorziehen

Standardmäßig priorisiert der Verteilungspunkt Peercachequellen ganz oben in der Liste der Inhaltsspeicherorte. Diese Einstellung kehrt diese Priorität für Clients um, die sich im gleichen Subnetz wie die Peercachequelle befinden.

> [!TIP]
> Dieses Verhalten gilt für den Konfigurations-Manager-Client. Es gilt nicht, wenn die Tasksequenz Inhalte herunterlädt. Wenn die Tasksequenz ausgeführt wird, bevorzugt sie Peercachequellen über Verteilungspunkte.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a> Cloudverteilungspunkte Verteilungspunkten vorziehen

Wenn Sie eine Niederlassung mit einer schnelleren Internetverbindung haben, können Sie jetzt Cloudinhalte priorisieren.  

In Version 1902 heißt diese Einstellung jetzt **Cloudbasierte Quellen lokalen Quellen vorziehen**. Cloudbasierte Quellen umfassen Folgendes:<!-- SCCMDocs#1529 -->

- Cloudverteilungspunkte
- Microsoft Update (in Version 1902 hinzugefügt)

## <a name="software-update-points"></a>Softwareupdatepunkte

Clients verwenden Begrenzungsgruppen zur Auswahl neuer Softwareupdatepunkte. Zur Steuerung, welchen Server ein Client finden kann, können Sie zu verschiedenen Begrenzungsgruppen einzelne Softwareupdatepunkte hinzufügen.

Wenn Sie alle vorhandenen Softwareupdatepunkte zur Standardbegrenzungsgruppe des Standorts hinzufügen, wählt der Client einen Softwareupdatepunkt aus dem Pool der verfügbaren Server aus. Dieses Verhalten ähnelt früheren Versionen von Configuration Manager (Current Branch). Fügen Sie individuelle Softwareupdatepunkte für gesteuertes Auswahl- und Fallbackverhalten zu verschiedenen Begrenzungsgruppen hinzu.

Wenn Sie einen neuen Standort installieren, werden der standardmäßigen Standortbegrenzungsgruppe keine Softwareupdatepunkte hinzugefügt. Weisen Sie Softwarepudatepunkte zu einer Begrenzungsgruppe hinzu, damit Clients sie suchen und nutzen können.

### <a name="fallback-for-software-update-points"></a>Fallback für Softwareupdatepunkte

Das Fallback für Softwareupdatepunkte wird genauso wie für andere Standortsystemrollen konfiguriert, hat aber folgende Probleme:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Neue Clients verwenden Begrenzungsgruppen zur Auswahl von Softwareupdatepunkten

Wenn Sie neue Clients installieren, wählen diese einen Softwareupdatepunkt unter den Servern aus, die den von Ihnen konfigurierten Begrenzungsgruppen zugeordnet sind. Durch dieses Verhalten wird das vorherige Verhalten ersetzt, bei dem die Clients zufällig einen Softwareupdatepunkt aus der Liste der Server auswählen, die sich die Gesamtstruktur des Clients teilen.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Clients verwenden so lange den bisher funktionierenden Softwareupdatepunkt, bis sie ein Fallback ausführen, um einen neuen zu finden

Clients, die bereits über einen Softwareupdatepunkt verfügen, verwenden diesen so lange weiter, bis er nicht erreicht werden kann. Dieses Verhalten betrifft auch die weitere Verwendung eines Softwareupdatepunkts, der nicht mit der aktuellen Begrenzungsgruppe des Clients verknüpft ist.

Dieses Verhalten ist beabsichtigt. Der Client verwendet weiterhin einen vorhandenen Softwareupdatepunkt, auch wenn er sich nicht in der aktuellen Begrenzungsgruppe des Clients befindet. Wenn sich der Softwareupdatepunkt ändert, synchronisiert der Client Daten mit dem neuen Server. Dies verursacht eine erhebliche Netzwerkauslastung. Wenn alle Clients gleichzeitig zu einem neuen Server wechseln, kann durch die Verzögerung beim Übergang eine Komplettauslastung Ihres Netzwerks vermieden werden.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Ein Client versucht immer 120 Minuten lang, den bisher funktionierenden Softwareupdatepunkt zu erreichen, bevor ein Fallback ausgelöst wird

Wenn der Client 120 Minuten lang keinen Kontakt herstellen konnte, kommt es zu einem Fallback. Die Einleitung des Fallbacks führt dazu, dass der Client von seiner aktuellen Begrenzungsgruppe eine Liste der Softwareupdatepunkte erhält. Abhängig von den Fallbackkonfigurationen können auch zusätzliche Softwareupdatepunkte in benachbarten und standardmäßigen Standortbegrenzungsgruppen verfügbar sein.

### <a name="fallback-configurations-for-software-update-points"></a>Fallbackkonfigurationen für Softwareupdatepunkte

Sie können die **Fallbackzeit (in Minuten)** für Softwareupdatepunkte auch auf unter 120 Minuten einstellen. Der Client versucht jedoch weiterhin 120 Minuten lang, seinen ursprünglichen Softwareupdatepunkt zu erreichen. Anschließend erweitert er seine Suche auf zusätzliche Server. Die Fallbackzeiten für Begrenzungsgruppen beginnen, wenn der Client seinen ursprünglichen Server zum ersten Mal nicht erreicht. Wenn der Client seine Suche erweitert, werden am Standort alle Begrenzungsgruppen bereitgestellt, die für weniger als 120 Minuten konfiguriert wurden.

Zum Blockieren des Fallbacks eines Softwareupdatepunkts auf eine benachbarte Begrenzungsgruppe können Sie die Einstellung **Kein Fallback** konfigurieren.

Nachdem er zwei Stunden erfolglos den Kontakt zu seinem ursprünglichen Server gesucht hat, sucht der Client nun mit einer kürzeren Zeitspanne nach einem neuen Softwareupdatepunkt. Durch dieses Verhalten kann der Client die erweiterte Liste potenzieller Softwareupdatepunkte schneller durchgehen.

#### <a name="example"></a>Beispiel

Sie konfigurieren Softwareupdatepunkte in Begrenzungsgruppe *A* so, dass nach **10** Minuten ein Fallback erfolgt. Sie legen dieselbe Einstellung für Begrenzungsgruppe *B* auf **130** Minuten fest. Ein Client in Begrenzungsgruppe *Z* kann seinen letzten bisher funktionierenden Softwareupdatepunkt nicht erreichen.

- Für die nächsten 120 Minuten versucht der Client ausschließlich, seinen ursprünglichen Server in der Begrenzungsgruppe Z zu erreichen. Nach 10 Minuten fügt Configuration Manager die Softwareupdatepunkte aus Begrenzungsgruppe A in den Pool verfügbarer Server ein. Der Client versucht jedoch erst nach Ablauf der 120-minütigen Frist, diese oder einen anderen Server zu kontaktieren.  

- Nachdem der Client versucht hat, den ursprünglichen Softwareupdatepunkt 120 Minuten lang zu kontaktieren, erweitert er seine Suche. Dazu fügt der Client Server aus seiner aktuellen Begrenzungsgruppe und aus benachbarten Begrenzungsgruppen, die für 120 Minuten oder weniger konfiguriert wurden, zum Pool der verfügbaren Softwareupdatepunkte hinzu. In diesem Pool sind die Server der Begrenzungsgruppe A enthalten, die bereits vorher zum Pool der verfügbaren Server hinzugefügt wurden.  

- Nach weiteren 10 Minuten weitet der Client die Suche auf Softwareupdatepunkte in Begrenzungsgruppe B aus. Dieser Zeitraum beträgt insgesamt 130 Minuten, nachdem der Client zum ersten Mal seinen letzten als funktionierend bekannten Softwareupdatepunkt nicht erreicht hat.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Manuell auf einen neuen Softwareupdatepunkt wechseln

Neben dem Fallback können Sie die Clientbenachrichtigung nutzen, um ein Gerät manuell zu einem Wechsel zu einem neuen Softwareupdatepunkt zu zwingen.

Beim Wechseln auf einen neuen Server wird das Fallback verwendet, um diesen zu finden. Clients wechseln während des Prüfzyklus des nächsten Softwareupdates zum neuen Softwareupdatepunkt.<!-- SCCMDocs#1537 -->

Überprüfen Sie die Konfigurationen für Ihre Begrenzungsgruppen. Bevor Sie diese Änderung umsetzen, stellen Sie sicher, dass sich Ihre Softwareupdatepunkte in den richtigen Begrenzungsgruppen befinden.

Weitere Informationen finden Sie unter [Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

## <a name="management-points"></a>Verwaltungspunkte

<!-- 1324594 -->
Konfigurieren Sie Fallbackbeziehungen für Verwaltungspunkte zwischen Begrenzungsgruppen. Dieses Verhalten ermöglicht eine bessere Steuerung der von Clients verwendeten Verwaltungspunkte. Auf der Registerkarte **Beziehungen** der Eigenschaften einer Begrenzungsgruppe gibt es eine Spalte für den Verwaltungspunkt. Wenn Sie eine neue Fallback-Begrenzungsgruppe hinzufügen, ist die Fallbackzeit für den Verwaltungspunkt derzeit immer Null (0). Dieses Verhalten entspricht dem **Standardverhalten** der Standardbegrenzungsgruppe des Standorts.

Zuvor ist ein gängiges Problem aufgetreten, wenn Sie über einen geschützten Verwaltungspunkt in einem sicheren Netzwerk verfügen. Clients im Hauptnetzwerk haben zuvor eine Richtlinie empfangen, die diesen geschützten Verwaltungspunkt enthält, auch wenn sie durch eine Firewall nicht mit diesem Punkt kommunizieren können. Verwenden Sie die Option **Nie ein Fallback durchführen**, um sicherzustellen, dass Clients nur ein Fallback zu Verwaltungspunkten durchführen, mit denen sie kommunizieren können, um dieses Problem in der aktuellen Version zu beheben.

> [!Note]  
> Wenn Sie Fallback für die Verteilungspunkte in der Standardbegrenzungsgruppe des Standorts aktivieren und ein Verwaltungspunkt und Verteilungspunkt zusammengestellt sind, fügt der Standort diesen Verwaltungspunkt auch der Standardbegrenzungsgruppe des Standorts hinzu.<!--VSO 2841292-->  

Wenn sich ein Kunde in einer Begrenzungsgruppe ohne zugewiesenen Verwaltungspunkt befindet, gibt der Standort dem Client die gesamte Liste der Verwaltungspunkte an. Dieses Verhalten stellt sicher, dass ein Client stets eine Liste von Verwaltungspunkten erhält.

Das Fallback bei Verwaltungspunkten in Begrenzungsgruppen ändert das Verhalten während der Clientinstallation („ccmsetup.exe“) nicht. Wenn der anfängliche Verwaltungspunkt nicht in der Befehlszeile mit dem Parameter „/MP“ angegeben wird, empfängt der neue Client die vollständige Liste aller verfügbaren Verwaltungspunkte. Für den anfänglichen Bootstrapprozess verwendet der Client den ersten Verwaltungspunkt, auf den er zugreifen kann. Sobald der Client beim Standort registriert ist, erhält er die gemäß diesem neuen Verhalten ordnungsgemäß sortierte Verwaltungspunktliste.

Weitere Informationen zum Verhalten des Clients zum Abrufen von Inhalt während der Installation finden Sie im Artikel zur [Clientinstallation](#bkmk_ccmsetup).

Wenn Sie beim Clientupgrade den Befehlszeilenparameter „/MP“ nicht angeben, fragt der Client Quellen wie Active Directory und WMI auf verfügbare Verwaltungspunkte ab. Beim Clientupgrade wird die Konfiguration der Begrenzungsgruppe nicht berücksichtigt. <!--VSO 2841292-->  

Damit Clients diese Funktionalität verwenden, aktivieren Sie die folgende Einstellung: **Clients bevorzugen das Verwenden von in Begrenzungsgruppen angegebenen Verwaltungspunkten** unter **Hierarchieeinstellungen**.

> [!Note]  
> Bei Prozessen zur Betriebssystembereitstellung haben Begrenzungsgruppen für Verwaltungspunkte keine Bedeutung.  

### <a name="troubleshooting"></a>Problembehandlung

Im **LocationServices.log** werden neue Einträge angezeigt. Das Attribut **Ort** identifiziert einen der folgenden Zustände:

- **0:** Unbekannt  

- **1:** Der angegebene Verwaltungspunkt befindet sich nur in der standardmäßigen Standortbegrenzungsgruppe für das Fallback.  

- **2:** Der angegebene Verwaltungspunkt befindet sich in einer Remotebegrenzungsgruppe oder einer benachbarten Begrenzungsgruppe. Wenn sich der Verwaltungspunkt sowohl in einer benachbarten als auch der standardmäßigen Standortbegrenzungsgruppe befindet, lautet der Wert für den Ort „2“.  

- **3:** Der angegebene Verwaltungspunkt befindet sich in der lokalen oder aktuellen Begrenzungsgruppe. Wenn sich der Verwaltungspunkt sowohl in der aktuellen und entweder in einer benachbarten oder der standardmäßigen Standortbegrenzungsgruppe befindet, lautet der Wert für den Ort „3“. Wenn Sie die Einstellung für bevorzugte Verwaltungspunkte in den Hierarchieeinstellungen nicht aktivieren, lautet der Ort immer „3“, unabhängig davon, in welcher Begrenzungsgruppe sich der Verwaltungspunkt befindet.  

Clients verwenden zuerst lokale Verwaltungspunkte (Ort 3), danach Remotepunkte (Ort 2), dann Fallbackpunkte (Ort 1).

Wenn ein Client innerhalb von 10 Minuten fünf Fehler empfängt und mit keinem Verwaltungspunkt in der aktuellen Begrenzungsgruppe kommunizieren kann, versucht er, einen Verwaltungspunkt in einer benachbarten Begrenzungsgruppe oder der standardmäßigen Standortbegrenzungsgruppe zu kontaktieren. Wenn der Verwaltungspunkt in der aktuellen Begrenzungsgruppe zu einem späteren Zeitpunkt wieder online geschaltet wird, kehrt der Client beim nächsten Aktualisierungszyklus zum lokalen Verwaltungspunkt zurück. Der Aktualisierungszyklus beträgt 24 Stunden. Er beginnt ebenfalls von Neuem, wenn der Configuration Manager-Agent-Dienst neu gestartet wird.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a> Bevorzugte Verwaltungspunkte

> [!Note]
> Das Verhalten dieser Hierarchieeinstellung, **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**, wurde in Version 1802 geändert. Wenn Sie diese Einstellung aktivieren, verwendet Configuration Manager die Begrenzungsgruppenfunktion für den zugewiesenen Verwaltungspunkt. Weitere Informationen finden Sie unter [Verwaltungspunkte](#management-points).

Bevorzugte Verwaltungspunkte ermöglichen einem Client die Identifikation eines Verwaltungspunkts, der seiner aktuellen Netzwerkadresse (oder Begrenzung) zugeordnet ist.  

- Ein Client versucht zunächst, einen bevorzugten Verwaltungspunkt seines zugewiesenen Standorts zu verwenden, bevor er einen Verwaltungspunkt seines zugewiesenen Standorts verwendet, der nicht als bevorzugt konfiguriert wurde.  

- Aktivieren Sie für die Verwendung dieser Option **Clients bevorzugen die Verwendung von in Begrenzungsgruppen angegebenen Verwaltungspunkten** unter **Hierarchieeinstellungen**. Konfigurieren Sie anschließend Begrenzungsgruppen an den einzelnen primären Standorten. Schließen Sie die Verwaltungspunkte ein, die mit den zugehörigen Grenzen dieser Begrenzungsgruppe verknüpft werden sollten. Weitere Informationen finden Sie unter [So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte](boundary-group-procedures.md#bkmk_proc-prefer).  

- Wenn Sie bevorzugte Verwaltungspunkte konfigurieren und ein Client seine Liste der Verwaltungspunkte organisiert, ordnet er die bevorzugten Verwaltungspunkte am Anfang seiner Liste an. Diese Liste enthält sämtliche Verwaltungspunkte von den zugewiesenen Standorten des Clients.  

> [!NOTE]  
> Clientroaming bedeutet, dass die Netzwerkadressen geändert werden. Beispiel: Wechsel eines Laptops an einen Remotestandort. Wenn ein Client die Netzwerkadresse wechselt, verwendet er möglicherweise einen Verwaltungspunkt am lokalen Standort, bevor er versucht, einen Server am zugewiesenen Standort zu verwenden. Die Liste der Server des ihm zugewiesenen Standorts enthält die bevorzugten Verwaltungspunkte. Weitere Informationen finden Sie unter [Understand how clients find site resources and services (Verstehen, wie Clients Standortressourcen und -dienste suchen)](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Überlappende Grenzen  

Bei der Abfrage von Inhaltsorten werden überlappende Grenzkonfigurationen von Configuration Manager unterstützt. Wenn der Netzwerkstandort des Clients zu mehr als einer Begrenzungsgruppe gehört:

- Wenn ein Client Inhalte anfordert, sendet Configuration Manager dem Client eine Liste mit sämtlichen Verteilungspunkten, die über diese Inhalte verfügen.  

- Wenn von einem Client Zustandsmigrationsinformationen bei einem Server angefordert bzw. an diesen gesendet werden, sendet Configuration Manager dem Client eine Liste mit sämtlichen Zustandsmigrationspunkten, die mit einer Begrenzungsgruppe mit der aktuellen Netzwerkadresse des Clients verknüpft sind.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  

## <a name="example-of-using-boundary-groups"></a>Beispiel für das Verwenden von Begrenzungsgruppen

In folgendem Beispiel wird ein Client verwendet, der in einem Verteilungspunkt nach Inhalt sucht. Dieses Beispiel kann auch auf andere Standortsystemrollen angewendet werden, die Begrenzungsgruppen verwenden.

Erstellen Sie drei Begrenzungsgruppen, die sich keine Grenzen oder Standortsystemserver teilen:  

- Gruppe BG_A mit den Verteilungspunkten DP_A1 und DP_A2  

- Gruppe BG_B mit den Verteilungspunkten DP_B1 und DP_B2  

- Gruppe BG_C mit den Verteilungspunkten DP_C1 und DP_C2  

Fügen Sie die Netzwerkadressen Ihrer Clients nur in der Begrenzungsgruppe BG_A als Grenzen hinzu. Konfigurieren Sie anschließend Beziehungen aus dieser Begrenzungsgruppe für die anderen zwei Begrenzungsgruppen:  

- Konfigurieren Sie Verteilungspunkte für die erste *benachbarte* Gruppe (BG_B), die nach 10 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_B1 und DP_B2. Beide verfügen über eine gute Verbindung mit den Grenzspeicherorten der ersten Gruppe.  

- Konfigurieren Sie die zweite *benachbarte* Gruppe (BG_C), die nach 20 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_C1 und DP_C2. Beide sind über ein WAN von den anderen Begrenzungsgruppen aus zugänglich.  

- Fügen Sie zudem zur standardmäßigen Standortbegrenzungsgruppe der Standorte einen weiteren Verteilungspunkt hinzu, der sich auf dem Standortserver befindet. Dieser Server ist der am wenigsten bevorzugte Quellspeicherort für Inhalt, der jedoch zentral zu allen Ihren Begrenzungsgruppen angesiedelt ist.

    Beispiel für Begrenzungsgruppen und Fallbackzeiten:

    ![Beispiel für Begrenzungsgruppen und Fallbackzeiten](media/BG_Fallback.png)  

Mit dieser Konfiguration:  

- Der Client beginnt in seiner *aktuellen* Begrenzungsgruppe (BG_A) mit der Suche nach Inhalten über Verteilungspunkte. Er durchsucht die einzelnen Verteilungspunkte zwei Minuten lang und wechselt anschließend zum nächsten Verteilungspunkt in der Begrenzungsgruppe. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1 und DP_A2.  

- Wenn der Client 10 Minuten lang keinen Inhalt aus der *aktuellen* Begrenzungsgruppe findet, fügt er die Verteilungspunkte aus der Begrenzungsgruppe BG_B zur Suche hinzu. Anschließend fährt er mit der Suche nach Inhalten über einen Verteilungspunkt in seinem kombinierten Serverpool fort. Dieser Pool enthält nun Server aus den Begrenzungsgruppen BG_A und BG_B. Der Client kontaktiert weiterhin zwei Minuten lang jeden Verteilungspunkt und wechselt anschließend zum nächsten Server in seinem Pool. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1, DP_A2, DP_B1 und DP_B2.  

- Nach weiteren 10 Minuten (insgesamt 20 Minuten), in denen der Client immer noch keinen Verteilungspunkt mit Inhalt gefunden hat, erweitert er seinen Pool durch verfügbare Server aus der zweiten *benachbarten* Gruppe, der Begrenzungsgruppe BG_C. Es gibt nun sechs Verteilungspunkte, die der Client suchen muss: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 und DP_C2. Er wechselt weiterhin alle zwei Minuten zu einem neuen Verteilungspunkt, bis er Inhalt findet.  

- Wenn der Client nach maximal 120 Minuten keinen Inhalt gefunden hat, greift er darauf zurück, die *standardmäßige Standortbegrenzungsgruppe* als Teil der kontinuierlichen Suche einzuschließen. In den Pool werden nun alle Verteilungspunkte aus den drei konfigurierten Begrenzungsgruppen sowie der letzte Verteilungspunkt eingeschlossen, der sich auf dem Standortserver befindet. Der Client setzt die Suche nach Inhalt anschließend fort und wechselt alle zwei Minuten den Verteilungspunkt, bis er Inhalt gefunden hat.  

Sie können steuern, wann bestimmte Verteilungspunkte als Quellspeicherorte für Inhalt hinzugefügt werden, indem Sie die unterschiedlichen benachbarten Gruppen so konfigurieren, dass sie zu unterschiedlichen Zeitpunkten verfügbar sind. Der Client verwendet das Fallback zur standardmäßigen Standortbegrenzungsgruppe als Sicherheitsnetz für Inhalte, die an einem anderen Speicherort nicht verfügbar sind.

## <a name="changes-from-prior-versions"></a>Änderungen gegenüber früheren Versionen

Im Folgenden handelt es sich um wichtige Änderungen an Begrenzungsgruppen und der Vorgehensweise von Clients bei der Suche nach Inhalten in Configuration Manager (Current Branch). Viele dieser Änderungen und Konzepte arbeiten zusammen.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Konfigurationen für „Schnell“ und „Langsam“ entfernt

Sie konfigurieren einzelne Verteilungspunkte nicht mehr so, dass diese schnell oder langsam sind. Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt. Aufgrund dieser Änderung unterstützt die Registerkarte **Referenz** der Begrenzungsgruppeneigenschaften die Konfiguration von „schnell“ und „langsam“ nicht mehr.  

### <a name="new-default-boundary-group-at-each-site"></a>Neue Standardbegrenzungsgruppe an jedem Standort

Jeder primäre Standort verfügt über eine neue Standardbegrenzungsgruppe mit dem Namen **Default-Site-Boundary-Group&lt;Standortcode>** . Wenn sich ein Client nicht an einer Netzwerkadresse befindet, die einer Begrenzungsgruppe zugewiesen wurde, verwendet er die Standortsysteme, die mit der Standardgruppe seines zugewiesenen Standorts verknüpft sind. Planen Sie, diese Begrenzungsgruppe als Ersatz für das Konzept der Fallbackinhaltsquelle zu verwenden.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Fallbackquellpfad für Inhalt zulassen** wurde entfernt

Sie konfigurieren nicht mehr explizit einen Verteilungspunkt, der für das Fallback verwendet wird. Die Optionen zum Konfigurieren dieser Einstellung werden von der Konsole entfernt.

Darüber hinaus hat sich das Ergebnis geändert, das auftritt, wenn die Einstellung **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen** auf einem Bereitstellungstyp für Anwendungen festgelegt wird. Diese Einstellung auf einem Bereitstellungstyp ermöglicht es einem Client nun, die Standard-Standortbegrenzungsgruppe als Quellspeicherort für Inhalt zu verwenden.

#### <a name="boundary-groups-relationships"></a>Beziehungen von Begrenzungsgruppen

Sie können eine Begrenzungsgruppe mit mindestens einer zusätzlichen Begrenzungsgruppe verknüpfen. Diese Verknüpfungen bilden Beziehungen, die auf der neuen Registerkarte der Begrenzungsgruppeneigenschaften mit dem Namen **Beziehungen** konfiguriert werden:  

- Jede Begrenzungsgruppe, der ein Client direkt zugewiesen ist, wird **aktuelle** Begrenzungsgruppe genannt.  

- Jede Begrenzungsgruppe, die ein Client aufgrund einer Zuweisung zwischen der *aktuellen* Begrenzungsgruppe des Clients und einer anderen Gruppe verwenden kann, wird als **benachbarte** Begrenzungsgruppe bezeichnet.  

- Fügen Sie auf der Registerkarte **Beziehungen** Begrenzungsgruppen hinzu, die als *benachbarte* Begrenzungsgruppe verwendet werden sollen. Außerdem sollten Sie eine Zeit in Minuten für das Fallback konfigurieren. Wenn ein Client keine Inhalte von einem Verteilungspunkt in der *aktuellen* Gruppe finden kann, beginnt er dieses Mal damit, Speicherorte für Inhalte von *benachbarten* Begrenzungsgruppen zu durchsuchen.  

    Beim Hinzufügen oder Ändern einer Begrenzungsgruppenkonfiguration können Sie das Fallback zu dieser bestimmte Begrenzungsgruppe von der aktuellen Gruppe blockieren, die Sie konfigurieren.  

Definieren Sie explizite Verknüpfungen (Links) zwischen den Begrenzungsgruppen, um die neue Konfiguration verwenden zu können. Konfigurieren Sie sämtliche Verteilungspunkte in dieser verknüpften Gruppe mit der gleichen Zeit in Minuten. Wenn ein Client keine Inhaltsquelle von seiner *aktuellen* Begrenzungsgruppe finden kann, bestimmt die von Ihnen konfigurierte Zeit, wann der Client damit beginnt, Inhaltsquellen von dieser benachbarten Begrenzungsgruppe zu suchen.

Zusätzlich zu Begrenzungsgruppen, die Sie explizit konfigurieren, verfügt jede Begrenzungsgruppe über einen implizierten Link zur Standard-Standortbegrenzungsgruppe. Dieser Link wird nach 120 Minuten aktiv. Dann wird die standardmäßige Standortbegrenzungsgruppe zu einer benachbarten Begrenzungsgruppe. Durch dieses Verhalten können die Clients die Verteilungspunkte, die mit dieser Begrenzungsgruppe verknüpft sind, als Quellspeicherorte für Inhalt verwenden.

Dieses Verhalten ersetzt, was zuvor als Fallback für den Inhalt bezeichnet wurde. Überschreiben Sie dieses Standardverhalten von 120 Minuten, indem Sie die standardmäßige Begrenzungsgruppe explizit mit einer *aktuellen* Gruppe verknüpfen. Legen Sie eine bestimmte Zeit in Minuten fest oder blockieren Sie das Fallback komplett, um eine Verwendung zu verhindern.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Clients versuchen bis zu zwei Minuten lang, Inhalte aus den einzelnen Verteilungspunkten abzurufen

Wenn ein Client nach einem Quellspeicherort für Inhalt sucht, versucht er zwei Minuten lang auf jeden Verteilungspunkt zuzugreifen, bevor er anschließend einen anderen Verteilungspunkt ausprobiert. Bei diesem Verhalten handelt es sich um eine Änderung gegenüber früheren Versionen, bei denen Clients bis zu zwei Stunden lang versucht haben, eine Verbindung mit einem Verteilungspunkt herzustellen.

- Clients wählen den ersten Verteilungspunkt zufällig aus dem Pool verfügbarer Server in der *aktuellen* Begrenzungsgruppe (bzw. den aktuellen Begrenzungsgruppen) des Clients aus.  

- Wenn der Client den Inhalt nach zwei Minuten nicht gefunden hat, wechselt er zu einem neuen Verteilungspunkt und versucht, Inhalt von diesem Server abzurufen. Dieser Vorgang wird alle zwei Minuten wiederholt, bis der Client den Inhalt findet oder den letzten Server im Pool erreicht.  

- Wenn ein Client in seinem *aktuellen* Pool keinen gültigen Quellspeicherort für Inhalt finden kann, bevor der Zeitraum für ein Fallback auf eine *benachbarte* Begrenzungsgruppe erreicht ist, fügt der Client die Verteilungspunkte aus dieser *benachbarten* Begrenzungsgruppe am Ende seiner aktuellen Liste hinzu. Anschließend durchsucht er die erweiterte Gruppe des Quellpfades, welche die Verteilungspunkte aus beiden Begrenzungsgruppen enthält.  

    > [!TIP]  
    > Wenn Sie einen expliziten Link von der aktuellen Begrenzungsgruppe zu der standardmäßigen Standortbegrenzungsgruppe erstellen und eine Fallbackzeit definieren, die kürzer ist als die Fallbackzeit für einen Link zu einer benachbarten Begrenzungsgruppe, beginnen Clients, Quellpfade aus der standardmäßigen Standortbegrenzungsgruppe zu durchsuchen, bevor sie die benachbarte Gruppe einschließen.  

- Wenn der Client vom letzten Server im Pool keinen Inhalt abrufen kann, beginnt er den Prozess erneut.  

## <a name="see-also"></a>Weitere Informationen:

- [Procedures for boundary groups (Prozeduren für Begrenzungsgruppen)](boundary-group-procedures.md)  

- [Informationen zu Begrenzungen](boundaries.md)  

- [Grundlegende Konzepte für das Content Management](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
