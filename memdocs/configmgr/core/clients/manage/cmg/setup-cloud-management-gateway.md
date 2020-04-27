---
title: Einrichten von Cloud Management Gateway
titleSuffix: Configuration Manager
description: Mithilfe dieses Prozesses können Sie Schritt für Schritt den Cloud Management Gateway-Dienst einrichten.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 36d256e674a0fe973eca4bc692a244af034d5cc1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076763"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Einrichten des Cloudverwaltungsgateways für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Prozess umfasst die erforderlichen Schritte für die Einrichtung eines Cloud Management Gateway-Diensts.

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../../servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="before-you-begin"></a>Vorbereitung

Lesen Sie zunächst den Artikel [Planen von Cloud Management Gateway](plan-cloud-management-gateway.md). Mithilfe dieses Artikels können Sie Ihren CMG-Entwurf bestimmen.

Verwenden Sie die folgende Prüfliste, um sicherzustellen, dass Sie über die erforderlichen Informationen und Voraussetzungen für die Erstellung eines CMG verfügen:  

- Die zu verwendende Azure-Umgebung. Beispiel: die Azure Public Cloud oder die Azure US Government Cloud.  

- Abhängig von Ihrem Entwurf benötigen Sie mindestens ein Zertifikat für das CMG. Weitere Informationen finden Sie unter [Zertifikate für Cloud Management Gateway](certificates-for-cloud-management-gateway.md).  

