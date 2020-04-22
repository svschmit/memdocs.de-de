---
title: Client-Peercache
titleSuffix: Configuration Manager
description: Verwenden Sie bei der Bereitstellung von Inhalten mit Configuration Manager den Clientpeercache für Quellenspeicherorte.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1b9afc8c9cde94488908e4cd9737a58547326f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703668"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peercache für Konfigurations-Manager-Clients

*Gilt für: Configuration Manager (Current Branch)*

<!--1101436-->
Der Peercache unterstützt Sie dabei, die Bereitstellung von Inhalten für Clients an Remotestandorten zu verwalten. Der Peercache ist eine integrierte Configuration Manager-Lösung, mit deren Hilfe Clients Inhalte für andere Clients direkt aus ihrem lokalen Cache freigeben können.   

> [!Note]  
> In Version 1906 wird dieses Feature standardmäßig von Configuration Manager aktiviert. In Version 1902 oder früher aktiviert Configuration Manager dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Übersicht

Definitionen:  

- **Peercacheclient:** ein Konfigurations-Manager-Client, der Inhalte von einem Peer herunterlädt.  

- **Peercachequelle:** ein Konfigurations-Manager-Client, den Sie für den Peercache aktivieren und über den Inhalte für andere Clients freigegeben werden.  

Wenn Sie Clients als Peercachequellen verwenden möchten, müssen Sie die Clienteinstellungen konfigurieren. Das Verwenden von Peercacheclients ist jedoch nicht obligatorisch. Wenn Sie Clients als Peercachequellen verwenden, werden diese vom Verwaltungspunkt in die Liste der Inhaltsquellenspeicherorte aufgenommen.<!--510397--> Weitere Informationen finden Sie unter [Vorgänge](#operations).  

Eine Peercachequelle muss ein Mitglied der aktuellen Begrenzungsgruppe des Peercacheclients sein. Der Verwaltungspunkt trägt keine Peercachequellen aus einer benachbarten Begrenzungsgruppe in die Liste der Inhaltsquellen ein, die dem Client bereitgestellt wird. Stattdessen werden nur die Verteilungspunkte einer benachbarten Begrenzungsgruppe eingeschlossen. Weitere Informationen zu aktuellen und benachbarten Begrenzungsgruppen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

Der Konfigurations-Manager-Client verwendet den Peercache, um anderen Clients unterschiedliche Inhalte aus dem Cache zur Verfügung zu stellen. Zu diesen Inhalten zählen Office 365-Dateien und Expressinstallationsdateien.<!--SMS.500850-->  

Der Peercache ersetzt nicht andere Lösungen wie Windows BranchCache oder die Übermittlungsoptimierung, sondern kann zusammen mit diesen verwendet werden. Diese Technologien bieten Ihnen mehr Optionen für das Erweitern herkömmlicher Inhaltsbereitstellungslösungen wie z.B. Verteilungspunkte. Der Peercache ist eine individuelle Lösung, die nicht von BranchCache abhängig ist. Sie können den Peercache kann auch dann verwenden, wenn Sie BranchCache nicht aktivieren oder nutzen.  

> [!Note]  
> Ab Version 1802 ist Windows BranchCache für Bereitstellungen immer aktiviert. Die Einstellung **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen** ist nicht mehr vorhanden.<!--SCCMDocs issue 539--> Sofern vom Verteilungspunkt unterstützt und in den Clienteinstellungen aktiviert, verwenden Clients BranchCache. Weitere Informationen finden Sie unter [Konfigurieren von BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Vorgänge

Stellen Sie die [Clienteinstellungen](#bkmk_settings) für eine Sammlung bereit, um den Peercache zu aktivieren. Mitglieder dieser Sammlung werden dann als Peercachequelle für andere Clients in derselben Begrenzungsgruppe verwendet.  

- Ein Client, der als Peerinhaltsquelle fungiert, übermittelt eine Liste der verfügbaren zwischengespeicherten Inhalte mithilfe von Zustandsmeldungen an seinen Verwaltungspunkt.

   > [!NOTE]
   > Eine Liste der verfügbaren Zustandsmeldungen für Peerinhaltsquellen, insbesondere der Meldungen mit den IDs 7200, 7201, 7202 und 7203, finden Sie unter [Zustandsmeldungen in Configuration Manager](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map).

- Ein anderer Client in derselben Begrenzungsgruppe sendet eine Inhaltsortsanforderung an den Verwaltungspunkt. Der Server gibt die Liste der möglichen Inhaltsquellen zurück. Diese enthält alle Peercachequellen, die online sind und über die angeforderten Inhalte verfügen. Die Liste enthält auch die Verteilungspunkte und andere Quellspeicherorte für Inhalte in dieser Begrenzungsgruppe. Weitere Informationen finden Sie unter [Content source priority (Priorität von Inhaltsquellen)](fundamental-concepts-for-content-management.md#content-source-priority).  

- Der Client, der nach den Inhalten sucht, wählt wie gewohnt eine Quelle aus der angegebenen Liste aus. Dann versucht der Client den Inhalt abzurufen.  

Ab Version 1806 bieten Begrenzungsgruppen zusätzliche Einstellungen, die Ihnen mehr Kontrolle über die Verteilung von Inhalten in Ihrer Umgebung einräumen. Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Wenn ein Client einen Fallback auf eine benachbarte Begrenzungsgruppe für Inhalte ausführt, fügt der Verwaltungspunkt die Peercachequellen aus der benachbarten Begrenzungsgruppe nicht der Liste der möglichen Quellspeicherorte für Inhalte hinzu.  

Wählen Sie nur Clients aus, die als Peercachequellen geeignet sind. Bewerten Sie die Eignung der Clients nach Attributen wie Chassistyp, Speicherplatz und Netzwerkkonnektivität. Weitere Informationen zum Auswählen geeigneter Clients für den Peercache finden Sie in [diesem Blog eines Microsoft-Beraters](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801).


### <a name="limited-access-to-a-peer-cache-source"></a>Eingeschränkter Zugriff auf eine Peercachequelle  

Eine Peercachequelle lehnt Anforderungen für Inhalte ab, wenn bei der Inhaltsanforderung eines Peers eine der folgenden Bedingungen erfüllt ist:  

- Niedriger Akkustand.  

- Prozessorauslastung überschreitet 80 %.  

- *AvgDiskQueueLength* der Datenträger-E/A überschreitet den Wert 10.  

- Es bestehen keine weiteren Verbindungen mit dem Computer.  

> [!Tip]  
> Konfigurieren Sie diese Einstellungen mithilfe der WMI-Klasse des Clientkonfigurationsservers für die Peerquellfunktion (*SMS_WinPEPeerCacheConfig*) im Configuration Manager SDK.  

Wenn die Peercachequelle eine Inhaltsanforderung ablehnt, sucht der Peercacheclient weiterhin nach Inhalten in seiner Liste mit den Quellspeicherorten für Inhalte.   



## <a name="requirements"></a>Anforderungen

- Der Peercache unterstützt alle unter [Unterstützte Betriebssysteme für Clients und Geräte](../configs/supported-operating-systems-for-clients-and-devices.md) aufgeführten Windows-Versionen. Andere Betriebssysteme als Windows werden nicht als Peercachequellen oder -clients unterstützt.  

- Bei einer Peercachequelle muss es sich um einen Konfigurations-Manager-Client handeln, der einer Domäne angehört. Ein Client, der nicht in eine Domäne eingebunden ist, kann jedoch Inhalte von einer Peercachequelle abrufen, die nicht der Domäne angehört.  

- Clients können nur Inhalte aus Peercachequellen herunterladen, die sich in ihrer aktuellen Begrenzungsgruppe befinden.  

- Ein [Netzwerkzugriffskonto](accounts.md#network-access-account) ist nur in folgenden Ausnahmefällen erforderlich:  

  - Ein Peercache-fähiger Client führt über das Softwarecenter eine Tasksequenz aus, die als Startimage neu startet. In diesem Fall müssen Sie ein Netzwerkzugriffskonto am Standort konfigurieren. Wenn das Gerät unter Windows PE ausgeführt wird, verwendet es das Netzwerkzugriffskonto, um Inhalte aus der Peercachequelle abzurufen.  

  - Die Peercachequelle verwendet bei Bedarf das Netzwerkzugriffskonto, um Downloadanforderungen von Peers zu authentifizieren. Dieses Konto benötigt zu diesem Zweck nur Domänenbenutzerberechtigungen.  

- Bei Version 1802 und älteren Versionen wird die aktuelle Grenze einer Peercachequelle durch die letzte Frequenzermittlungsübertragung des Clients festgelegt. Ein Client, der zu einer anderen Begrenzungsgruppe wandert, ist als Peercache möglicherweise weiterhin ein Mitglied der früheren Begrenzungsgruppe. Durch dieses Verhalten wird einem Client eine Peercachequelle bereitgestellt, die sich nicht am angrenzenden Netzwerkstandort befindet. Legen Sie Roamingclients nicht als Peercachequellen fest.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > Ab Version 1806 bestimmt Configuration Manager effizienter, ob eine Peercachequelle per Roaming zu einem anderen Speicherort gewechselt hat. Durch dieses Verhalten wird sichergestellt, dass diese vom Verwaltungspunkt am neuen statt am alten Speicherort als Inhaltsquelle für Clients bereitgestellt wird. Wenn Sie die Peercachefunktion mit Roaming von Peercachequellen verwenden, führen Sie nach dem Update des Standorts auf Version 1806 auch Updates auf die neueste Clientversion für alle Peercachequellen durch. Der Verwaltungspunkt führt diese Peercachequellen erst in der Liste der Speicherorte für Inhalte auf, wenn sie mindestens auf Version 1806 aktualisiert wurden.<!--SCCMDocs issue 850-->  

- Der Verwaltungspunkt überprüft vor dem Herunterladen von Inhalten zunächst, ob die Peercachequelle online ist.<!--sms.498675--> Diese Überprüfung erfolgt über den „Schnellkanal“ für die Clientbenachrichtigung, der TCP-Port 10123 verwendet.<!--511673-->  

> [!Note]  
> Wenn Sie neue Configuration Manager-Features nutzen möchten, müssen Sie zunächst die Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a> Peercache-Clienteinstellungen

Weitere Informationen zu Peercache-Clienteinstellungen finden Sie unter [Einstellungen des Clientcaches](../../clients/deploy/about-client-settings.md#client-cache-settings). 

Weitere Informationen zum Konfigurieren dieser Einstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../../clients/deploy/configure-client-settings.md).

Auf Peercache-fähigen Clients, die die Windows-Firewall verwenden, konfiguriert Configuration Manager die Firewallports, die Sie in den Clienteinstellungen festlegen.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a> Unterstützung von unvollständigen Downloads
<!--1357346-->
Ab Version 1806 können Clientpeercache-Quellen Inhalte aufteilen. Diese Teile minimieren die Netzwerkdatenübertragung, um die WAN-Auslastung zu reduzieren. Der Verwaltungspunkt erlaubt eine genauere Nachverfolgung der Inhaltsteile. Er versucht, mehrere Downloads desselben Inhalts pro Begrenzungsgruppe zu vermeiden. 


### <a name="example-scenario"></a>Beispielszenario

Contoso hat einen einzigen primären Standort mit zwei Begrenzungsgruppen: Hauptsitz (HQ) und Filiale. Zwischen den Begrenzungsgruppen besteht eine Fallbackbeziehung mit einer Fallbackzeit von 30 Minuten. Der Verwaltungs- und Verteilungspunkt für den Standort befindet sich nur innerhalb der HQ-Grenze. Der Filialstandort hat keinen lokalen Verteilungspunkt. Zwei der vier Clients in der Filiale sind als Peercachequellen konfiguriert. 

![Diagramm der Netzwerkkonfiguration für das beschriebene Beispielszenario](media/1357346-peer-cache-source-parts.png)

1. Sie beabsichtigen eine Bereitstellung mit Inhalt für alle vier Clients in der Filiale. Sie haben den Inhalt nur an den Verteilungspunkt verteilt.  

2. Client3 und Client4 verfügen über keine lokale Quelle für die Bereitstellung. Der Verwaltungspunkt weist die Clients an, bis zu einem Fallback auf die Remotebegrenzungsgruppe 30 Minuten zu warten.  

3. Client1 (PCS1) ist die erste Peercachequelle, die die Richtlinie mit dem Verwaltungspunkt aktualisiert. Da dieser Client als Peercachequelle aktiviert ist, weist der Verwaltungspunkt ihn an, unverzüglich mit dem Herunterladen von Teil A vom Verteilungspunkt zu beginnen.  

4. Wenn Client2 (PCS2) den Verwaltungspunkt kontaktiert, während Teil A bereits heruntergeladen wird, aber noch nicht abgeschlossen ist, weist der Verwaltungspunkt ihn an, unverzüglich mit dem Herunterladen von Teil B vom Verteilungspunkt zu beginnen.  

5. PCS1 beendet das Herunterladen von Teil A und benachrichtigt unverzüglich den Verwaltungspunkt. Da Teil B bereits heruntergeladen wird, aber noch nicht abgeschlossen ist, weist der Verwaltungspunkt ihn an, unverzüglich mit dem Herunterladen von Teil C vom Verteilungspunkt zu beginnen.  

6. PCS2 beendet das Herunterladen von Teil B und benachrichtigt unverzüglich den Verwaltungspunkt. Der Verwaltungspunkt weist ihn an, mit dem Herunterladen von Teil D vom Verteilungspunkt zu beginnen.  

7. PCS1 beendet das Herunterladen von Teil C und benachrichtigt unverzüglich den Verwaltungspunkt. Der Verwaltungspunkt teilt mit, dass keine weiteren Teile vom Remoteverteilungspunkt verfügbar sind. Der Verwaltungspunkt weist ihn an, Teil B von seinem lokalen Peer, PCS2, herunterzuladen.  

8. Dieser Prozess wird so lange fortgesetzt, bis beide Client-Peercachequellen gegenseitig alle Teile heruntergeladen haben. Der Verwaltungspunkt priorisiert Teile vom Remoteverteilungspunkt, bevor er die Peercachequellen anweist, Teile von lokalen Peers herunterzuladen.  

9. Client3 ist der erste Client, der die Richtlinie aktualisiert, nachdem die Fallbackzeit von 30 Minuten abgelaufen ist. Er meldet sich erneut beim Verwaltungspunkt, der den Client über neue lokale Quellen informiert. Anstatt den Inhalt vollständig vom Verteilungspunkt über das WAN herunterzuladen, lädt er den Inhalt vollständig von einer der Client-Peercachequellen herunter. Clients priorisieren lokale Peerquellen. 

> [!Note]  
> Wenn die Anzahl der Client-Peercachequellen größer ist als die Anzahl der Inhaltsteile, weist der Verwaltungspunkt die weiteren Peercachequellen an, wie ein normaler Client auf einen Fallback zu warten. 


### <a name="configure-partial-download"></a>Konfigurieren von unvollständigen Downloads

1. Richten Sie wie gewohnt [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md) und Peercachequellen ein.  

2. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Klicken Sie im Menüband auf **Hierarchieeinstellungen**.  

3. Aktivieren Sie auf der Registerkarte **Allgemein** die Option **Configure client peer cache sources to divide content into parts** (Client-Peercachequellen so konfigurieren, dass Inhalt in Teile untergliedert wird).  

4. Erstellen Sie eine erforderliche Bereitstellung mit Inhalt.  

   > [!Note]  
   > Diese Funktion ist nur verfügbar, wenn der Client Inhalt im Hintergrund herunterlädt, wie bei einer erforderlichen Bereitstellung. Bedarfsgesteuerte Downloads, z.B. wenn der Benutzer eine verfügbare Bereitstellung im Softwarecenter installiert, verhalten sich wie gewohnt.  

Um zu sehen, wie das Herunterladen von Inhalten in Teilen abgewickelt wird, prüfen Sie das Protokoll **ContentTransferManager.log** auf der Client-Peercachequelle und das Protokoll **MP_Location.log** auf dem Verwaltungspunkt.  



## <a name="guidance-for-cache-management"></a>Anleitung zur Cacheverwaltung
<!--510645-->
Der Peercache ist zur Freigabe von Inhalten auf den Configuration Manager-Client angewiesen. Bei der Verwaltung des Clientcaches in Ihrer Umgebung sollten Sie die folgenden Punkte berücksichtigen:  

- Der Konfigurations-Manager-Clientcache ist nicht mit der Inhaltsbibliothek auf einem Verteilungspunkt vergleichbar. Inhalte, die an den Verteilungspunkt verteilt werden, werden von Ihnen verwaltet, während Inhalte im Cache des Konfigurations-Manager-Clients automatisch verwaltet werden. Mithilfe bestimmter Einstellungen und Methoden können Sie steuern, welche Inhalte im Cache einer Peercachequelle gespeichert werden. Weitere Informationen finden Sie unter [Konfigurieren des Clientcaches für Konfigurations-Manager-Clients](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- Für Peercachequellen können die übliche Cachegröße und die regulären Wartungsmethoden eingesetzt werden. Weitere Informationen hierzu finden Sie unter [Konfigurieren der Clientcachegröße](../../clients/deploy/about-client-settings.md#configure-client-cache-size). Beachtung verdienen größere Inhalte wie Updatepakete für Betriebssysteme oder Windows 10-Expressupdatedateien. Bei derartigen Inhalten sollten Sie den verfügbaren Speicherplatz auf den Peercachequellen berücksichtigen.  

- Der Client der Peercachequelle aktualisiert den letzten Zeitpunkt, zu dem auf Inhalte im Cache verwiesen wurde, sobald ein Peer die Inhalte herunterlädt. Der Client verwendet diesen Zeitstempel bei der automatischen Verwaltung seines Caches und entfernt ältere Inhalte zuerst. Inhalte, die häufig von den Peercacheclients heruntergeladen werden, sollten daher (wenn überhaupt) erst nach einer bestimmten Zeit vom Client entfernt werden.  

- Verwenden ggf. während einer Tasksequenz zur Betriebssystembereitstellung die Variable **SMSTSPreserveContent**, um Inhalte im Clientcache beizubehalten. Weitere Informationen finden Sie unter [Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent).  

- Verwenden Sie beim Erstellen der folgenden Software ggf. die Option **Inhalt dauerhaft im Clientcache speichern**:  
  - Applications
  - Pakete
  - Betriebssystemimages
  - Betriebssystemupgradepakete
  - Startabbilder



## <a name="monitoring"></a>Überwachung   

Wenn Sie das Dashboard **Clientdatenquellen** aufrufen, können Sie besser nachvollziehen, wie der Peercache verwendet wird. Weitere Informationen finden Sie unter [Dashboard „Clientdatenquellen“](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

Des Weiteren können Sie sich auch Berichte ansehen, um mehr über die Nutzung des Peercaches zu erfahren. Wechseln Sie in der Konsole zum Arbeitsbereich **Überwachung**, erweitern Sie **Berichterstellung**, und klicken Sie auf den Knoten **Berichte**. Die folgenden Berichte sind der Kategorie **Softwareverteilung – Inhalt**  zugeordnet:  

1.  **Ablehnen von Inhalt einer Peercachequelle**: Gibt an, wie häufig die Peercachequellen in einer Begrenzungsgruppe die Inhaltsanforderungen ablehnen.  

    > [!Note]  
    > **Bekanntes Problem**<!--486652-->: Wenn Sie einen Drilldown für Ergebnisse wie *MaxCPULoad* und *MaxDiskIO* durchführen, wird möglicherweise ein Fehler angezeigt, der darauf hinweist, dass der Bericht oder Angaben nicht gefunden werden können. Verwenden Sie die anderen beiden Berichte, die die Ergebnisse direkt anzeigen, um dieses Problem zu umgehen.  

2. **Ablehnen von Inhalt einer Peercachequelle durch eine Bedingung**: So können Sie Angaben zur Ablehnung einer angegebenen Begrenzungsgruppe oder eines Ablehnungstyps interpretieren. 

    > [!Note]  
    > **Bekanntes Problem**<!--486652-->: Sie können verfügbare Parameter nicht auswählen, sondern müssen diese manuell eingeben. Geben Sie für *Name der Begrenzungsgruppe* und *Rejection Type* (Ablehnungstyp) die Werte aus dem Bericht **Inhaltsablehnung durch Peercachequelle** ein. Sie können z.B. für *Rejection Type* (Ablehnungstyp) *MaxCPULoad* oder *MaxDiskIO* eingeben.  

3. **Angaben zur Ablehnung von Inhalt einer Peercachequelle**: Der Inhalt, den der Client anfordert hat, als die Anforderung abgelehnt wurde.  

    > [!Note]  
    > **Bekanntes Problem**<!--486652-->: Sie können verfügbare Parameter nicht auswählen, sondern müssen diese manuell eingeben. Geben Sie den Wert für *Rejection Type* (Ablehnungstyp) ein, wie im Bericht **Ablehnen von Inhalt einer Peercachequelle** gezeigt wird. Geben Sie dann die *Ressourcen-ID* für die Inhaltsquelle ein, über die Sie mehr Informationen sehen möchten. 
    > 
    > So finden Sie die Resource ID der Quelle des Inhalts heraus:  
    > 
    > 1. Machen Sie den Namen des Computers ausfindig, der als *Peercachequelle* in den Ergebnissen des Berichts **Ablehnen von Inhalt einer Peercachequelle durch eine Bedingung** angezeigt wird.  
    > 
    > 2. Wechseln Sie zum Arbeitsbereich **Assets und Konformität**, klicken Sie auf den Knoten **Geräte**, und suchen Sie nach dem Computernamen. Verwenden Sie den Wert aus der Spalte „Resource ID“.  

