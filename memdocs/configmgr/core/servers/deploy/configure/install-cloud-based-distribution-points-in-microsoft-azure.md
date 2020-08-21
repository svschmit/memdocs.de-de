---
title: Installieren von Cloudverteilungspunkten
titleSuffix: Configuration Manager
description: Gehen Sie wie folgt vor, um einen Cloudverteilungspunkt in Configuration Manager einzurichten.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a1e19025af82c9beeed8c227871df94b4674791
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692705"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Installieren eines Cloudverteilungspunkts für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Die Implementierung für die Freigabe von Inhalten aus Azure hat sich geändert. Verwenden Sie ein inhaltsfähiges Cloud-Management-Gateway, indem Sie die Option **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen** aktivieren. Weitere Informationen finden Sie unter [Ändern eines CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Zukünftig können Sie keinen herkömmlichen Cloudverteilungspunkt mehr erstellen. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

In diesem Artikel werden die Schritte für die Installation eines Configuration Manager-Cloudverteilungspunkts in Microsoft Azure beschrieben. Er enthält folgende Abschnitte:

- [Vorbereitung](#bkmk_before)
- [Einrichten](#bkmk_setup)
- [Konfigurieren von DNS](#bkmk_dns)
- [Einrichten eines Standortserverproxys](#bkmk_proxy)
- [Verteilen von Inhalten und Konfigurieren von Clients](#bkmk_client)
- [Verwalten und Überwachen](#bkmk_monitor)
- [Änderung](#bkmk_modify)
- [Erweiterte Problembehandlung](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> Vorbereitung

Lesen Sie zunächst den Artikel [Verwenden eines cloudbasierten Verteilungspunkts](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Mithilfe dieses Artikels können Sie Ihre Cloudverteilungspunkte planen und entwerfen.

Verwenden Sie die folgende Prüfliste, um sicherzustellen, dass Sie über die erforderlichen Informationen und Voraussetzungen für die Erstellung eines Cloudverteilungspunkts verfügen:  

- Der Standortserver kann eine Verbindung mit Azure herstellen. Wenn in Ihrem Netzwerk ein Proxy verwendet wird, [konfigurieren Sie die Standortsystemrolle](#bkmk_proxy).  

- Die zu verwendende **Azure-Umgebung**. Beispiel: die Azure Public Cloud oder die Azure US Government Cloud.  

- Verwenden Sie ab Version 1806 die **Azure Resource Manager-Bereitstellung**. Dies ist die *empfohlene Vorgehensweise*. In diesem Fall gelten die folgenden Anforderungen:<!--1322209-->  

    - Integration in [Azure Active Directory](azure-services-wizard.md) für **Cloud Management**. Die Azure Active Directory-Benutzerermittlung ist nicht erforderlich.  

    - Azure-**Abonnement-ID**  

    - Azure-**Ressourcengruppe**  

    - Bei der Ausführung des Assistenten muss ein **Abonnement-Administratorkonto** angemeldet werden.  

- Ein als PFX-Datei exportiertes **Serverauthentifizierungszertifikat**  

- Ein global eindeutiger **Dienstname** für den Cloudverteilungspunkt  

    > [!TIP]  
    > Überzeugen Sie sich zunächst davon, dass der gewünschte Azure-Domänenname eindeutig ist, bevor Sie das Serverauthentifizierungszertifikat mit diesem Dienstnamen anfordern. Beispiel: *WallaceFalls.CloudApp.Net*.
    >
    > 1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an.
    > 1. Wählen Sie **Alle Ressourcen** und dann **Hinzufügen** aus.
    > 1. Suchen Sie nach **Clouddienst**. Wählen Sie **Erstellen** aus.
    > 1. Geben Sie im Feld **DNS-Name** das gewünschte Präfix ein, z.B. *WallaceFalls*. Auf der Benutzeroberfläche wird angezeigt, ob der Domänenname verfügbar ist oder bereits von einem anderen Dienst verwendet wird.
    >
    > Verwenden Sie diesen Vorgang nicht, um den Dienst im Portal zu erstellen, sondern nur, um die Verfügbarkeit des Namens zu überprüfen.

- Die Azure-**Region** für diese Bereitstellung.  

- Wenn Sie in Configuration Manager, Version 1810 oder früher, weiterhin die **klassische Dienstbereitstellung** von Azure verwenden müssen, gelten folgende Anforderungen:  

    > [!Important]  
    > Klassische Dienstbereitstellungen in Azure sind ab Version 1810 in Configuration Manager veraltet. Verwenden Sie Azure Resource Manager-Bereitstellungen für den Cloudverteilungspunkt. Weitere Informationen finden Sie unter [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > Ab Configuration Manager Version 1902 ist Azure Resource Manager der einzige Mechanismus zur Bereitstellung neuer Instanzen des Cloudverteilungspunkts.<!-- 3605704 -->

    - Azure-**Abonnement-ID**  

    - Ein als CER- und PFX-Datei exportiertes Azure-**Verwaltungszertifikat**. Das CER-Verwaltungszertifikat muss von einem Administrator für das Azure-Abonnement im [Azure-Portal](https://portal.azure.com) dem Abonnement hinzugefügt werden.  

### <a name="branchcache"></a>BranchCache

Wenn Sie einen Cloudverteilungspunkt für die Verwendung von Windows-BranchCache aktivieren möchten, installieren Sie das BranchCache-Feature auf dem Standortserver.<!-- SCCMDocs-pr#4054 -->

- Wenn der Standortserver über eine lokale Standortsystemrolle für den Verteilungspunkt verfügt, konfigurieren Sie die Option in den Eigenschaften dieser Rolle, um **BranchCache zu aktivieren und zu konfigurieren**. Weitere Informationen finden Sie unter [Konfigurieren eines Verteilungspunkts](install-and-configure-distribution-points.md#bkmk_config-general).

- Wenn der Standortserver nicht über eine Verteilungspunktrolle verfügt, installieren Sie das BranchCache-Feature in Windows. Weitere Informationen finden Sie unter [Installieren des BranchCache-Features](/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Wenn Sie Inhalte bereits an einen Cloudverteilungspunkt verteilt haben und dann das BranchCache-Feature aktivieren möchten, müssen Sie das Feature vorher installieren. Verteilen Sie den Inhalt anschließend an den Cloudverteilungspunkt.

> [!NOTE]  
> Wenn Sie über mehr als einen Cloudverteilungspunkt verfügen, müssen Sie in Configuration Manager, Version 1810 und früher die Passphrase für den BranchCache-Schlüssel manuell festlegen. Weitere Informationen finden Sie unter [Microsoft-Support KB 4458143](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a> Einrichten  

Führen Sie dieses Verfahren für den Standort durch, um diesen Cloudverteilungspunkt gemäß Ihrem [Entwurf](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology) zu hosten.  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie **Cloudverteilungspunkte** aus. Klicken Sie im Menüband auf **Cloudverteilungspunkt erstellen**.  

2. Konfigurieren Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Cloudverteilungspunkten folgende Einstellungen:  

    1. Geben Sie zunächst die **Azure-Umgebung** an.  

    2. Verwenden Sie ab Version 1806 die **Azure Resource Manager-Bereitstellung** als Bereitstellungsmethode. Dies ist die *empfohlene Vorgehensweise*. Klicken Sie auf **Anmelden**, um sich mit dem Administratorkonto eines Azure-Abonnements zu authentifizieren. Der Assistent füllt die verbleibenden Felder automatisch aus den Informationen auf, die im Rahmen der Voraussetzungen für die Azure AD-Integration gespeichert wurden. Wenn Sie mehrere Abonnements besitzen, wählen Sie die **Abonnement-ID** des Abonnements aus, das Sie verwenden möchten.  

    > [!Note]  
    > Klassische Dienstbereitstellungen in Azure sind ab Version 1810 in Configuration Manager veraltet.
    >
    > Wenn Sie eine klassische Dienstbereitstellung verwenden müssen, wählen Sie diese Option auf dieser Seite aus. Geben Sie zuerst Ihre Azure-**Abonnement-ID** ein. Klicken Sie anschließend auf **Durchsuchen**, und wählen Sie die PFX-Datei für das Azure-Verwaltungszertifikat aus.  

3. Wählen Sie **Weiter** aus. Warten Sie, bis der Standort die Verbindung mit Azure getestet hat.  

4. Geben Sie auf der Seite **Einstellungen** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**:  

    - **Region:** Wählen Sie die Azure-Region aus, in der Sie den Cloudverteilungspunkt erstellen möchten.  

    - **Ressourcengruppe** (nur Azure Resource Manager-Bereitstellungsmethode)  

        - **Vorhandene verwenden:** Wählen Sie in der Dropdownliste eine vorhandene Ressourcengruppe aus.  

        - **Neue erstellen:** Geben Sie den Namen der neuen Ressourcengruppe ein, die Sie in Ihrem Azure-Abonnement erstellen möchten.  

    - **Primärer Standort:** Wählen Sie den primären Standort für die Verteilung von Inhalten an diesen Verteilungspunkt aus.

    - **Zertifikatdatei:** Klicken Sie auf **Durchsuchen**, und wählen Sie die PFX-Datei für das Serverauthentifizierungszertifikat dieses Cloudverteilungspunkts aus. Mit dem allgemeinen Namen dieses Zertifikats werden die erforderlichen Felder **Dienst-FQDN** und **Dienstname** aufgefüllt.  

        > [!NOTE]  
        > Vom Serverauthentifizierungszertifikat des Cloudverteilungspunkts werden Platzhalter unterstützt. Wenn Sie ein Platzhalterzertifikat verwenden, ersetzen Sie das Sternchen (`*`) im Feld **Dienst-FQDN** durch den gewünschten Hostnamen für den Dienst.  

5. Richten Sie auf der Seite **Warnungen** Speicher- und Übertragungsquoten ein, und geben Sie an, bei welchem Prozentsatz dieser Quoten von Configuration Manager Warnungen generiert werden sollen. Klicken Sie dann auf **Weiter**.  

6. Schließen Sie den Assistenten ab.  

### <a name="monitor-installation"></a>Überwachen der Installation  

Am Standort wird mit der Erstellung eines neuen gehosteten Diensts für den Cloudverteilungspunkt begonnen. Überwachen Sie den Installationsfortschritt des Cloudverteilungspunkts in der Configuration Manager-Konsole, nachdem Sie den Assistenten geschlossen haben. Überwachen Sie außerdem die Datei **CloudMgr.log** auf dem primären Standortserver. Überwachen Sie ggf. die Bereitstellung des Clouddiensts im Azure-Portal.  

> [!NOTE]  
> Die Bereitstellung eines neuen Verteilungspunkts in Azure kann bis zu 30 Minuten dauern. Bis zur Bereitstellung des Speicherkontos wird die folgende Meldung in der Datei **CloudMgr.log** wiederholt angezeigt:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Nach der Bereitstellung des Speicherkontos wird der Dienst erstellt und konfiguriert.  

### <a name="verify-installation"></a>Überprüfen der Installation

Prüfen Sie mithilfe der folgenden Verfahren, ob die Installation des Cloudverteilungspunkts abgeschlossen ist:  

- Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Cloudverteilungspunkte** aus. Suchen Sie in der Liste nach dem neuen Cloudverteilungspunkt. In der Spalte „Status“ sollte **Bereit** angezeigt werden.  

- Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Systemstatus**, und wählen Sie den Knoten **Komponentenstatus** aus. Zeigen Sie alle Meldungen aus der Komponente **SMS_CLOUD_SERVICES_MANAGER** an, und suchen Sie nach der Statusmeldungs-ID **9409**.  

- Wechseln Sie ggf. zum Azure-Portal. Unter **Bereitstellung** wird für den Cloudverteilungspunkt der Status **Bereit** angezeigt.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> Konfigurieren von DNS  

Damit Clients den Cloudverteilungspunkt verwenden können, muss auf diesen Clients der Name des Cloudverteilungspunkts in eine IP-Adresse aufgelöst werden können, die von Azure verwaltet wird. Dabei wird der **Dienst-FQDN** des Cloudverteilungspunkts vom Verwaltungspunkt bereitgestellt. Der Cloudverteilungspunkt ist in Azure als **Dienstname** vorhanden. Prüfen Sie diese Werte auf der Registerkarte **Einstellungen** in den Eigenschaften des Cloudverteilungspunkts.

> [!Note]  
> Der Knoten **Cloudverteilungspunkte** in der Konsole enthält eine Spalte mit dem Namen **Dienstname**, die jedoch den Wert für den **Dienst-FQDN** enthält. Öffnen Sie **Eigenschaften** für den Cloudverteilungspunkt, und wechseln Sie zur Registerkarte **Einstellungen**, um beide Werte anzuzeigen.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Der allgemeine Name des Zertifikats sollte Ihren Domänennamen enthalten. Diesen Namen benötigen Sie, wenn Sie ein Zertifikat von einem öffentlichen Anbieter erwerben. Er wird empfohlen, wenn Sie dieses Zertifikat über Ihre PKI ausstellen. Beispiel: `WallaceFalls.contoso.com`. Wenn Sie dieses Zertifikat im Assistenten zum Erstellen von Cloudverteilungspunkten angeben, wird für die Eigenschaft **Dienst-FQDN** (`WallaceFalls.contoso.com`) der allgemeine Name angegeben. Der **Dienstname** übernimmt den Hostnamen (`WallaceFalls`) und hängt ihn an den Azure-Domänennamen `cloudapp.net` an. In diesem Szenario müssen Clients den **Dienst-FQDN** (`WallaceFalls.contoso.com`) Ihrer Domäne in den Azure-**Dienstnamen** (`WallaceFalls.cloudapp.net`) auflösen. Erstellen Sie zum Zuordnen dieser Namen einen CNAME-Alias.

### <a name="create-cname-alias"></a>Erstellen eines CNAME-Alias

Erstellen Sie einen CNAME-Eintrag für den öffentlichen, mit dem Internet verbundenen DNS-Server Ihrer Organisation. Mit diesem Eintrag wird ein Alias für die Eigenschaft **Dienst-FQDN** des Cloudverteilungspunkts, den Clients erhalten, erstellt und dem Azure-**Dienstnamen** zugeordnet. Erstellen Sie beispielsweise einen neuen CNAME-Eintrag für `WallaceFalls.contoso.com`, und ordnen Sie ihn `WallaceFalls.cloudapp.net` zu.  

### <a name="client-name-resolution-process"></a>Auflösung von Clientnamen

Das folgende Verfahren zeigt, wie ein Client den Namen des Cloudverteilungspunkts auflöst:  

1. Der Client erhält den **Dienst-FQDN** des Cloudverteilungspunkts in der Liste der Inhaltsquellen. Beispiel: `WallaceFalls.contoso.com`.  

2. DNS wird abgefragt. Dadurch wird der Dienst-FQDN mit dem CNAME-Alias in den Azure-**Dienstnamen** aufgelöst. Beispiel: `WallaceFalls.cloudapp.net`.  

3. DNS wird erneut abgefragt. Dadurch wird der Azure-Dienstname in die öffentliche Azure-IP-Adresse aufgelöst.  

4. Der Client verwendet diese IP-Adresse für die Kommunikation mit dem Cloudverteilungspunkt.  

5. Der Cloudverteilungspunkt übergibt das Serverauthentifizierungszertifikat an den Client. Der Client verwendet die Vertrauenskette des Zertifikats zur Überprüfung.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> Einrichten eines Standortserverproxys  

Der primäre Standortserver, der den Cloudverteilungspunkt verwaltet, muss mit Azure kommunizieren. Wenn Ihre Organisation zur Steuerung des Internetzugriffs einen Proxyserver verwendet, konfigurieren Sie den primären Standortserver so, dass er diesen Proxy verwendet.  

Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> Verteilen von Inhalten und Konfigurieren von Clients

Verteilen Sie Inhalte an den Cloudverteilungspunkt so wie an jeden anderen lokalen Verteilungspunkt. Der Cloudverteilungspunkt ist nur in der Liste der Inhaltsorte enthalten, wenn der Verwaltungspunkt über den von Clients angeforderten Inhalt verfügt. Weitere Informationen finden Sie unter [Bereitstellen und Verwalten von Inhalt](deploy-and-manage-content.md).

Verwalten Sie einen Cloudverteilungspunkt so wie jeden anderen lokalen Verteilungspunkt. Zu diesen Aktionen gehört die Zuweisung zu einer Verteilungspunktgruppe und die Verwaltung von Inhaltspaketen. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](install-and-configure-distribution-points.md).

Clientstandardeinstellungen ermöglichen Clients automatisch die Verwendung von Cloudverteilungspunkten. Steuern Sie den Zugriff auf alle Cloudverteilungspunkte in Ihrer Hierarchie über folgende Einstellungen:  

- Ändern Sie in der Gruppe **Cloudeinstellungen** die Einstellung **Zugriff auf Cloudverteilungspunkt zulassen**.  

    - Diese Einstellung ist standardmäßig auf **Ja** festgelegt.  

    - Ändern Sie diese Einstellung für Benutzer und Geräte, und stellen Sie sie bereit.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> Verwalten und Überwachen  

Überwachen Sie den Inhalt, den Sie an einen Cloudverteilungspunkt verteilen, so wie bei der Verteilung an jeden anderen lokalen Verteilungspunkt. Weitere Informationen finden Sie unter [Überwachen von Inhalt](monitor-content-you-have-distributed.md).

Wenn Sie die Liste der Cloudverteilungspunkte in der Konsole aufrufen, können Sie der Liste zusätzliche Spalten hinzufügen. In der Spalte **Data egress** (Datenausgang) wird die Datenmenge angezeigt, die Clients in den letzten 30 Tagen vom Dienst heruntergeladen haben.<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a> Warnungen  

Configuration Manager überprüft den Azure-Dienst regelmäßig. Wenn der Dienst nicht aktiv ist oder wenn Abonnement- oder Zertifikatsprobleme vorliegen, wird von Configuration Manager eine Warnung ausgelöst.

Konfigurieren Sie Schwellenwerte für die Menge an Daten, die Sie auf einem Verteilungspunkt speichern möchten, sowie für die Menge an Daten, die Clients von einem Verteilungspunkt herunterladen. Verwenden Sie für diese Schwellenwerte Warnungen, die Ihnen bei der Entscheidung helfen, wann Sie den Clouddienst beenden oder löschen sollen, sowie beim Anpassen des Inhalts, den Sie auf dem Cloudverteilungspunkt speichern, oder der Einstellung, welche Clients den Dienst nutzen dürfen.

- **Schwellenwert für die Speicherwarnung:** Durch einen Schwellenwert für die Speicherwarnung wird eine Obergrenze für die Menge an Daten oder Inhalten festgelegt, die Sie auf dem Cloudverteilungspunkt speichern möchten. Standardmäßig beträgt dieser Schwellenwert 2.000 GB. Configuration Manager kann Warnungen und kritische Warnungen generieren, wenn der verbleibende freie Speicherplatz den von Ihnen angegebenen Stand erreicht. Standardmäßig werden diese Warnungen bei 50 % und 90 % des Schwellenwerts ausgelöst.  

- **Monatlicher Schwellenwert für die Übertragungswarnung:** Ein Schwellenwert für die Übertragungswarnung hilft Ihnen bei der Überwachung der Menge an Inhalten, die innerhalb von 30 Tagen vom Verteilungspunkt an Clients übertragen werden. Standardmäßig beträgt dieser Schwellenwert 10.000 GB. Am Standort werden Warnungen und kritische Warnungen ausgelöst, wenn bei Übertragungen die von Ihnen definierten Werte erreicht werden. Standardmäßig werden diese Warnungen bei 50 % und 90 % des Schwellenwerts ausgelöst.  

    > [!IMPORTANT]  
    > Configuration Manager überwacht die Übertragung von Daten, beendet die Datenübertragung jedoch nicht, wenn sie den angegebenen Übertragungswarnschwellenwert überschreitet.  

Geben Sie bei der Installation für jeden Cloudverteilungspunkt Schwellenwerte an, oder verwenden Sie die Registerkarte **Warnungen** in den Eigenschaften des Cloudverteilungspunkts.  

> [!NOTE]  
> Warnungen für einen Cloudverteilungspunkt hängen von den Nutzungsstatistiken aus Azure ab. Es kann bis zu 24 Stunden dauern, bis sie verfügbar sind. Weitere Informationen zu Storage Analytics für Azure finden Sie unter [Storage Analytics](/rest/api/storageservices/storage-analytics).  

Der primäre Standort, der den Cloudverteilungspunkt überwacht, lädt stündlich Transaktionsdaten von Azure herunter. Diese Transaktionsdaten werden in der Datei `CloudDP-<ServiceName>.log` auf dem Standortserver gespeichert. Configuration Manager wertet dann diese Informationen anhand der Speicher- und Übertragungskontingente für die einzelnen Cloudverteilungspunkte aus. Wenn die Datenübertragung das für Warnungen oder kritische Warnungen angegebene Volumen erreicht oder überschreitet, generiert Configuration Manager die entsprechende Warnung.  

> [!WARNING]  
> Da die Informationen zu Datenübertragungen am Standort stündlich von Azure heruntergeladen werden, kann die Nutzung eine Warnung oder einen kritischen Schwellenwert überschreiten, bevor Configuration Manager auf die Daten zugreifen und eine Warnung ausgeben kann.  


## <a name="modify"></a><a name="bkmk_modify"></a> Änderung

Zeigen Sie detaillierte Informationen zum Verteilungspunkt im Arbeitsbereich **Verwaltung** im Knoten **Cloudverteilungspunkte** unter **Clouddienste** auf der Configuration Manager-Konsole an. Wählen Sie einen Verteilungspunkt aus, und klicken Sie auf **Eigenschaften**, um weitere Details anzuzeigen.  

Wenn Sie die Eigenschaften eines Cloudverteilungspunkts bearbeiten, enthalten die folgenden Registerkarten bearbeitbare Einstellungen:  

#### <a name="settings"></a>Einstellung

- **Beschreibung**  

- **Zertifikatdatei**: Stellen Sie vor Ablauf des Serverauthentifizierungszertifikats ein neues Zertifikat mit demselben allgemeinen Namen aus. Fügen Sie das neue Zertifikat anschließend hier hinzu, damit es vom Dienst verwendet werden kann. Wenn das Zertifikat abläuft, vertrauen Clients dem Dienst nicht und verwenden ihn nicht.  

#### <a name="alerts"></a>Warnungen

Passen Sie die Datenschwellenwerte für die Speicherwarnung und für die monatliche Übertragungswarnung an.  

#### <a name="content"></a>Content

Verwalten Sie den Inhalt wie bei einem lokalen Verteilungspunkt.  

### <a name="redeploy-the-service"></a>Erneutes Bereitstellen des Diensts

Bei wichtigeren Änderungen, wie z.B. den folgenden Konfigurationen, muss der Dienst erneut bereitgestellt werden:

- Klassische Bereitstellungsmethode in Azure Resource Manager
- Abonnement
- Dienstname
- Für öffentliche PKI privat
- Azure-Region

Wenn bei der klassischen Bereitstellungsmethode ein Cloudverteilungspunkt vorhandenen ist, müssen Sie ab Version 1806 zur Verwendung der Azure Resource Manager-Bereitstellungsmethode einen neuen Cloudverteilungspunkt bereitstellen. Es stehen zwei Optionen zur Verfügung:

- Wenn Sie den gleichen Dienstnamen wiederverwenden möchten:  

    1. Löschen Sie zunächst den klassischen Cloudverteilungspunkt. Wenn kein weiterer Cloudverteilungspunkt vorhanden ist, können Clients möglicherweise keinen Inhalt abrufen.  

    2. Erstellen Sie mithilfe einer Resource Manager-Bereitstellung einen neuen Cloudverteilungspunkt. Verwenden Sie dasselbe CMG-Serverauthentifizierungszertifikat wieder.  

    3. Verteilen Sie den erforderlichen Inhalt des Softwarepakets an den neuen Cloudverteilungspunkt.  

- Wenn Sie einen neuen Dienstnamen verwenden möchten:  

    1. Erstellen Sie mithilfe einer Resource Manager-Bereitstellung einen neuen Cloudverteilungspunkt. Verwenden Sie ein neues CMG-Serverauthentifizierungszertifikat.  

    2. Verteilen Sie den erforderlichen Inhalt des Softwarepakets an den neuen Cloudverteilungspunkt.  

    3. Löschen Sie den klassischen Cloudverteilungspunkt.

> [!Tip]  
> So ermitteln Sie das aktuelle Bereitstellungsmodell eines Cloudverteilungspunkts:<!--SCCMDocs issue #611-->  
>
> 1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Cloudverteilungspunkte** aus.  
> 2. Fügen Sie der Listenansicht das Attribut **Bereitstellungsmodell** als Spalte hinzu. Für eine Resource Manager-Bereitstellung ist dieses Attribut **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Clouddienst nach Bedarf starten oder beenden

In der Configuration Manager-Konsole können Sie einen Cloudverteilungspunkt jederzeit beenden. Dadurch werden Clients mit sofortiger Wirkung daran gehindert, zusätzliche Inhalte vom Dienst herunterzuladen. Starten Sie den Clouddienst über die Configuration Manager-Konsole neu, um den Zugriff für die Clients wiederherzustellen. Beenden Sie einen Clouddienst beispielsweise, wenn er einen Datenschwellenwert erreicht.  

Wenn Sie einen Cloudverteilungspunkt beenden, wird der Inhalt im Speicherkonto nicht gelöscht. Darüber hinaus wird auch nicht verhindert, dass der Standortserver weiteren Inhalt an den Cloudverteilungspunkt überträgt. Der Verwaltungspunkt gibt den Cloudverteilungspunkt weiterhin als gültige Inhaltsquelle zurück.

Gehen Sie wie folgt vor, um einen Cloudverteilungspunkt zu beenden:  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Cloud Services**, und wählen Sie den Knoten **Cloudverteilungspunkte** aus.  

2. Wählen Sie den Cloudverteilungspunkt aus. Klicken Sie im Menüband auf **Dienst beenden**, um den Clouddienst in Azure zu beenden.  

3. Klicken Sie auf **Dienst starten**, um den Cloudverteilungspunkt neu zu starten.  

### <a name="delete-a-cloud-distribution-point"></a>Löschen eines Cloudverteilungspunkts

Zur Deinstallation eines Cloudverteilungspunkts wählen Sie diesen in der Configuration Manager-Konsole und anschließend **Löschen** aus.  

Wenn Sie einen Cloudverteilungspunkt aus einer Hierarchie löschen, dann entfernt Configuration Manager den Inhalt aus dem Clouddienst in Azure.

Durch das manuelle Entfernen von Komponenten in Azure wird das System in einen inkonsistenten Zustand versetzt. Dieser Zustand hinterlässt verwaiste Informationen. Zudem kann es zu unerwartetem Verhalten kommen.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> Erweiterte Problembehandlung

Wenn Sie zur Behandlung von Problemen mit dem Cloudverteilungspunkt Diagnoseprotokolle von den Azure-VMs sammeln müssen, verwenden Sie das folgende PowerShell-Beispiel, um die Diagnoseerweiterung des Diensts für das Abonnement zu aktivieren:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

Hierbei handelt es sich um eine **diagnostics.wadcfgx**-Beispieldatei, auf die in der Variablen **public_config** im obigen PowerShell-Skript verwiesen wird. Weitere Informationen finden Sie unter [Konfigurationsschema der Azure-Diagnoseerweiterung](/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```