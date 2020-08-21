---
title: Planen von Softwareupdates
titleSuffix: Configuration Manager
description: Ein Plan für die Softwareupdatepunkt-Infrastruktur ist wichtig, bevor Sie Softwareupdates in einer Configuration Manager-Produktionsumgebung verwenden.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: b7b3ef78924389232ea292d16c6840fbef9bb321
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123590"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Planen von Softwareupdates in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie Softwareupdates in einer Configuration Manager-Produktionsumgebung verwenden, ist es wichtig, den Planungsprozess durchzugehen. Einen guter Plan für die Softwareupdatepunkt-Infrastruktur ist wichtig für eine erfolgreiche Softwareupdateimplementierung. Informationen zur Kapazitätsplanung für Softwareupdates finden Sie unter [Größe und Skalierung von Zahlen](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point).


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> Bestimmen der Softwareupdatepunkt-Infrastruktur  

Dieser Abschnitt enthält die folgenden Unterthemen:    
- [Softwareupdatepunkt-Liste](#BKMK_SUPList)
- [Wechseln des Softwareupdatepunkts](#BKMK_SUPSwitching)
- [Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt](#BKMK_ManuallySwitchSUPs)
- [Softwareupdatepunkte in einer nicht vertrauenswürdigen Gesamtstruktur](#BKMK_SUP_CrossForest)
- [Verwenden eines vorhandenen WSUS-Servers als Synchronisierungsquelle am Standort der obersten Ebene](#BKMK_WSUSSyncSource)
- [Softwareupdatepunkt an sekundärem Standort](#BKMK_SUPSecSite)  
- [Planen internetbasierter Clients](#bkmk_internet-clients)  
- [Planen von Softwareupdateinhalten](#bkmk_content)  
- [Planen der Updates von Drittanbietern](#bkmk_thirdparty)  


Der Standort der zentralen Verwaltung und alle untergeordneten primären Standorte müssen über einen Softwareupdatepunkt verfügen. Bestimmen Sie beim Planen der Infrastruktur von Softwareupdatepunkten die folgenden Abhängigkeiten:
- Wo der Softwareupdatepunkt des Standorts installiert werden soll  
- Welche Standorte einen Softwareupdatepunkt erfordern, der Kommunikation von internetbasierten Clients akzeptiert
- Ob Sie einen Softwareupdatepunkt an sekundären Standorten benötigen  

> [!IMPORTANT]  
>  Weitere Informationen zu den internen und externen Abhängigkeiten, die für Softwareupdates erforderlich sind, finden Sie unter [Voraussetzungen für Softwareupdates](prerequisites-for-software-updates.md).  

Fügen Sie mehrere Softwareupdatepunkte zu einem primären Standort von Configuration Manager hinzu, um die Fehlertoleranz zu verbessern. Das Failoverdesign des Softwareupdatepunkts unterscheidet sich von dem auf einer rein zufälligen Anordnung beruhenden Modell, das die Designgrundlage für Verwaltungspunkte bildet. Anders als beim Design von Verwaltungspunkten ist bei Softwareupdatepunkten der Wechsel zu einem neuen Softwareupdatepunkt mit Client- und Netzwerkleistungskosten verbunden. Durch den Wechsel des Clients zu einem neuen WSUS-Server zwecks Überprüfung auf Softwareupdates werden die Kataloggröße, die zugehörigen clientseitigen Anforderungen sowie die Anforderungen an die Netzwerkleistung gesteigert. Aus diesem Grund wird vom Client die Affinität mit dem letzten Softwareupdatepunkt aufrechterhalten, bei dem die Überprüfung erfolgreich war.  

Der erste Softwareupdatepunkt, den Sie an einem primären Standort installieren, dient als Synchronisierungsquelle für alle weiteren Softwareupdatepunkte, die Sie dem primären Standort hinzufügen. Nachdem Sie Softwareupdatepunkte hinzugefügt und die Synchronisierung gestartet haben, können Sie den Status der Softwareupdatepunkte und der Synchronisierungsquelle im Knoten **Synchronisierungsstatus der Softwareupdatepunkte** des Arbeitsbereichs **Überwachung** anzeigen.  

Wenn es zu einem Fehler des Softwareupdatepunkts kommt, der als Synchronisierungsquelle für den Standort konfiguriert ist, entfernen Sie manuell die fehlgeschlagene Rolle. Wählen Sie dann einen neuen Softwareupdatepunkt als zu verwendende Synchronisierungsquelle aus. Weitere Informationen finden Sie unter [Entfernen einer Standortsystemrolle](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role).  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Softwareupdatepunkt-Liste  

Configuration Manager stellt in folgenden Situationen eine Softwareupdatepunktliste für den Client bereit:  

- Ein neuer Client erhält die Richtlinie zur Aktivierung von Softwareupdates  

- Ein Client kann keine Verbindung zu dem ihm zugewiesenen Softwareupdatepunkt herstellen und muss zu einem anderen Punkt wechseln  

Der Client wählt nach dem Zufallsprinzip einen Softwareupdatepunkt aus der Liste aus. Er priorisiert die Softwareupdatepunkte in derselben Gesamtstruktur. Configuration Manager stellt Clients je nach Clienttyp eine unterschiedliche Liste zur Verfügung:  

-   **Intranetbasierte Clients:** Diese Clients erhalten eine Liste mit Softwareupdatepunkten, die Sie so konfigurieren können, dass nur Verbindungen mit dem Intranet zulässig sind, bzw. eine Liste mit Softwareupdatepunkten, bei denen Clientverbindungen mit dem Internet und dem Intranet möglich sind.  

-   **Internetbasierte Clients:** Diese Clients erhalten eine Liste mit Softwareupdatepunkten, die Sie so konfigurieren können, dass nur Verbindungen mit dem Internet zulässig sind, bzw. eine Liste mit Softwareupdatepunkten, bei denen Clientverbindungen mit dem Internet und dem Intranet möglich sind.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Wechseln des Softwareupdatepunkts  

> [!NOTE]  
> Clients verwenden Begrenzungsgruppen zur Auswahl neuer Softwareupdatepunkte. Wenn nicht mehr auf ihren aktuellen Softwareupdatepunkt zugegriffen werden kann, nutzen sie auch Begrenzungsgruppen für das Fallback und das Suchen eines neuen Softwareupdatepunkts. Fügen Sie individuelle Softwareupdatepunkte zu verschiedenen Begrenzungsgruppen hinzu, um zu steuern, welche Server ein Client finden kann. Weitere Informationen finden Sie unter [Softwareupdatepunkte](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

Wenn es an einem Standort mehrere Softwareupdatepunkte gibt und einer davon fehlerhaft oder nicht mehr verfügbar ist, wird von Clients eine Verbindung zu einem anderen Softwareupdatepunkt hergestellt. Die Clients suchen weiterhin mit diesem neuen Server nach den aktuellsten Softwareupdates. Die ursprüngliche Zuweisung eines Clients zu einem Softwareupdatepunkt bleibt so lange bestehen, bis bei der Überprüfung auf Softwareupdates ein Fehler auftritt.  

Bei der Überprüfung auf Softwareupdates kann eine Reihe unterschiedlicher Wiederholungs- bzw. Nichtwiederholungsfehlercodes ausgegeben werden. Bei einem Überprüfungsfehler mit einem Wiederholungsfehlercode wird vom Client ein Wiederholungsprozess zur Überprüfung des Softwareupdatepunkts auf Softwareupdates gestartet. Ein Wiederholungsfehlercode ist in der Regel darauf zurückzuführen, dass der WSUS-Server nicht verfügbar oder vorübergehend überlastet ist. Wenn bei der Überprüfung auf Softwareupdates ein Fehler auf dem Client auftritt, werden folgende Vorgänge ausgeführt:  

1.  Der Client sucht nach Softwareupdates:  
    - Zum nächsten für ihn geplanten Zeitpunkt
    - Wenn die Suche manuell in der Systemsteuerung auf dem Client ausgeführt wird
    - Wenn die Suche manuell über die Configuration Manager-Konsole über eine Clientbenachrichtigungsaktion ausgeführt wird
    - Wenn die Suche von einer Configuration Manager SDK-Methode ausgeführt wird  

2.  Wenn die Überprüfung fehlschlägt, wartet der Client 30 Minuten, bevor er die Überprüfung wiederholt. Er verwendet dazu denselben Softwareupdatepunkt.  

3.  Vom Client werden mindestens vier Wiederholungsversuche in Abständen von 30 Minuten ausgeführt. Nach dem vierten Fehlschlagen und einer weiteren Wartezeit von 2 Minuten wechselt der Client zum nächsten Softwareupdatepunkt in seiner Liste.  

4.  Der Client wiederholt diesen Prozess mit dem neuen Softwareupdatepunkt. Nach einer erfolgreichen Überprüfung stellt der Client fortan eine Verbindung mit dem neuen Softwareupdatepunkt her.  

Die folgende Liste enthält zusätzliche Informationen, die Sie bei Wiederholungsversuchen und beim Wechseln von Softwareupdatepunkten in Betracht ziehen müssen:  

-   Wenn ein Client vom Intranet getrennt ist und bei der Überprüfung auf Softwareupdates ein Fehler auftritt, findet kein Wechsel zu einem anderen Softwareupdatepunkt statt. Dies ist ein erwarteter Fehler, da der Client das interne Netzwerk bzw. einen Softwareupdatepunkt, der Verbindungen aus dem Intranet zulässt, nicht erreichen kann. Der Configuration Manager-Client bestimmt die Verfügbarkeit des Softwareupdatepunkts im Intranet.  

-   Wenn Sie Clients im Internet verwalten und mehrere Softwareupdatepunkte so konfiguriert haben, dass sie eine Kommunikation von Clients im Internet akzeptieren, erfolgt der Wechsel nach dem oben beschriebenen Standardwiederholungsprozess.  

-   Wenn der Überprüfungsprozess startet, der Client aber vor dessen Abschluss heruntergefahren wird, gilt dies weder als Überprüfungsfehler noch als eine der vier Wiederholungen.  

Wenn Configuration Manager einen der folgenden Fehlercodes des Windows Update-Agents erhält, wiederholt der Client den Verbindungsaufbau:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Um die Bedeutung eines Fehlercodes nachzuschlagen, wandeln Sie den dezimalen Fehlercode in einen Hexadezimalwert um und suchen diesen dann auf einer Website, beispielsweise in der [Wiki zu den Fehlercodes des Windows Update-Agents](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx). Der dezimale Fehlercode 2149842970 entspricht beispielsweise dem hexadezimalen Wert 8024001A, der bedeutet, dass der Richtlinienwert WU_E_POLICY_NOT_SET A nicht festgelegt wurde.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a> Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt

Führen Sie für Konfigurations-Manager-Clients einen Wechsel zu einem neuen Softwareupdatepunkt durch, wenn beim aktiven Softwareupdatepunkt Probleme auftreten. Zu diesem Wechsel kommt es nur, wenn ein Client mehrere Softwareupdatepunkte von einem Verwaltungspunkt erhält.

> [!IMPORTANT]    
> Wenn Sie die Geräte wechseln, um einen neuen Server zu verwenden, verwenden die Geräte einen Fallback, um den neuen Server zu finden. Clients wechseln während des Prüfzyklus des nächsten Softwareupdates zum neuen Softwareupdatepunkt.<!-- SCCMDocs#1537 -->
>
> Deshalb sollten Sie vor diesem Wechsel die Konfigurationen Ihrer Begrenzungsgruppen überprüfen, um sicherzustellen, dass sich Ihre Softwareupdatepunkte in den korrekten Begrenzungsgruppen befinden. Weitere Informationen finden Sie unter [Softwareupdatepunkte](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  
>
> Der Wechsel zu einem neuen Softwareupdatepunkt generiert zusätzlichen Netzwerkdatenverkehr. Die Menge des Datenverkehrs hängt von Ihren WSUS-Konfigurationseinstellungen ab, beispielsweise den synchronisierten Klassifizierungen und Produkten oder der Verwendung einer freigegebenen WSUS-Datenbank. Wenn Sie den Wechsel für mehrere Geräte durchführen möchten, sollten Sie diesen in ein Wartungsfenster legen. Diese Vorgehensweise reduziert die Auswirkungen auf Ihr Netzwerk, wenn Clients Überprüfungen mit dem neuen Softwareupdatepunkt durchführen.  

#### <a name="process-to-switch-software-update-points"></a>Wechseln von Softwareupdatepunkten  
Starten Sie diesen Wechsel für eine Gerätesammlung. Nach der Aktivierung suchen die Clients bei der nächsten Überprüfung nach anderen Softwareupdatepunkten.  

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus.  

2.  Wählen Sie die Zielsammlung aus. Klicken Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Sammlung** auf **Clientbenachrichtigung**und anschließend auf **Zum nächsten Softwareupdatepunkt wechseln**.  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Softwareupdatepunkte in einer nicht vertrauenswürdigen Gesamtstruktur  

Erstellen Sie an einem Standort mindestens einen Softwareupdatepunkt zur Unterstützung von Clients in einer nicht vertrauenswürdigen Gesamtstruktur. Zum Hinzufügen eines Softwareupdatepunkts zu einer anderen Gesamtstruktur müssen Sie in dieser Gesamtstruktur zuerst einen WSUS-Server installieren und konfigurieren. Starten Sie dann den Assistenten, um einen Configuration Manager-Standortserver mit der Standortsystemrolle des Softwareupdatepunkts hinzuzufügen. Konfigurieren Sie im Assistenten die folgenden Einstellungen, damit eine Verbindung mit dem WSUS-Server in der nicht vertrauenswürdigen Gesamtstruktur hergestellt werden kann:  

-   Geben Sie ein **Standortsystem-Installationskonto** mit Zugriff auf den WSUS-Server in der nicht vertrauenswürdigen Gesamtstruktur an.  

-   Geben Sie ein **Verbindungskonto für WSUS-Server** für die Verbindung zum WSUS-Server an.  

Angenommen, Sie verfügen in Gesamtstruktur A über einen primären Standort mit zwei Softwareupdatepunkten (SUP01 und SUP02). Für denselben primären Standort verfügen Sie ferner über zwei Softwareupdatepunkte (SUP03 und SUP04) in Gesamtstruktur B. Beim Wechsel zum nächsten Softwareupdatepunkt priorisieren die Clients die Server, die sich in der gleichen Gesamtstruktur befinden.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> Verwenden eines vorhandenen WSUS-Servers als Synchronisierungsquelle am Standort der obersten Ebene  

Der Standort der obersten Ebene in einer Hierarchie ist in der Regel für die Synchronisierung der Metadaten für Softwareupdates mit Microsoft Update konfiguriert. Wenn die Sicherheitsrichtlinie Ihrer Organisation keinen Zugriff vom Standort der obersten Ebene auf das Internet zulässt, müssen Sie die Synchronisierungsquelle für den Standort der obersten Ebene so konfigurieren, dass sie einen vorhandenen WSUS-Server verwendet. Dieser WSUS-Server befindet sich nicht in Ihrer Configuration Manager-Hierarchie. Sie verfügen beispielsweise über einen WSUS-Server in einem mit dem Internet verbundenen Netzwerk (Umkreisnetzwerk), aber Ihr Standort der obersten Ebene befindet sich in einem internen Netzwerk ohne Internetzugang. Konfigurieren Sie den WSUS-Server in dem Umkreisnetzwerk als Synchronisierungsquelle für die Metadaten für Softwareupdates. Konfigurieren Sie den WSUS-Server in dem Umkreisnetzwerk so, dass Softwareupdates anhand derselben Kriterien synchronisiert werden, die Sie in Configuration Manager benötigen. Andernfalls werden vom Standort der obersten Ebene nicht die von Ihnen erwarteten Softwareupdates synchronisiert. Konfigurieren Sie bei der Installation des Softwareupdatepunkts ein WSUS-Serververbindungskonto. Dieses Konto benötigt Zugriff auf den WSUS-Server im Umkreisnetzwerk. Vergewissern Sie sich auch, dass die Firewall Datenverkehr für die entsprechenden Ports zulässt. Weitere Informationen finden Sie im Abschnitt über [Ports, die vom Softwareupdatepunkt als Synchronisierungsquelle genutzt werden](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Softwareupdatepunkt an sekundärem Standort  

An sekundären Standorten ist der Softwareupdatepunkt optional. Installieren Sie an einem sekundären Standort nur einen Softwareupdatepunkt. Wenn am sekundären Standort kein Softwareupdatepunkt installiert ist, verwenden Geräte innerhalb der Grenzen eines sekundären Standorts einen Softwareupdatepunkt an dem ihnen zugewiesenen primären Standort. In der Regel installieren Sie einen Softwareupdatepunkt an einem sekundären Standort, wenn die Netzwerkbandbreite zwischen den Geräten am sekundären Standort und den Softwareupdatepunkten am übergeordneten primären Standort begrenzt ist. Sie können diese Konfiguration auch verwenden, wenn die Kapazitätsgrenze des Softwareupdatepunkts am primären Standort fast erreicht ist. Nach der erfolgreichen Installation und Konfiguration eines Softwareupdatepunkts am sekundären Standort wird auf den Clients ein Update für eine standortweite Richtlinie durchgeführt. Danach wird der neue Softwareupdatepunkt von den Clients verwendet.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a> Planen internetbasierter Clients

Wenn Sie Geräte verwalten müssen, die aus Ihrem Netzwerk ins Internet wechseln, entwickeln Sie einen Plan zur Verwaltung von Softwareupdates auf diesen Geräten. Configuration Manager unterstützt mehrere Technologien für dieses Szenario. Verwenden Sie eine dieser Technologien oder eine Kombination derselben, um die Anforderungen Ihrer Organisation zu erfüllen.

#### <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway
Erstellen Sie in Microsoft Azure ein Cloud Management Gateway, und aktivieren Sie mindestens einen lokalen Softwareupdatepunkt, um Datenverkehr von internetbasierten Clients zuzulassen. Wenn Clients ins Internet wechseln, erfolgt weiterhin die Prüfung mit Ihren Softwareupdatepunkten. Alle internetbasierten Clients erhalten stets Inhalte des Microsoft Update-Clouddienstes. 

Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) und [Konfigurieren von Begrenzungsgruppen](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

#### <a name="internet-based-client-management"></a>Internetbasierte Clientverwaltung
Platzieren Sie einen Softwareupdatepunkt in einem Netzwerk mit Internetverbindung, und lassen Sie für ihn Datenverkehr von internetbasierten Clients zu. Wenn Clients ins Internet wechseln, wechseln sie für die Überprüfung zu diesem Softwareupdatepunkt. Alle internetbasierten Clients erhalten stets Inhalte des Microsoft Update-Clouddienstes.

Weitere Informationen über die Vor- und Nachteile der internetbasierten Clientverwaltung finden Sie unter [Verwalten von Clients im Internet](../../core/clients/manage/manage-clients-internet.md).

#### <a name="windows-update-for-business"></a>Windows Update for Business
Mit Windows Update for Business können Sie Windows 10-Geräte stets mit aktuellsten Qualitäts- und Featureupdates auf dem neuesten Stand halten. Diese Geräte stellen direkt eine Verbindung zum Windows Update-Clouddienst her. Configuration Manager kann zwischen Windows 10-Computern unterscheiden, die WUfB und WSUS zum Abrufen von Softwareupdates verwenden.

Weitere Informationen finden Sie unter [Integration mit Windows Update for Business](../deploy-use/integrate-windows-update-for-business-windows-10.md).


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a> Planen von Softwareupdateinhalten

Clients müssen die Inhaltsdateien für Softwareupdates herunterladen, um sie zu installieren. Configuration Manager bietet verschiedene Technologien, um die Verwaltung und Bereitstellung dieser Inhalte zu unterstützen. Konfigurieren Sie alternativ Softwareupdatebereitstellungen, um zuzulassen oder vorzugeben, dass Clients Inhalte direkt vom Microsoft Update-Clouddienst abrufen.

#### <a name="download-and-distribute-content"></a>Herunterladen und Verteilen von Inhalten 
Standardmäßig verwendet der Softwareupdate-Verwaltungsprozess in Configuration Manager die integrierten Inhaltsverwaltungsfunktionen. Zu diesen Funktionen gehören die zentrale Speicherinhaltsbibliothek mit einer Instanz und das verteilte Design der Verteilungspunkt-Standortsystemrolle. Sie verwenden diese Funktionen, wenn Sie Softwareupdate-Bereitstellungspakete herunterladen und bereitstellen. 

Weitere Informationen finden Sie unter [Herunterladen von Softwareupdates](../deploy-use/download-software-updates.md).

#### <a name="manage-express-installation-files-for-windows-10"></a>Verwalten von Expressinstallationsdateien für Windows 10
Configuration Manager unterstützt die Verwendung von Expressinstallationsdateien für Windows 10-Updates. Expressupdatedateien und unterstützende Technologien wie die Übermittlungsoptimierung können helfen, Auswirkungen auf die Netzwerkleistung zu reduzieren, wenn große Inhaltsdateien auf Clients heruntergeladen werden. 

Weitere Informationen finden Sie unter [Optimieren der Bereitstellung von Updates für Windows 10](../deploy-use/optimize-windows-10-update-delivery.md).

#### <a name="clients-download-content-from-the-internet"></a>Clients laden Inhalte aus dem Internet herunter
Wenn Sie Softwareupdates auf Clients bereitstellen, konfigurieren Sie die Bereitstellung für Clients, wenn diese Inhalte vom Microsoft Update-Clouddienst herunterladen. Wenn Clients Inhalte nicht von einer anderen Inhaltsquelle herunterladen können, können sie die Inhalte weiterhin aus dem Internet herunterladen. 

Ab Version 1806 müssen Sie kein Bereitstellungspaket erstellen, wenn Sie Softwareupdates bereitstellen. Wenn Sie die Option **Kein Bereitstellungspaket** auswählen, können Clients weiterhin Inhalte von lokalen Quellen (sofern verfügbar) herunterladen, üblicherweise erfolgt der Download jedoch vom Microsoft Update-Dienst.<!--1357933-->

Internetbasierte Clients laden Inhalte stets vom Microsoft Update-Clouddienst herunter. Verteilen Sie keine Softwareupdate-Bereitstellungspakete an einen Cloudverteilungspunkt. Die Speicherung auf dem Cloudverteilungspunkt wird in Rechnung gestellt, Clients laden diese Pakete aber nicht herunter. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a> Planen der Updates von Drittanbietern
Configuration Manager integriert WSUS, die von Microsoft veröffentlichte Softwareupdates nativ unterstützen. Die meisten Kunden verwenden Anwendungen von Drittanbietern, die ebenfalls Updates benötigen. Es gibt mehrere Möglichkeiten, um Drittanbieteranwendungen auf dem neuesten Stand zu halten.

#### <a name="supersede-applications-to-update"></a>Ablösen von zu aktualisierenden Anwendungen
Verwenden Sie mit der Anwendungsverwaltung in Configuration Manage eine Ablösungsbeziehung, um ein Upgrade für vorhandene Anwendungen vorzunehmen oder diese zu ersetzen. Wenn Sie eine Anwendung ablösen, geben Sie einen neuen Bereitstellungstyp als Ersatz für den Bereitstellungstyp der abgelösten Anwendung an. Legen Sie außerdem fest, ob vor dem Installieren der ablösenden Anwendung ein Upgrade der abzulösenden Anwendung ausgeführt oder die abzulösende Anwendung deinstalliert werden soll.

Weitere Informationen finden Sie unter [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md).

#### <a name="third-party-software-updates"></a>Updates für Drittanbietersoftware
Verwenden Sie ab Version 1806 den Knoten **Katalog mit Updates für Drittanbietersoftware** in der Configuration Manager-Konsole, um Drittanbieterkataloge zu abonnieren, deren Updates auf Ihrem Softwareupdatepunkt zu veröffentlichen und sie anschließend auf Clients bereitzustellen.<!--1352101-->

Weitere Informationen finden Sie unter [Third-party software updates (Updates für Drittanbietersoftware)](../deploy-use/third-party-software-updates.md).

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP) ist ein eigenständiges Tool, mit dem unabhängige Softwarehersteller oder Entwickler branchenspezifischer Anwendungen benutzerdefinierte Updates verwalten können. Dies schließt Updates mit Abhängigkeiten wie Treiber und Updatepakete mit ein.

Weitere Informationen finden Sie unter [System Center Updates Publisher](../tools/updates-publisher.md).



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> Planen der Installation von Softwareupdatepunkten  

Dieser Abschnitt enthält die folgenden Unterthemen:  
- [Anforderungen für den Softwareupdatepunkt](#BKMK_SUPSystemRequirements)
- [Planen der WSUS-Installation](#BKMK_PlanningForWSUS)
- [Konfigurieren von Firewalls](#BKMK_ConfigureFirewalls)  


Dieser Abschnitt enthält Informationen zu den Schritten, die für die erfolgreiche Planung und Vorbereitung der Installation von Softwareupdatepunkten erforderlich sind. Bevor Sie eine Standortsystemrolle für den Softwareupdatepunkt in Configuration Manager erstellen, müssen mehrere Anforderungen berücksichtigt werden. Die konkreten Anforderungen hängen von Ihrer Configuration Manager-Infrastruktur ab. Wenn Sie den Softwareupdatepunkt für die Kommunikation über HTTPS konfigurieren, ist es besonders wichtig, diesen Abschnitt zu beachten. HTTPS-fähige Server erfordern zusätzliche Schritte, um ordnungsgemäß zu funktionieren.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Anforderungen für den Softwareupdatepunkt  

Installieren Sie die Softwareupdatepunkt-Rolle auf einem Standortsystem, das die Mindestanforderungen für WSUS erfüllt und den unterstützten Konfigurationen für Configuration Manager-Standortsysteme entspricht.  

-   Weitere Informationen zu den Mindestanforderungen für die WSUS-Serverrolle in Windows Server finden Sie unter [Review considerations and system requirements (Zu berücksichtigende Überlegungen und Systemanforderungen)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements).  

-   Weitere Informationen zu den unterstützten Konfigurationen für Configuration Manager-Standortsysteme finden Sie unter [Anforderungen an Standorte und Standortsysteme](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Planen der WSUS-Installation  

Installieren Sie eine unterstützte Version von WSUS auf allen Standortsystemservern, die Sie für die Softwareupdatepunkt-Rolle konfigurieren. Wenn Sie den Softwareupdatepunkt nicht auf dem Standortserver installieren, müssen Sie auf dem Standortserver die WSUS-Administrationskonsole installieren. Diese Komponente erlaubt es dem Standortserver, mit auf dem Softwareupdatepunkt ausgeführten WSUS zu kommunizieren.  

Wenn Sie WSUS auf Windows Server 2012 oder höher verwenden, müssen Sie zusätzliche Berechtigungen konfigurieren, um es der Komponente **WSUS Configuration Manager** in Configuration Manager zu erlauben, eine Verbindung zu WSUS herzustellen. Diese Komponente führt regelmäßige Integritätsprüfungen durch. Zum Konfigurieren der erforderlichen Berechtigungen stehen folgende Möglichkeiten zur Auswahl:  

-   Fügen Sie der Gruppe **WSUS-Administratoren** das Konto **SYSTEM** hinzu.  

-   Fügen Sie das Konto **NT AUTHORITY\SYSTEM** als Benutzer für die WSUS-Datenbank (SUSDB) hinzu. Konfigurieren Sie mindestens die WebService-Datenbankrollenmitgliedschaft.  
  
Weitere Informationen zum Installieren von WSUS unter Windows Server finden Sie unter [Install the WSUS Server Role (Installieren der WSUS-Serverrolle)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Wenn Sie an einem primären Standort mehrere Softwareupdatepunkte installieren, sollten Sie für jeden Softwareupdatepunkt einer Active Directory-Gesamtstruktur die gleiche WSUS-Datenbank verwenden. Die Freigabe derselben Datenbank verbessert die Leistung, wenn Clients zu einem neuen Softwareupdatepunkt wechseln. Weitere Informationen finden Sie unter [Verwenden einer freigegebenen WSUS-Datenbank für Softwareupdatepunkte](software-updates-best-practices.md#bkmk_shared-susdb).  

#### <a name="configuring-the-wsus-content-directory-path"></a>Konfigurieren des WSUS-Inhaltsverzeichnispfads

Wenn Sie WSUS installieren, müssen Sie einen Inhaltsverzeichnispfad angeben. Das WSUS-Inhaltsverzeichnis wird hauptsächlich zum Speichern der Dateien für die Microsoft-Software-Lizenzbedingungen verwendet, die während des Scans von Clients benötigt werden. Das WSUS-Inhaltsverzeichnis sollte nicht mit Ihrem Inhaltsquellverzeichnis für Configuration Manager-Softwarebereitstellungspakete überlappen. Wenn das WSUS-Inhaltsverzeichnis und die Configuration Manager-Paketquelle überlappen, werden die falschen Dateien aus dem WSUS-Inhaltsverzeichnis entfernt.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a> Konfigurieren von WSUS für die Verwendung einer benutzerdefinierten Website  
Beim Installieren von WSUS haben Sie die Möglichkeit, die vorhandene IIS-Standardwebsite zu verwenden oder eine benutzerdefinierte WSUS-Website zu erstellen. Erstellen Sie eine benutzerdefinierte Website für WSUS, damit IIS die WSUS-Dienste auf einer dedizierten virtuellen Website hosten. Andernfalls verwenden sie dieselbe Website, die von den anderen Configuration Manager-Standortsystemen oder -Anwendungen verwendet wird. Diese Konfiguration ist insbesondere erforderlich, wenn Sie die Softwareupdatepunkt-Rolle auf dem Standortserver installieren. Wenn Sie WSUS unter Windows Server 2012 oder höher ausführen, wird WSUS standardmäßig für die Verwendung von Port 8530 für HTTP und Port 8531 für HTTPS konfiguriert. Geben Sie diese Ports beim Erstellen des Softwareupdatepunkts an einem Standort an.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Verwenden einer vorhandenen WSUS-Infrastruktur  
Wählen Sie einen WSUS-Server aus, der bereits vor der Installation von Configuration Manager in Ihrer Umgebung aktiv war, als Softwareupdatepunkt aus. Geben Sie beim Konfigurieren des Softwareupdatepunkts die Synchronisierungseinstellungen an. Configuration Manager stellt eine Verbindung mit dem WSUS-Server auf dem Softwareupdatepunkt-Server her, und konfiguriert WSUS mit den gleichen Einstellungen. 

Bevor Sie den Server als Softwareupdatepunkt konfigurieren, vergleichen Sie seine Konfiguration für Produkte und Klassifizierungen mit Ihren Configuration Manager-Einstellungen. Wenn Sie den vorhandenen WSUS-Server synchronisiert haben, bevor Sie ihn als Softwareupdatepunkt konfigurieren, und die Listen von Produkten und Klassifizierungen voneinander abweichen, werden alle Metadaten für Softwareupdates unabhängig von den konfigurierten Einstellungen synchronisiert. Dieses Verhalten führt zu unerwarteten Metadaten für Softwareupdates in der Standortdatenbank. 

Dieses Verhalten kann auch beobachtet werden, wenn Sie Produkte oder Klassifizierungen direkt in der WSUS-Verwaltungskonsole hinzufügen und die Synchronisierung sofort initiieren. Standardmäßig stellt Configuration Manager stündlich eine Verbindung mit WSUS her und setzt alle Einstellungen zurück, die außerhalb von Configuration Manager geändert wurden. Softwareupdates, die nicht den von Ihnen in den Synchronisierungseinstellungen angegebenen Produkten und Klassifizierungen entsprechen, werden als abgelaufen festgelegt. Anschließend werden sie aus der Standortdatenbank entfernt.  

Wenn ein WSUS-Server als Softwareupdatepunkt konfiguriert wurde, können Sie ihn nicht mehr als eigenständigen WSUS-Server verwenden. Wenn Sie einen separaten eigenständigen WSUS-Server benötigen, der nicht von Configuration Manager verwaltet wird, müssen Sie diesen auf einem anderen Server konfigurieren.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Konfigurieren von WSUS als Replikatserver  
Wenn Sie die Softwareupdatepunkt-Rolle auf einem primären Standortserver hinzufügen, können Sie keinen WSUS-Server verwenden, der als Replikat konfiguriert ist. Ist der WSUS-Server als Replikat konfiguriert, kann er nicht von Configuration Manager konfiguriert werden, und bei der WSUS-Synchronisierung tritt ein Fehler auf. Der erste Softwareupdatepunkt, den Sie an einem primären Standort installieren, ist der Standard-Softwareupdatepunkt. Weitere Softwareupdatepunkte am Standort werden als Replikate des Standard-Softwareupdatepunkts konfiguriert.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Entscheiden, ob WSUS zur Verwendung von SSL konfiguriert werden soll  
Verwenden Sie das SSL-Protokoll, um den Softwareupdatepunkt zu schützen. SSL wird von WSUS zur Authentifizierung von Clientcomputern und WSUS-Downstreamservern gegenüber dem WSUS-Server verwendet. SSL wird von WSUS auch zum Verschlüsseln von Metadaten für Softwareupdates verwendet. Wenn Sie sich entscheiden, WSUS durch SSL zu schützen, müssen Sie den WSUS-Server vor der Installation des Softwareupdatepunkts entsprechend vorbereiten. Weitere Informationen finden Sie im Artikel [Configure SSL on the WSUS server (Konfigurieren von SSL auf dem WSUS-Server)](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) in der Dokumentation zu WSUS. 

Wählen Sie beim Installieren und Konfigurieren des Softwareupdatepunkts die Option **Enable SSL communications for the WSUS Server** (SSL-Kommunikation für den WSUS-Server aktivieren) aus. Andernfalls konfiguriert Configuration Manager WSUS nicht zur Verwendung von SSL. Wenn Sie SSL auf einem Softwareupdatepunkt aktivieren, müssen Sie auch alle Softwareupdatepunkte an untergeordneten Standorten so konfigurieren, dass sie SSL verwenden.  


###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> Konfigurieren von Firewalls  

Der Softwareupdatepunkt an einem Standort der zentralen Verwaltung von Configuration Manager kommuniziert mit WSUS auf dem Softwareupdatepunkt. WSUS kommuniziert mit der Synchronisierungsquelle, um Softwareupdate-Metadaten zu synchronisieren. Softwareupdatepunkte an einem untergeordneten Standort kommunizieren mit dem Softwareupdatepunkt am übergeordneten Standort. Wenn es an einem primären Standort mehrere Softwareupdatepunkte gibt, müssen die zusätzlichen Softwareupdatepunkte mit dem Standard-Softwareupdatepunkt kommunizieren. Die Standardrolle ist der erste Softwareupdatepunkt, der am Standort installiert wurde.  

Sie müssen möglicherweise die Firewall so konfigurieren, dass sie den HTTP- bzw. HTTPS-Datenverkehr zulässt, der von WSUS in folgenden Situationen verwendet wird: 
- Zwischen dem Softwareupdatepunkt und dem Internet
- Zwischen einem Softwareupdatepunkt und der Upstream-Synchronisierungsquelle
- Zwischen zusätzlichen Softwareupdatepunkten  

Die Verbindung mit Microsoft Update ist immer für die Verwendung von Port 80 für HTTP und von Port 443 für HTTPS konfiguriert. Verwenden Sie einen benutzerdefinierten Port für die Verbindung von WSUS auf dem Softwareupdatepunkt an einem untergeordneten Standort zu WSUS auf dem Softwareupdatepunkt am übergeordneten Standort. Wenn die Verbindung aufgrund Ihrer Sicherheitsrichtlinie nicht möglich ist, verwenden Sie die Export-/Import-Synchronisierungsmethode. Weitere Informationen finden Sie im Abschnitt [Synchronisierungsquelle](#BKMK_SyncSource) in diesem Artikel. Weitere Informationen zu den Ports, die von WSUS verwendet werden, finden Sie unter [Bestimmen der Porteinstellungen für WSUS in Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Beschränken des Zugriffs auf bestimmte Domänen  

Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, müssen Sie den Zugriff auf Internetendpunkte durch den aktiven Softwareupdatepunkt zulassen. Dann können WSUS und automatische Updates mit dem Microsoft Update-Clouddienst kommunizieren.

Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../core/plan-design/network/internet-endpoints.md#bkmk_sum).


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Planen der Synchronisierungseinstellungen  

Dieser Abschnitt enthält die folgenden Unterthemen:  
- [Synchronisierungsquelle](#BKMK_SyncSource)
- [Synchronisierungszeitplan](#BKMK_SyncSchedule)
- [Updateklassifizierungen](#BKMK_UpdateClassifications)
- [Produkte](#BKMK_UpdateProducts)
- [Ablösungsregeln](#BKMK_SupersedenceRules)
- [Sprachen](#BKMK_UpdateLanguages)  
- [Maximale Laufzeit](#bkmk_maxruntime)


Bei der Softwareupdatesynchronisierung in Configuration Manager werden die Metadaten für Softwareupdates unter Berücksichtigung der von Ihnen konfigurierten Kriterien heruntergeladen. Der Standort der obersten Ebene in Ihrer Hierarchie synchronisiert Softwareupdates von Microsoft Update. Sie haben die Möglichkeit, den Softwareupdatepunkt am Standort der obersten Ebene so zu konfigurieren, dass er mit einem vorhandenen WSUS-Server, der sich nicht in der Configuration Manager-Hierarchie befindet, synchronisiert wird. Von untergeordneten primären Standorten werden Metadaten für Softwareupdates synchronisiert, die vom Softwareupdatepunkt am Standort der zentralen Verwaltung stammen. Planen Sie mithilfe dieses Abschnitts die Synchronisierungseinstellungen, bevor Sie einen Softwareupdatepunkt installieren und konfigurieren.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> Synchronisierungsquelle  

In den Einstellungen für die Synchronisierungsquelle des Softwareupdatepunkts wird angegeben, von welchem Ort die Metadaten für Softwareupdates vom Softwareupdatepunkt abgerufen werden. Außerdem wird angegeben, ob die Synchronisierung WSUS-Berichterstattungsereignisse erstellt.  

-   **Synchronisierungsquelle:** Die Synchronisierungsquelle für Microsoft Update wird standardmäßig vom Softwareupdatepunkt am Standort der obersten Ebene konfiguriert. Sie haben die Möglichkeit, den Standort der obersten Ebene mit einem vorhandenen WSUS-Server zu synchronisieren. Vom Softwareupdatepunkt an einem untergeordneten primären Standort wird die Synchronisierungsquelle als Softwareupdatepunkt des Standorts der zentralen Verwaltung konfiguriert.  

    -  Der erste Softwareupdatepunkt, den Sie an einem primären Standort installieren und der als Standard-Softwareupdatepunkt dient, wird mit dem Standort der zentralen Verwaltung synchronisiert. Weitere Softwareupdatepunkte am primären Standort werden mit dem Standard-Softwareupdatepunkts am primären Standort synchronisiert.  

    - Wenn ein Softwareupdatepunkt von Microsoft Update oder dem Upstream-Updateserver getrennt ist, können Sie die Synchronisierungsquelle so konfigurieren, dass die Synchronisierung nicht mit einer konfigurierten Synchronisierungsquelle erfolgt. Stattdessen konfigurieren Sie sie mithilfe der Export- und Importfunktion des Tools **WSUSUtil**, um Softwareupdates zu synchronisieren. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt](../get-started/synchronize-software-updates-disconnected.md).  

-   **Ereignisse der WSUS-Berichterstattung:** Der Windows Update-Agent auf Clientcomputern kann Ereignismeldungen erstellen, die für die WSUS-Berichterstattung verwendet werden. Diese Ereignisse werden nicht von Configuration Manager verwendet. Daher ist die Option **Keine WSUS-Berichterstattungsereignisse erstellen** standardmäßig aktiviert. Wenn diese Ereignisse nicht erstellt werden, sollte der Client lediglich während der Softwareupdatebewertung und Kompatibilitätsüberprüfung eine Verbindung mit dem WSUS-Server herstellen. Wenn diese Ereignisse für die Berichterstattung außerhalb von Configuration Manager benötigt werden, müssen Sie diese Einstellung ändern, damit WSUS-Berichterstattungsereignisse erstellt werden können.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Synchronisierungszeitplan  

Konfigurieren Sie den Synchronisierungszeitplan nur auf dem Softwareupdatepunkt am Standort der obersten Ebene in der Configuration Manager-Hierarchie. Wenn Sie den Synchronisierungszeitplan konfigurieren, findet die Synchronisierung des Softwareupdatepunkts mit der Synchronisierungsquelle zum angegebenen Zeitpunkt statt. Der benutzerdefinierte Zeitplan erlaubt es Ihnen, Softwareupdates zu synchronisieren und so für Ihre Umgebung zu optimieren. Berücksichtigen Sie die Leistungsanforderungen des WSUS-Servers, des Standortservers und des Netzwerks. Beispiel: 2:00 Uhr einmal pro Woche. Alternativ kann die Synchronisierung am Standort der obersten Ebene mit der Aktion **Softwareupdates synchronisieren** manuell gestartet werden. Diese Aktion befindet sich im Knoten **Alle Softwareupdates** oder **Softwareupdategruppen** in der Configuration Manager-Konsole.  

> [!TIP]  
>  Planen Sie die Softwareupdatesynchronisierung so, dass sie zu einem für Ihre Umgebung geeigneten Zeitpunkt ausgeführt wird. Eine häufig verwendete Möglichkeit besteht darin, den Zeitplan so zu wählen, dass die Synchronisierung kurz nach der Veröffentlichung der regulären Microsoft-Softwareupdates am zweiten Dienstag eines jeden Monats ausgeführt wird. Dieser Tag wird üblicherweise als *Patch-Dienstag* bezeichnet. Wenn Sie Configuration Manager verwenden, um Endpoint Protection- und Windows Defender-Definitions- und -Engine-Updates bereitzustellen, sollten Sie eine tägliche Ausführung des Synchronisierungszeitplans festlegen.  

Nach der erfolgreichen Synchronisierung durch den Softwareupdatepunkt wird eine Synchronisierungsanforderung an untergeordnete Standorte gesendet. Wenn es an einem primären Standort weitere Softwareupdatepunkte gibt, sendet der Softwareupdatepunkt eine Synchronisierungsanforderung an jeden dieser Softwareupdatepunkte. Dieser Prozess wird an jedem Standort der Hierarchie wiederholt.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Updateklassifizierungen  

Jedes Softwareupdate ist mit einer Updateklassifizierung definiert, die bei der Einteilung in verschiedene Updatearten behilflich ist. Bei der Synchronisierung synchronisiert der Standort die Metadaten für die angegebenen Klassifizierungen. 

Configuration Manager unterstützt die Synchronisierung der folgenden Updateklassifizierungen:  

-   **Wichtige Updates:** Gibt ein im großen Umfang freigegebenes Update für ein bestimmtes Problem an, mit dem ein wichtiger, nicht sicherheitsrelevanter Fehler behoben wird.  

-   **Definitionsupdates:** Gibt ein Update für Virus- oder andere Definitionsdateien an.  

-   **Feature Packs:** Neue Produktfunktionen, die außerhalb einer Produktversion verteilt werden und in der Regel in der nächsten vollständigen Produktversion enthalten sind.  

-   **Sicherheitsupdates**: Gibt ein im großen Umfang freigegebenes Update für ein produktspezifisches, sicherheitsrelevantes Problem an.  

-   **Service Packs:** Kumulative Hotfixes, die auf ein Betriebssystem oder eine Anwendung angewendet werden. Diese Hotfixes können Sicherheitsupdates, wichtige Updates und Softwareupdates umfassen.  

-   **Tools:** Ein Dienstprogramm oder Feature, das bei der Durchführung einer oder mehrerer Aufgaben hilft.  

-   **Updaterollups:** Kumulative Hotfixes, die zwecks einfacher Bereitstellung gebündelt sind. Diese Hotfixes können Sicherheitsupdates, wichtige Updates und Softwareupdates umfassen. Ein Aktualisierungsrollup betrifft in der Regel einen bestimmten Bereich, z. B. Sicherheit oder eine Produktkomponente.  

-   **Updates:** Ein Update für eine aktuell installierte Anwendung oder Datei.  

-   **Upgrades**: Ein Featureupdate auf eine neue Version von Windows 10.  

Konfigurieren Sie die Updateklassifizierungseinstellungen nur am Standort der obersten Ebene. Die Updateklassifizierungseinstellungen werden nicht auf dem Softwareupdatepunkt untergeordneter Standorte konfiguriert, da die Metadaten der Softwareupdates vom Standort der obersten Ebene repliziert werden. Beim Auswählen der Updateklassifizierungen nimmt die Synchronisierung der Softwareupdate-Metadaten umso mehr Zeit in Anspruch, je mehr Klassifizierungen ausgewählt werden.  

> [!WARNING]  
>  Es wird empfohlen, vor der ersten Synchronisierung die Auswahl sämtlicher Klassifizierungen aufzuheben. Wählen Sie nach der Erstsynchronisierung die gewünschten Klassifizierungen aus, und wiederholen Sie die Synchronisierung.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a> Produkte  

Anhand der Metadaten für die einzelnen Softwareupdates werden ein oder mehrere Produkte definiert, für die das Update gilt. Ein Produkt ist eine bestimmte Edition eines Betriebssystems oder einer Anwendung. Ein Beispiel für ein Produkt ist Microsoft Windows 10. Eine Produktfamilie ist das Basisbetriebssystem bzw. die Basisanwendung, von dem bzw. der die einzelnen Produkte abgeleitet sind. Ein Beispiel für eine Produktfamilie ist Microsoft Windows. Windows 10 und Windows Server 2016 sind Mitglieder dieser Produktfamilie. Wählen Sie eine Produktfamilie oder einzelne Produkte innerhalb einer Produktfamilie aus.  

Wenn Softwareupdates auf mehrere Produkte anwendbar sind und mindestens eines der Produkte für die Synchronisierung ausgewählt wurde, werden sämtliche Produkte in der Configuration Manager-Konsole angezeigt, auch wenn einige Produkte nicht ausgewählt wurden. Wählen Sie beispielsweise nur das Produkt Windows Server 2012 aus. Wenn ein Softwareupdate für Windows Server 2012 und Windows Server 2012 Datacenter Edition gilt, befinden sich beide Produkte in der Standortdatenbank.  

Konfigurieren Sie die Produkteinstellungen nur am Standort der obersten Ebene. Die Produkteinstellungen werden nicht auf dem Softwareupdatepunkt für untergeordnete Standorte konfiguriert, da die Metadaten der Softwareupdates vom Standort der obersten Ebene repliziert werden. Je mehr Produkte ausgewählt sind, desto länger dauert die Synchronisierung der Softwareupdate-Metadaten.  

> [!IMPORTANT]  
>  Configuration Manager speichert eine Liste der Produkte und Produktfamilien, aus denen Sie bei der Erstinstallation des Softwareupdatepunkts eine Auswahl treffen. Produkte und Produktfamilien, die nach der Veröffentlichung von Configuration Manager veröffentlicht werden, können möglicherweise erst ausgewählt werden, nachdem Sie die Synchronisierung abgeschlossen haben. Der Synchronisierungsvorgang aktualisiert die Liste der verfügbaren Produkte und Produktfamilien, aus denen Sie eine Auswahl treffen können. Heben Sie die Auswahl sämtlicher Produkte auf, bevor Sie erstmalig Softwareupdates synchronisieren. Wählen Sie nach der Erstsynchronisierung die gewünschten Produkte aus, und wiederholen Sie die Synchronisierung.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a> Ablösungsregeln  

Mit einem Softwareupdate, das ein anderes Softwareupdate ablöst, werden in der Regel folgende Aktionen ausgeführt:  

-   Erweiterung, Verbesserung oder Aktualisierung der Korrekturen, die von früher herausgegebenen Updates bereitgestellt wurden.  

-   Steigerung der Effizienz des abgelösten Updatedateipakets, das auf Clients installiert wird, sofern die Installation des Updates genehmigt wird. Ein abgelöstes Update kann beispielsweise Dateien enthalten, die für die von dem neuen Update unterstützten Fixes oder Betriebssysteme nicht mehr relevant sind. Solche Dateien sind in dem ablösenden Dateipaket des Updates nicht enthalten.  

-   Ausführung eines Updates für neuere Produktversionen. Anders ausgedrückt: Es werden Versionen aktualisiert, die für ältere Versionen oder Konfigurationen eines Produkts nicht mehr gültig sind. Updates können außerdem durch andere Updates abgelöst werden, wenn zur Erweiterung der Sprachunterstützung entsprechende Änderungen vorgenommen wurden. Beispielsweise wäre es möglich, dass in einer späteren Version eines Produktupdates für Microsoft 365-Apps ein älteres Betriebssystem nicht mehr unterstützt, dafür aber in der Erstversion des Updates die Sprachunterstützung erweitert wird.  

Geben Sie in den Eigenschaften des Softwareupdatepunkts an, dass abgelöste Softwareupdates sofort ablaufen. Diese Einstellung verhindert, dass sie in neue Bereitstellungen eingeschlossen werden. Außerdem werden so auch die vorhandenen Bereitstellungen gekennzeichnet, um anzugeben, dass sie mindestens ein abgelaufenes Softwareupdate enthalten. Geben Sie alternativ einen Zeitraum an, bis zu dem die abgelösten Softwareupdates ablaufen. Mit dieser Aktion können Sie die Updates weiterhin bereitstellen. 

Die Bereitstellung eines abgelösten Softwareupdates kann in folgenden Situationen empfehlenswert sein:  

-   Ein ablösendes Softwareupdate unterstützt nur neuere Versionen eines Betriebssystems. Auf einigen Ihrer Clientcomputer werden frühere Versionen des Betriebssystems ausgeführt.  

-   Die Anwendbarkeit eines ablösenden Softwareupdates ist stärker eingeschränkt als die des abzulösenden Softwareupdates. Dieses Verhalten würde das ablösende Softwareupdate für einige Clientcomputer ungeeignet machen.  

-   Die Bereitstellung eines ablösenden Softwareupdates wurde in Ihrer Produktionsumgebung nicht genehmigt.  

    > [!NOTE]  
    > - Vor Configuration Manager-Version 1806, wenn Configuration Manager ein abgelöstes Softwareupdate auf **Abgelaufen** festlegt, wird das Update in WSUS nicht auf **Abgelehnt** festgelegt. Clients suchen so lange weiterhin nach einem abgelaufenen Update, bis das Update manuell oder mit einem benutzerdefinierten Skript abgelehnt wird.  Nach Configuration Manager-Version 1806 lehnt Configuration Manager auch die abgelösten Updates in WSUS ab. Weitere Informationen zur WSUS-Bereinigungsaufgabe finden Sie unter [Wartung für Softwareupdates](../deploy-use/software-updates-maintenance.md).
    > - Ab Version 1810 von Configuration Manager können Sie das Verhalten der Ablösungsregeln für **Featureupdates** separat von **anderen Updates** festlegen.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a> Sprachen  

Mit den Spracheinstellungen für den Softwareupdatepunkt können Sie Folgendes konfigurieren: 
- Die Sprachen, für die Übersichtsdetails (Softwareupdate-Metadaten) für Softwareupdates synchronisiert werden  
- Die Softwareupdate-Dateisprachen, die für Softwareupdates heruntergeladen werden  

#### <a name="software-update-file"></a>Softwareupdatedatei  
Konfigurieren Sie Sprachen für die Einstellung **Softwareupdatedatei** in den Eigenschaften für den Softwareupdatepunkt. Mit dieser Einstellung werden die Standardsprachen bereitgestellt, die verfügbar sind, wenn Sie Softwareupdates an einem Standort herunterladen. Passen Sie an, welche Sprachen beim Herunterladen oder Bereitstellen von Softwareupdates standardmäßig ausgewählt sind. Während des Herunterladens werden die verfügbaren Softwareupdatedateien für die konfigurierten Sprachen an den Quellspeicherort des Bereitstellungspakets heruntergeladen, wenn die Softwareupdatedateien in der ausgewählten Sprache verfügbar sind. Anschließend werden sie in die Inhaltsbibliothek auf dem Standortserver kopiert. Danach werden sie an die Verteilungspunkte verteilt, die für das Paket konfiguriert sind.  

Konfigurieren Sie die Spracheinstellungen der Softwareupdatedatei mit den Sprachen, die in Ihrer Umgebung am häufigsten verwendet werden. Die Clients an Ihrem Standort verwenden beispielsweise überwiegend Englisch und Japanisch für Windows oder Anwendungen. Am Standort werden noch einige wenige andere Sprachen verwendet. Wählen Sie in der Spalte **Softwareupdatedatei** nur Englisch und Japanisch aus, wenn Sie das Softwareupdate herunterladen oder bereitstellen. Mit dieser Aktion können Sie die Standardeinstellungen auf der Seite **Sprachauswahl** der Assistenten zum Bereitstellen und Herunterladen verwenden. Ferner wird durch diese Aktion verhindert, dass nicht benötigte Updatedateien heruntergeladen werden. Konfigurieren Sie diese Einstellung auf jedem Softwareupdatepunkt in der Configuration Manager-Hierarchie.  



#### <a name="summary-details"></a>Übersichtsdetails  
Während des Synchronisierungsprozesses werden die Übersichtsdetails (Softwareupdate-Metadaten) für Softwareupdates in den angegebenen Sprachen aktualisiert. Die Metadaten enthalten beispielsweise folgende Informationen zum Softwareupdate:
- Name
- Beschreibung
- Produkte, die das Update unterstützt
- Updateklassifizierung
- Artikel-ID
- Download-URL
- Anwendbarkeitsregeln

Konfigurieren Sie die Einstellungen der Übersichtsdetails nur am Standort der obersten Ebene. Die Übersichtsdetails werden nicht auf dem Softwareupdatepunkt untergeordneter Standorte konfiguriert, da die Metadaten der Softwareupdates mithilfe dateibasierter Replikation vom Standort der zentralen Verwaltung repliziert werden. Wählen Sie für die Übersichtsdetails nur die in der Umgebung erforderlichen Sprachen aus. Je mehr Sprachen ausgewählt sind, desto länger dauert die Synchronisierung der Softwareupdate-Metadaten. Configuration Manager zeigt die Metadaten der Softwareupdates im Gebietsschema des Betriebssystems an, unter dem die Configuration Manager-Konsole ausgeführt wird. Falls die lokalisierten Eigenschaften der Softwareupdates im Gebietsschema dieses Betriebssystems nicht verfügbar sind, werden die Softwareupdateinformationen auf Englisch angezeigt.  

> [!IMPORTANT]  
>  Wählen Sie alle Sprachen für Übersichtsdetails aus, die Sie benötigen. Beim Synchronisieren des Softwareupdatepunkts am Standort der obersten Ebene mit der Synchronisierungsquelle wird anhand der ausgewählten Sprachen für Übersichtsdetails bestimmt, welche Softwareupdate-Metadaten abgerufen werden. Wenn Sie die Sprachen für Übersichtsdetails ändern, nachdem die Synchronisierung mindestens einmal ausgeführt wurde, werden die Softwareupdate-Metadaten für die geänderten Übersichtsdetailsprachen nur für neue und aktualisierte Softwareupdates abgerufen. Für die bereits synchronisierten Softwareupdates werden neue Metadaten für die geänderten Sprachen nur abgerufen, wenn auf der Synchronisierungsquelle eine Änderung des Softwareupdates vorgenommen wurde.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a> Maximale Laufzeit
<!--3734426-->
*(Eingeführt in Version 1906)*

Ab Version 1906 können Sie angeben, wie lange die Installation eines Softwareupdates maximal dauern darf. Sie können die maximal zulässige Ausführungsdauer für Folgendes angeben:

- **Maximale Laufzeit für Windows-Featureupdates (Minuten)**
  - **Featureupdates**: ein Update, das zu einer der folgenden drei Klassifizierungen gehört:
    - Upgrades
    - Updaterollups
    - Service Packs

- **Maximale Laufzeit für Office 365-Updates und Nicht-Featureupdates für Windows (Minuten)**
  - **Nicht-Featureupdates**: ein Update, das kein Upgrade von Features darstellt und dessen Produkt als eines der folgenden aufgeführt ist:
    - Windows 10 (alle Versionen)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- Diese Einstellungen ändern nur die maximale Ausführungsdauer für neue Updates, die mit Microsoft Update synchronisiert sind. Die Ausführungsdauer für vorhandene Feature- und Nicht-Featureupdates wird nicht geändert.
- Alle anderen Produkte und Klassifizierungen sind nicht mit dieser Einstellung konfigurierbar. Wenn Sie die maximale Ausführungsdauer eines dieser Updates ändern müssen, [konfigurieren Sie die Einstellungen für Softwareupdate](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings).

> [!NOTE]
> In Version 1906 ist die maximale Laufzeit nicht verfügbar, wenn Sie den Softwareupdatepunkt der obersten Ebene installieren. Bearbeiten Sie nach der Installation die maximale Laufzeit für Ihren Softwareupdatepunkt der obersten Ebene.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> Planung eines Wartungsfensters für Softwareupdates  

Fügen Sie ein Wartungsfenster speziell für die Installation von Softwareupdates hinzu. Durch diese Aktion können Sie ein allgemeines Wartungsfenster sowie ein abweichendes Wartungsfenster für Softwareupdates konfigurieren. Wenn Sie ein allgemeines Wartungsfenster und ein Wartungsfenster für Softwareupdates konfigurieren, werden Softwareupdates auf Clients nur während des Wartungsfensters für Softwareupdates installiert. 

Ab Version 1810 von Configuration Manager können Sie dieses Verhalten ändern und die Installation von Softwareupdates während eines allgemeinen Wartungsfensters zulassen. Weitere Informationen zu dieser Clienteinstellung finden Sie unter [Clienteinstellungen für Softwareupdates](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).

Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Neustartoptionen für Windows 10-Clients nach der Installation von Softwareupdates

Wenn ein Softwareupdate, das einen Neustart benötigt, mit Configuration Manager bereitgestellt und installiert wird, plant der Client einen ausstehenden Neustart, und das Dialogfeld „Neu starten“ wird angezeigt.

Bei einem ausstehenden Neustart für ein Configuration Manager-Softwareupdate sind die Optionen **Aktualisieren und neu starten** und **Aktualisieren und herunterfahren** auf Windows 10-Computern in den Energieoptionen von Windows verfügbar. Nach der Verwendung einer dieser Optionen wird das Dialogfeld „Neu starten“ nach dem Neustart des Computers nicht angezeigt. Unter gewissen Umständen kann das Betriebssystem die Optionen für ausstehende Neustarts entfernen. Dies kann beispielsweise geschehen, wenn das Schnellstartfeature unter Windows 10 aktiviert ist. Weitere Informationen finden Sie unter [Updates können möglicherweise nicht mit Schnellstart in Windows 10 installiert werden](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup).

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a> Auswerten von Softwareupdates nach einem Wartungsstapelupdate
<!--4639943-->
Ab Version 2002 erkennt Configuration Manager, ob ein Wartungsstapelupdate (Servicing Stack Update, SSU) Teil einer Installation für mehrere Updates ist. Wenn ein SSU erkannt wird, wird es zuerst installiert. Nach der Installation des SSU wird ein Auswertungszyklus für Softwareupdates ausgeführt, um die verbleibenden Updates zu installieren. Mit dieser Änderung kann nach dem Wartungsstapelupdate ein abhängiges kumulatives Update installiert werden. Das Gerät muss zwischen den Installationen nicht neu gestartet werden, und Sie müssen kein zusätzliches Wartungsfenster erstellen. SSUs werden nur bei nicht vom Benutzer initiierten Installationen zuerst installiert. Wenn ein Benutzer beispielsweise eine Installation von mehreren Updates aus dem Software Center initiiert, wird das SSU möglicherweise nicht zuerst installiert. Bei der Verwendung der Configuration Manager-Version 2002 können SSUs für Windows Server-Betriebssysteme nicht zuerst installiert werden. <!--7813007-->Diese Funktionalität wurde in Configuration Manager-Version 2006 für Windows Server-Betriebssysteme hinzugefügt.



## <a name="next-steps"></a>Nächste Schritte
Lesen Sie [Vorbereiten der Softwareupdateverwaltung](../get-started/prepare-for-software-updates-management.md), sobald Sie Softwareupdates planen.  

Weitere Informationen zum Verwalten von Windows-as-a-Service finden Sie unter [Fundamentals of Configuration Manager as a service and Windows as a service (Grundlagen von Configuration Manager-as-a-Service und Windows-as-a-Service)](../../core/understand/configuration-manager-and-windows-as-service.md).