- Für eine [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager)-Bereitstellung des CMG müssen folgende Voraussetzungen erfüllt sein:  

    - Integration in [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) für die **Cloudverwaltung**. Die Azure Active Directory-Benutzerermittlung ist nicht erforderlich.  

    - Die Ressourcenanbieter **Microsoft.ClassicCompute** & **Microsoft.Storage** müssen im Azure-Abonnement registriert werden. Weitere Informationen finden Sie unter [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - Ein Abonnementadministrator muss sich anmelden.  

- Ein global eindeutiger Name für den Dienst. Dieser Name stammt aus dem [CMG-Serverauthentifizierungszertifikat](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Wenn Sie CMG als Cloudverteilungspunkt aktivieren, muss der gleiche global eindeutige Name des ausgewählten CMG-Diensts auch als global eindeutiger Name des Speicherkontos verfügbar sein. Dieser Name stammt aus dem [CMG-Serverauthentifizierungszertifikat](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- Die Azure-Region für diese CMG-Bereitstellung.  

- Die Anzahl der VM-Instanzen für die Skalierung und Redundanz.  

- Wenn Sie in Configuration Manager, Version 1810 oder früher, weiterhin die klassische Dienstbereitstellung von Azure verwenden müssen, gelten folgende Anforderungen:  

    > [!Important]  
    > Klassische Dienstbereitstellungen in Azure sind ab Version 1810 in Configuration Manager veraltet. Verwenden Sie Azure Resource Manager-Bereitstellungen für das Cloudverwaltungsgateway. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > Ab Configuration Manager Version 1902 ist Azure Resource Manager der einzige Mechanismus zur Bereitstellung neuer Instanzen des Cloudverwaltungsgateways.<!-- 3605704 -->

    - Azure-Abonnement-ID  

    - Azure-Verwaltungszertifikat  


## <a name="set-up-a-cmg"></a>Einrichten eines CMG

Führen Sie diese Prozedur am Standort der obersten Ebene aus. Bei diesem Standort handelt es sich entweder um einen eigenständigen primären Standort oder um den Standort der zentralen Verwaltung.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie **Cloudverwaltungsgateway** aus.  

2. Klicken Sie im Menüband auf **Cloudverwaltungsgateway erstellen**.  

3. Wählen Sie auf der Seite „Allgemein“ des Assistenten die Option **Anmelden** aus. Authentifizieren Sie sich mit dem Administratorkonto eines Azure-Abonnements. Der Assistent füllt die verbleibenden Felder automatisch aus den Informationen auf, die im Rahmen der Voraussetzungen für die Azure AD-Integration gespeichert wurden. Wenn Sie mehrere Abonnements besitzen, wählen Sie die **Abonnement-ID** des Abonnements aus, das Sie verwenden möchten.

    > [!Note]  
    > Klassische Dienstbereitstellungen in Azure sind ab Version 1810 in Configuration Manager veraltet. Wählen Sie in Version 1902 und früher **Azure Resource Manager-Bereitstellung** als CMG-Bereitstellungsmethode aus.
    >
    > Wenn Sie eine klassische Dienstbereitstellung verwenden müssen, wählen Sie diese Option auf dieser Seite aus. Geben Sie zuerst Ihre Azure-**Abonnement-ID** ein. Klicken Sie anschließend auf **Durchsuchen**, und wählen Sie die PFX-Datei für das Azure-Verwaltungszertifikat aus.

4. Geben Sie die **Azure-Umgebung** für dieses CMG an. Die Optionen in der Dropdownliste können je nach Bereitstellungsmethode variieren.  

5. Wählen Sie **Weiter** aus. Warten Sie, bis der Standort die Verbindung mit Azure getestet hat.  

6. Klicken Sie auf der Seite „Einstellungen“ des Assistenten zunächst auf **Durchsuchen**, und wählen Sie anschließend die PFX-Datei für das CMG-Serverauthentifizierungszertifikat aus. Mit dem Namen dieses Zertifikats werden die erforderlichen Felder **Dienst-FQDN** und **Dienstname** aufgefüllt.  

   > [!NOTE]  
   > Das CMG-Serverauthentifizierungszertifikat unterstützt Platzhalter. Wenn Sie ein Platzhalterzertifikat verwenden, ersetzen Sie das Sternchen (`*`) in dem Feld **Dienst-FQDN** durch den gewünschten Hostnamen für das CMG.<!--491233-->  

7. Klicken Sie auf die Dropdownliste **Region**, um die Azure-Region für dieses CMG auszuwählen.  

8. Wählen Sie eine Option für **Ressourcengruppe** aus.
   1. Wenn Sie **Vorhandene verwenden** auswählen, wählen Sie anschließend aus der Dropdownliste eine vorhandene Ressourcengruppe aus. Die ausgewählte Ressourcengruppe muss bereits in der Region vorhanden sein, die Sie in Schritt 7 ausgewählt haben. Wenn Sie eine vorhandene Ressourcengruppe auswählen und sich diese in einer anderen als der zuvor ausgewählten Region befindet, kann CMG nicht bereitgestellt werden.
   2. Wenn Sie **Neu erstellen** auswählen, geben Sie anschließend den Namen der neuen Ressourcengruppe ein.

9. Geben Sie in das Feld **VM-Instanz** die Anzahl der virtuellen Computer für diesen Dienst ein. Der Standardwert ist 1, er kann jedoch auf bis zu 16 virtuelle Computer pro CMG hochskaliert werden.  

10. Klicken Sie auf **Zertifikate**, um ein vom Client als vertrauenswürdig eingestuftes Stammzertifikat hinzuzufügen. Fügen Sie in der Vertrauenskette alle Zertifikate hinzu.  

    > [!Note]  
    > Wenn Sie ein CMG erstellen, müssen Sie ab Version 1806 auf der Seite „Einstellungen“ kein vertrauenswürdiges Stammzertifikat mehr angeben. Dieses Zertifikat ist nicht erforderlich, wenn Sie Azure Active Directory (Azure AD) für die Clientauthentifizierung verwenden. Früher war es im Assistenten erforderlich. Wenn Sie PKI-Clientauthentifizierungszertifikate verwenden, müssen Sie weiterhin ein vertrauenswürdiges Stammzertifikat für das Cloudverwaltungsgateway hinzufügen.<!--SCCMDocs-pr issue #2872-->  
    >
    > In Version 1902 und früher können Sie nur zwei vertrauenswürdige Stammzertifizierungsstellen und vier Zwischenzertifizierungsstellen (untergeordnete Zertifizierungsstellen) hinzufügen.<!-- SCCMDocs-pr#4022 -->

11. Die Option **Clientzertifikatsperre überprüfen** wird vom Assistenten standardmäßig aktiviert. Eine Zertifikatsperrliste (Certificate Revocation List, CRL) muss öffentlich veröffentlicht werden, damit diese Überprüfung durchgeführt werden kann. Weitere Informationen finden Sie unter [Veröffentlichen der Zertifikatsperrungsliste](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. Ab Version 1906 können Sie **TLS 1.2 erzwingen**. Diese Einstellung betrifft nur die Azure Cloud-Dienst-VM. Sie gilt nicht für lokale Configuration Manager-Standortserver oder -Clients. Weitere Informationen zu TLS 1.2 finden Sie unter [Aktivieren von TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. Ab Version 1806 wird die folgende Option standardmäßig vom Assistenten aktiviert: **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen**. Jetzt kann ein CMG auch als Inhalt für Clients dienen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs.  

14. Wählen Sie **Weiter** aus.  

15. Zur Überwachung des Cloudverwaltungsgateway-Datenverkehrs mit einem Schwellenwert von 14 Tagen müssen Sie das Kontrollkästchen für Schwellenwertwarnungen aktivieren. Legen Sie dann die Schwellenwerte und Prozentsätze für die verschiedenen Warnungsebenen fest. Klicken Sie auf **Weiter**, wenn Sie fertig sind.  

16. Überprüfen Sie die Einstellungen, und klicken Sie auf **Weiter**. Configuration Manager beginnt mit der Einrichtung des Diensts. Nach dem Schließen des Assistenten dauert es 5 bis 15 Minuten, bis der Dienst vollständig in Azure bereitgestellt ist. Überprüfen Sie die Spalte **Status** für das neue CMG, um zu bestimmen, wann der Dienst bereit ist.  

    > [!Note]  
    > Verwenden Sie **CloudMgr.log** und **CMGSetup.log** für die Problembehandlung von CMG-Bereitstellungen. Weitere Informationen finden Sie in den [Protokolldateien](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Konfigurieren des primären Standorts für die Clientzertifikatauthentifizierung

Führen Sie die hier beschriebene Prozedur zum Konfigurieren der einzelnen primären Standorte durch, wenn Sie für die Authentifizierung von Clients beim CMG [Clientauthentifizierungszertifikate](certificates-for-cloud-management-gateway.md#bkmk_clientauth) verwenden.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus.  

2. Wählen Sie den primären Standort, dem Ihre internetbasierten Clients zugewiesen sind, und wählen Sie **Eigenschaften** aus.  

3. Wechseln Sie zur Registerkarte **Clientcomputerkommunikation** im Eigenschaftenblatt für den primären Standort, und aktivieren Sie **Use PKI client certificate (client authentication) when available** (PKI-Clientzertifikat (Clientauthentifizierung) verwenden, sofern verfügbar).  

    > [!Note]
    > Ab Version 1906 heißt diese Registerkarte **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->  

4. Wenn Sie keine Zertifikatsperrliste veröffentlichen, deaktivieren Sie die Option **Die Zertifikatsperrliste für Standortsysteme wird von Clients überprüft**.  


## <a name="add-the-cmg-connection-point"></a>Hinzufügen des CMG-Verbindungspunkts

Bei dem CMG-Verbindungspunkt handelt es sich um die Standortsystemrolle für die Kommunikation mit dem CMG. Befolgen Sie die allgemeinen Anweisungen zum [Installieren von Standortsystemrollen](../../../servers/deploy/configure/install-site-system-roles.md), um den CMG-Verbindungspunkt hinzuzufügen. Wählen Sie auf der Seite „Systemrollenauswahl“ des Assistenten zum Hinzufügen von Standortsystemrollen den Eintrag **Verbindungspunkt für Cloudverwaltungsgateway** aus. Wählen Sie anschließend den **Namen des Cloudverwaltungsgateways** aus, mit dem dieser Server eine Verbindung herstellt. Der Assistent zeigt die Region für das ausgewählte CMG an.

> [!Important]
> Der CMG-Verbindungspunkt muss in einigen Szenarios über ein [Clientauthentifizierungszertifikat](certificates-for-cloud-management-gateway.md#bkmk_clientauth) verfügen.

Verwenden Sie **CMGService.log** und **SMS_Cloud_ProxyConnector.log** für die Problembehandlung der CMG-Dienstintegrität. Weitere Informationen finden Sie in den [Protokolldateien](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Konfigurieren von Rollen mit Clientkontakt für den CMG-Datenverkehr

Konfigurieren Sie die Verwaltungspunkt- und Softwareupdatepunkt-Standortsysteme, um CMG-Datenverkehr zu akzeptieren. Führen Sie diese Prozedur für alle Verwaltungspunkte und Softwareupdatepunkte am primären Standort durch, die Dienste für internetbasierte Clients bereitstellen.  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Server und Standortsystemrollen** aus. Klicken Sie auf dem Menüband auf der Registerkarte „Start“ in der Gruppe „Ansicht“ auf **Server mit Rolle**. Wählen Sie anschließend **Verwaltungspunkt** aus der Liste aus.  

2. Wählen Sie den Standortsystemserver aus, den Sie für den CMG-Datenverkehr konfigurieren möchten. Wählen Sie im Detailbereich die Rolle **Verwaltungspunkt** aus, und klicken Sie anschließend im Menüband auf **Eigenschaften**.  

3. Aktivieren Sie auf dem Eigenschaftenblatt „Verwaltungspunkt“ unter „Clientverbindungen“ das Kontrollkästchen neben **Allow Configuration Manager cloud management gateway traffic** (Datenverkehr über Cloud Management Gateway von Configuration Manager zulassen).

    Abhängig von Ihrem CMG-Entwurf und der Configuration Manager-Version müssen Sie möglicherweise die Option **HTTPS** aktivieren. Weitere Informationen finden Sie unter [Verwaltungspunkt für HTTPS aktivieren](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Klicken Sie auf **OK**, um das Fenster „Eigenschaften des Verwaltungspunkts“ zu schließen.  

Wiederholen Sie diese Schritte ggf. für weitere Verwaltungspunkte und für Softwareupdatepunkte.


## <a name="configure-boundary-groups"></a>Konfigurieren von Begrenzungsgruppen

<!--3640932-->
Ab Version 1902 können Sie einer Begrenzungsgruppe ein CMG zuordnen. Mit dieser Konfiguration können Clients für die Clientkommunikation entsprechend der Begrenzungsgruppenbeziehungen den Standardwert für das CMG verwenden oder Fallbacks dafür zulassen.

Weitere Informationen finden Sie unter [Konfigurieren von Begrenzungsgruppen](../../../servers/deploy/configure/boundary-groups.md).

Wenn Sie [eine Begrenzungsgruppe erstellen oder konfigurieren](../../../servers/deploy/configure/boundary-group-procedures.md), fügen Sie auf der Registerkarte **Verweise** ein Cloudverwaltungsgateway hinzu. Durch diese Aktion wird das CMG dieser Begrenzungsgruppe zugeordnet.


## <a name="configure-clients-for-cmg"></a>Konfigurieren von Clients für das CMG

Sobald das CMG und die Standortsystemrollen ausgeführt werden, empfangen die Clients bei der nächsten Anforderung des Speicherorts automatisch den Speicherort des CMG-Diensts. Clients müssen sich im Intranet befinden, um den Speicherort des CMG-Diensts empfangen zu können, sofern Sie nicht [Windows 10-Clients mithilfe von Azure AD für die Authentifizierung installieren und zuweisen](../../deploy/deploy-clients-cmg-azure.md). Der Abfragezyklus für Standortanfragen beträgt 24 Stunden. Wenn Sie nicht auf die normal geplante Standortanfragen warten möchten, können Sie sie erzwingen, indem Sie den SMS-Agent-Hostdienst (ccmexec.exe) auf dem Computer neustarten.  

> [!Note]
> Standardmäßig empfangen alle Clients die CMG-Richtlinie. Sie können dieses Verhalten mit der Clienteinstellung [Enable clients to use a cloud management gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway) (Clients die Verwendung eines Cloud Management Gateway-Diensts ermöglichen) steuern.

Der Configuration Manager-Client bestimmt automatisch, ob er sich im Intranet oder im Internet befindet. Wenn der Client einen Domänencontroller oder einen lokalen Verwaltungspunkt kontaktieren kann, wird der Verbindungstyp auf **Derzeit Intranet** festgelegt. Andernfalls wechselt er zu **Derzeit Internet** und verwendet den Speicherort des CMG-Diensts für die Kommunikation mit dem Standort.

>[!NOTE]
> Sie können erzwingen, dass der Client immer das CMG verwendet, und zwar unabhängig davon, ob er sich im Intranet oder im Internet befindet. Diese Konfiguration eignet sich für Testzwecke oder für die Clients, bei denen Sie die Verwendung des CMG immer erzwingen möchten. Legen Sie folgenden Registrierungsschlüssel für den Client fest:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Sie können diese Einstellung auch während der Clientinstallation mithilfe der Eigenschaft [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) angeben.
>
> Diese Einstellung wird immer angewendet, auch wenn der Client per Roaming an einen Standort wechselt, an dem Begrenzungsgruppenkonfigurationen andernfalls lokale Ressourcen nutzen würden.


Öffnen Sie eine Windows PowerShell-Eingabeaufforderung als Administrator auf dem Clientcomputer, und führen Sie den folgenden Befehl aus, um zu überprüfen, ob Clients über die Richtlinie verfügen, in der das CMG angegeben ist: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Dieser Befehl zeigt alle internetbasierten Verwaltungspunkte an, die dem Client bekannt sind. Das CMG ist technisch gesehen kein internetbasierter Verwaltungspunkt, wird Clients jedoch als solcher angezeigt.

> [!Note]  
> Verwenden Sie **CMGHttpHandler.log**, **CMGService.log** und **SMS_Cloud_ProxyConnector.log** für die Problembehandlung des CMG-Clientdatenverkehrs. Weitere Informationen finden Sie in den [Protokolldateien](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="modify-a-cmg"></a>Ändern eines CMG

Nach der Erstellung eines CMG können Sie einige der zugehörigen Einstellungen ändern. Wählen Sie das CMG in der Configuration Manager-Konsole aus, und klicken Sie auf **Eigenschaften**. Konfigurieren Sie Einstellungen auf den folgenden Registerkarten:  

#### <a name="general"></a>Allgemein

- **Azure-Verwaltungszertifikat**: Ändern des Azure-Verwaltungszertifikats für das CMG. Diese Option ist nützlich, wenn das Zertifikat vor Ablauf aktualisiert wird.  

#### <a name="settings"></a>Einstellung

- **Zertifikatsdatei**: Ändern des Serverauthentifizierungszertifikats für das CMG. Diese Option ist nützlich, wenn das Zertifikat vor Ablauf aktualisiert wird.  

- **VM-Instanz**: Ändern der Anzahl der virtuellen Computer, die der Dienst in Azure verwendet. Mit dieser Einstellung können Sie den Dienst basierend auf Nutzung und Kostenüberlegungen dynamisch hoch- oder herunterskalieren.  

- **Zertifikate**: Hinzufügen oder Entfernen vertrauenswürdiger Stamm- oder Zwischenzertifizierungsstellenzertifikate Diese Option ist nützlich, wenn neue Zertifizierungsstellen hinzugefügt werden oder abgelaufene Zertifikate zurückgezogen werden.  

- **Clientzertifikatsperre überprüfen**: Wenn Sie diese Einstellung bei der Erstellung des CMG nicht ursprünglich aktiviert haben, können Sie dies tun, sobald Sie die Zertifikatsperrliste veröffentlicht haben. Weitere Informationen finden Sie unter [Veröffentlichen der Zertifikatsperrungsliste](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen**: Ab Version 1806 ist diese neue Option standardmäßig aktiviert. Jetzt kann ein CMG auch als Inhalt für Clients dienen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs.<!--1358651-->  

#### <a name="alerts"></a>Warnungen

Konfigurieren Sie die Warnungen nach der Erstellung des CMG jederzeit neu.


### <a name="redeploy-the-service"></a>Erneutes Bereitstellen des Diensts

Bei wichtigeren Änderungen, wie z.B. den folgenden Konfigurationen, muss der Dienst erneut bereitgestellt werden:

- Klassische Bereitstellungsmethode in Azure Resource Manager
- Abonnement
- Dienstname
- Für öffentliche PKI privat
- Region

Bewahren Sie immer mindestens ein aktives CMG für internetbasierte Clients auf, um die aktualisierte Richtlinie empfangen zu können. Internetbasierte Clients können nicht mit einem entfernten CMG kommunizieren. Client erfahren erst dann von einer neuen Richtlinie, wenn sie ins Intranet wechseln. Bei der Erstellung einer zweiten CMG-Instanz zum Löschen der ersten Instanz müssen Sie auch einen weiteren CMG-Verbindungspunkt erstellen.

Clients aktualisieren eine Richtlinie standardmäßig alle 24 Stunden. Daher sollten Sie mindestens einen Tag nach Erstellung eines neuen CMG warten, bis Sie das alte CMG löschen. Wenn Clients deaktiviert oder ohne Internetverbindung sind, müssen Sie möglicherweise etwas länger warten.

Wenn Sie über eine vorhandene CMG-Instanz der klassischen Bereitstellungsmethode verfügen, müssen Sie für die Verwendung der Azure Resource Manager-Bereitstellungsmethode eine neue CMG-Instanz bereitstellen.<!--509753--> Es stehen zwei Optionen zur Verfügung:  

- Wenn Sie den gleichen Dienstnamen wiederverwenden möchten:  

    1. Löschen Sie zunächst das klassische CMG, und berücksichtigen Sie dabei die Anweisung, dass immer mindestens ein aktives CMG für internetbasierte Clients vorhanden sein sollte.  

    2. Erstellen Sie mithilfe einer Resource Manager-Bereitstellung ein neues CMG. Verwenden Sie dasselbe CMG-Serverauthentifizierungszertifikat wieder.  

    3. Konfigurieren Sie den CMG-Verbindungspunkt neu, um die neue CMG-Instanz verwenden zu können.  

- Wenn Sie einen neuen Dienstnamen verwenden möchten:  

    1. Erstellen Sie mithilfe einer Resource Manager-Bereitstellung ein neues CMG. Verwenden Sie ein neues CMG-Serverauthentifizierungszertifikat.  

    2. Erstellen Sie einen neuen CMG-Verbindungspunkt, und verbinden Sie diesen mit dem neuen CMG.  

    3. Warten Sie mindestens einen Tag, bis internetbasierte Clients eine Richtlinie zum neuen CMG empfangen.  

    4. Löschen Sie das klassische CMG.  

> [!Tip]  
> So bestimmen Sie das aktuelle Bereitstellungsmodell einer CMG-Instanz:<!--SCCMDocs issue #611-->  
>
> 1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Cloudverwaltungsgateway** aus.  
> 2. Wählen Sie die CMG-Instanz aus.  
> 3. Suchen Sie im Detailbereich am unteren Rand des Fensters nach dem Attribut **Bereitstellungsmodell**. Für eine Resource Manager-Bereitstellung ist dieses Attribut **Azure Resource Manager**. Das alte Bereitstellungsmodell mit Azure-Verwaltungszertifikat wird als **Azure Service Manager** angezeigt.
>
> Sie können der Listenansicht das **Bereitstellungsmodell**-Attribut auch als Spalte hinzufügen.  

### <a name="modifications-in-the-azure-portal"></a>Änderungen im Azure-Portal

Ändern Sie das CMG nur über die Configuration Manager-Konsole. Änderungen an dem Dienst oder zugrunde liegenden VM können nicht direkt in Azure vorgenommen werden. Änderungen gehen möglicherweise ohne Ankündigung verloren. Wie einen PaaS kann der Dienst auch die VM jederzeit neu erstellen. Diese Neuerstellungen können für die Wartung von Back-End-Hardware oder für die Anwendung von Updates für das VM-Betriebssystem erfolgen.

### <a name="delete-the-service"></a>Löschen des Diensts

Wenn Sie das CMG löschen müssen, machen Sie auch dies über die Configuration Manager-Konsole. Durch das manuelle Entfernen von Komponenten in Azure wird das System in einen inkonsistenten Zustand versetzt. Dieser Zustand hinterlässt verwaiste Informationen. Zudem kann es zu unerwartetem Verhalten kommen.


## <a name="next-steps"></a>Nächste Schritte

- [Überwachen von Clients für das Cloudverwaltungsgateway](monitor-clients-cloud-management-gateway.md)
- [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](cloud-management-gateway-faq.md)
