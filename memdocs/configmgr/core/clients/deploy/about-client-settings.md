---
title: Clienteinstellungen
titleSuffix: Configuration Manager
description: Informationen zu Standardeinstellungen und benutzerdefinierten Einstellungen zur Steuerung von Clientverhalten
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 21e837d5d97c42f095159a87e015f181c5e53419
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347167"
---
# <a name="about-client-settings-in-configuration-manager"></a>Informationen zu Clienteinstellungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwalten Sie alle Clienteinstellungen in der Configuration Manager-Konsole über den Knoten **Clienteinstellungen** im Arbeitsbereich **Verwaltung**. Mit Configuration Manager wird ein Satz Standardeinstellungen geliefert. Wenn Sie die Clientstandardeinstellungen verändern, werden diese Einstellungen auf alle Clients in der Hierarchie angewendet. Sie können auch benutzerdefinierte Clienteinstellungen konfigurieren, die die standardmäßigen Clienteinstellungen überschreiben, wenn sie Sammlungen zugewiesen werden. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](configure-client-settings.md).

In den folgenden Abschnitten werden diese Einstellungen und Optionen ausführlicher beschrieben.  


## <a name="background-intelligent-transfer-service-bits"></a>Intelligenter Hintergrundübertragungsdienst (BITS – Background Intelligent Transfer Service)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Maximale Netzwerkbandbreite für BITS-Übertragungen im Hintergrund begrenzen

Wenn diese Option auf **Ja** festgelegt ist, verwenden Clients die BITS-Bandbreiteneinschränkung. Sie müssen diese Einstellung aktivieren, um andere Einstellungen in dieser Gruppe zu konfigurieren.

### <a name="throttling-window-start-time"></a>Beginn des Einschränkungszeitfensters

Geben Sie die lokale Startzeit für das BITS-Einschränkungszeitfenster an.  

### <a name="throttling-window-end-time"></a>Ende des Einschränkungszeitfensters

Geben Sie die lokale Endzeit für das BITS-Einschränkungszeitfenster an. Entspricht die Endzeit dem Wert von **Beginn des Einschränkungszeitfensters**, ist die BITS-Einschränkung immer aktiviert.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Maximale Übertragungsrate während des Einschränkungszeitfensters (KBit/s)

Geben Sie die maximale Übertragungsrate an, die den Clients während des Zeitfensters zur Verfügung steht.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>BITS-Downloads außerhalb des Einschränkungszeitfensters zulassen

Ermöglichen Sie Clients das Verwenden von separaten BITS-Einstellungen außerhalb des angegebenen Zeitfensters.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Maximale Übertragungsrate außerhalb des Einschränkungszeitfensters (KBit/s)

Geben Sie die maximale Übertragungsrate an, die Clients außerhalb des Zeitfensters der BITS-Bandbreiteneinschränkung verwenden können.  



## <a name="client-cache-settings"></a>Einstellungen des Clientcaches

### <a name="configure-branchcache"></a>BranchCache konfigurieren

Richten Sie den Clientcomputer für [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
) ein. Um die BranchCache-Zwischenspeicherung auf dem Client zuzulassen, legen Sie **BranchCache aktivieren** auf **Ja** fest.

- **BranchCache aktivieren**: aktiviert BranchCache auf Clientcomputern.

- **Maximale BranchCache-Cachegröße (Prozentsatz des Datenträgers)** : Der Prozentsatz des Datenträgers, den BranchCache verwenden kann.

> [!TIP]
> Wenn Sie **BranchCache konfigurieren** auf **Nein** festlegen, konfiguriert Configuration Manager keine BranchCache-Einstellungen.
>
> Um BranchCache zu deaktivieren, legen Sie **BranchCache konfigurieren** auf **Ja** und **BranchCache aktivieren** auf **Nein** fest.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Clientcachegröße konfigurieren

Der Konfigurations-Manager-Clientcache auf Windows-Computern speichert temporäre Dateien, die zum Installieren von Anwendungen und Programmen verwendet werden. Wenn diese Option auf **Nein** festgelegt ist, beträgt die Standardgröße 5.120 MB.

Wenn Sie **Ja** auswählen, geben Sie Folgendes an:

- **Maximale Cachegröße (MB)**
- **Maximale Cachegröße (Prozentsatz des Datenträgers)** : Die Cachegröße kann auf die maximale Größe in Megabyte (MB) oder auf den Prozentsatz des Datenträgers erweitert werden, je nachdem, welcher Wert kleiner ist.

### <a name="enable-as-peer-cache-source"></a>Als Peercachequelle aktivieren

> [!Note]  
> In Version 1902 und früher hieß diese Einstellung **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren**. Das Verhalten der Einstellung hat sich nicht geändert.

Aktiviert den [Peercache](../../plan-design/hierarchy/client-peer-cache.md) für Konfigurations-Manager-Clients. Klicken Sie auf **Ja**, und geben Sie dann den Port ein, über den der Client mit dem Peercomputer kommuniziert.

- **Port für erste Netzwerkübertragung** (Standard: 8004): Configuration Manager verwendet diesen Port in Windows PE oder dem gesamten Windows-Betriebssystem. Die Tasksequenzengine in Windows PE sendet die Übertragung, um Inhaltsorte abzurufen, bevor sie die Tasksequenz startet.<!--SCCMDocs issue 910-->

- **Port für den Download der Inhalte vom Peer** (Standard: TCP 8003): Configuration Manager konfiguriert die Regeln der Windows-Firewall automatisch so, dass dieser Datenverkehr zugelassen wird. Bei Verwendung einer anderen Firewall müssen Sie die Regeln manuell konfigurieren, um diesen Datenverkehr zuzulassen.  

    Weitere Informationen finden Sie unter [Für Verbindungen verwendete Ports](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Mindestdauer vor dem Entfernen von Inhalten aus dem Cache (Minuten)

<!--4485509-->
Ab Version 1906 können Sie für den Configuration Manager-Client festlegen, wie lange Inhalte mindestens im Cache aufbewahrt werden sollen. Diese Clienteinstellung definiert die minimale Zeitspanne, die der Configuration Manager-Agent warten sollte, bevor er Inhalt aus dem Cache entfernt, wenn mehr Speicherplatz benötigt wird.

Standardmäßig ist dieser Wert auf 1.440 Minuten (24 Stunden) festgelegt.
Der Maximalwert für diese Einstellung ist 10.080 Minuten (eine Woche).

Diese Einstellung bietet Ihnen mehr Kontrolle über den Clientcache auf verschiedenen Gerätetypen. Sie können den Wert auf Clients mit kleinen Festplatten verringern, die keine vorhandenen Inhalte aufbewahren müssen, ehe eine weitere Bereitstellung erfolgt.


## <a name="client-policy"></a>Clientrichtlinie  

### <a name="client-policy-polling-interval-minutes"></a>Clientrichtlinien-Abrufintervall (Minuten)

Gibt an, wie häufig die Clientrichtlinie von folgenden Konfigurations-Manager-Clients heruntergeladen werden soll:

- Windows-Computer (z. B. Desktops, Server, Laptops)  
- Von Configuration Manager registrierte mobile Geräte  
- Macintosh-Computer  
- Computer, auf denen Linux oder UNIX ausgeführt wird  

Dieser Wert ist standardmäßig auf 60 Minuten festgelegt. Die Reduzierung dieses Wertes führt dazu, dass Clients den Standort häufiger abfragen. Bei vielen Clients kann dieses Verhalten einen negativen Einfluss auf die Standortleistung haben. Der [Leitfaden für Größe und Skalierung](../../plan-design/configs/size-and-scale-numbers.md) basiert auf dem Standardwert. Die Erhöhung dieses Wertes führt dazu, dass Clients den Standort seltener abfragen. Das Herunterladen und Verarbeiten von Änderungen an Clientrichtlinien, einschließlich neuer Bereitstellungen, durch Clients dauert länger.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Benutzerrichtlinie auf Clients aktivieren

Wenn Sie diese Option auf **Ja** festlegen und die [Benutzerermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) verwenden, erhalten die Clients die Anwendungen und Programme, die dem angemeldeten Benutzer zugeordnet sind.  

Wenn diese Einstellung auf **Nein** festgelegt ist, erhalten Benutzer erforderliche Anwendungen nicht, die Sie für Benutzer bereitstellen. Benutzer erhalten ebenfalls keine anderen Verwaltungstasks in den Benutzerrichtlinien.  

Diese Einstellung gilt für Benutzer, deren Computer mit dem Intranet und dem Internet verbunden sind. Die Einstellung muss **Ja** lauten, wenn Sie auch Benutzerrichtlinien im Internet aktivieren möchten.  

> [!Note]  
> Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Sie können keine neuen Anwendungskatalogrollen installieren.
>
> Wenn Sie immer noch den Anwendungskatalog verwenden, empfängt dieser die Liste der für den Benutzer verfügbaren Software vom Standortserver. Daher muss diese Einstellung nicht auf **Ja** festgelegt werden, damit Benutzer Anwendungen im Anwendungskatalog anzeigen und von dort anfordern können. Wenn diese Einstellung auf **Nein** festgelegt ist, können Benutzer die im Anwendungskatalog angezeigten Anwendungen nicht installieren.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Benutzerrichtlinienanforderungen von Internetclients aktivieren

Legen Sie diese Option auf **Ja** fest, damit Benutzer die Benutzerrichtlinie auf internetbasierten Computern erhalten. Zudem gelten folgende Anforderungen:  

- Client und Standort wurden für die [internetbasierte Clientverwaltung](../manage/plan-internet-based-client-management.md) oder ein [Cloudverwaltungsgateway](../manage/cmg/plan-cloud-management-gateway.md) konfiguriert.  

- Die Einstellung **Benutzerrichtlinie auf Clients aktivieren** wurde auf **Ja** festgelegt.  

- Der Benutzer wird vom internetbasierten Verwaltungspunkt erfolgreich mithilfe der Windows-Authentifizierung (Kerberos oder NTLM) authentifiziert. Weitere Informationen finden Sie unter [Considerations for client communications from the internet (Überlegungen zur Clientkommunikation über das Internet)](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- Das Cloudverwaltungsgateway authentifiziert den Benutzer erfolgreich mithilfe von Azure Active Directory. Weitere Informationen finden Sie unter [Deploy user-available applications on Azure AD-joined devices (Bereitstellen von für Benutzer verfügbare Anwendungen auf in Azure AD eingebundenen Geräten)](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

Wenn Sie diese Option auf **Nein** festlegen oder eine der vorherigen Anforderungen nicht erfüllt ist, erhält ein internetbasierter Computer nur Computerrichtlinien. In diesem Fall können Benutzer weiterhin Anwendungen über einen internetbasierten Anwendungskatalog anzeigen, anfordern und installieren. Wenn diese Einstellung auf **Nein**, aber **Benutzerrichtlinie auf Clients aktivieren** auf **Ja** festgelegt ist, empfangen Benutzer keine Benutzerrichtlinien, bis der Computer mit dem Intranet verbunden ist.  

> [!NOTE]  
> Bei der Verwaltung internetbasierter Clients sind für Anforderungen von Benutzern zur Genehmigung von Anwendungen keine Benutzerrichtlinien und keine Benutzerauthentifizierung erforderlich. Cloud Management Gateway unterstützt keine Anforderungen zur Genehmigung von Anwendungen.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Aktivieren der Benutzerrichtlinie für mehrere Benutzersitzungen

<!--4737447-->

*Gilt für Version 1910*

Diese Einstellung ist standardmäßig deaktiviert. Auch wenn Sie Benutzerrichtlinien aktivieren, werden diese ab Version 1906 vom Client standardmäßig auf Geräten deaktiviert, die mehrere gleichzeitige aktive Benutzersitzungen zulassen. Beispiele hierfür sind Terminalserver oder mehrere Windows 10 Enterprise-Sitzungen in [Windows Virtual Desktop](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

Der Client deaktiviert eine Benutzerrichtlinie nur, wenn er diesen Gerätetyp während einer neuen Installation erkennt. Für einen vorhandenen Client dieses Typs, den Sie auf Version 1906 oder höher aktualisieren, bleibt das vorherige Verhalten bestehen. Bei einem bestehenden Gerät wird die Benutzerrichtlinieneinstellung auch dann konfiguriert, wenn erkannt wird, dass das Gerät mehrere Benutzersitzungen ermöglicht.

Aktivieren Sie diese Clienteinstellung, wenn Sie in diesem Szenario eine Benutzerrichtlinie benötigen und mögliche Auswirkungen auf die Leistung akzeptieren.


## <a name="cloud-services"></a>Clouddienste

### <a name="allow-access-to-cloud-distribution-point"></a>Zugriff auf Cloudverteilungspunkt zulassen

Legen Sie diese Option auf **Ja** fest, damit Clients Inhalte von einem Cloudverteilungspunkt abrufen können. Diese Einstellung erfordert keine internetbasierten Geräte.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registrieren Sie neue, in die Domäne eingebundene Windows 10-Geräte automatisch bei Azure Active Directory.

Wenn Sie Azure Active Directory so konfigurieren, dass eine hybride Einbindung unterstützt wird, konfiguriert Configuration Manager Windows 10-Geräte für diese Funktionalität. Weitere Informationen finden Sie unter [Konfigurieren von in Azure Active Directory eingebundenen Hybridgeräten](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Ermöglichen Sie Clients die Verwendung eines Cloudverwaltungsgateways.

Standardmäßig verwenden alle Clients für Internetroaming jedes verfügbare [Cloudverwaltungsgateway](../manage/cmg/plan-cloud-management-gateway.md). Sie müssen diese Einstellung beispielsweise auf **Nein** festlegen, wenn Sie die Nutzung des Diensts während eines Pilotprojekts oder aus Kostengründen einschränken möchten.



## <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

### <a name="enable-compliance-evaluation-on-clients"></a>Konformitätsauswertung auf Clients aktivieren

Legen Sie diese Option auf **Ja** fest, um die anderen Einstellungen in dieser Gruppe zu konfigurieren.

### <a name="schedule-compliance-evaluation"></a>Konformitätsauswertung planen

Wählen Sie **Zeitplan** aus, um den Standardzeitplan für Bereitstellungen von Konfigurationsbaselines zu erstellen. Dieser Wert kann im Dialogfeld **Konfigurationsbaseline bereitstellen** für jede Baseline konfiguriert werden.  

### <a name="enable-user-data-and-profiles"></a>Benutzerdaten und Profile aktivieren

Wählen Sie **Ja** aus, wenn Sie Konfigurationselemente für [Benutzerdaten und Profile](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) bereitstellen möchten.



## <a name="computer-agent"></a>Computer-Agent  

### <a name="user-notifications-for-required-deployments"></a>Benutzerbenachrichtigungen für erforderliche Bereitstellungen

Weitere Informationen zu den folgenden drei Einstellungen finden Sie unter [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_notify):

- **Bereitstellungsstichtag in mehr als 24 Stunden, Erinnerung alle (Stunden)**
- **Bereitstellungsstichtag in weniger als 24 Stunden, Erinnerung alle (Stunden)**
- **Bereitstellungsstichtag in weniger als 1 Stunde, Erinnerung alle (Minuten)**

### <a name="default-application-catalog-website-point"></a>Websitepunkt des Standardanwendungskatalogs

> [!Important]  
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Diese Einstellung wird von Configuration Manager verwendet, um Benutzer über das Softwarecenter mit dem Anwendungskatalog zu verbinden. Wählen Sie **Website festlegen** aus, um einen Server anzugeben, der den Anwendungskatalog-Websitepunkt hostet. Geben Sie den NetBIOS-Namen oder den vollqualifizierten Domänennamen des Servers ein, und legen Sie die automatische Erkennung oder eine URL für benutzerdefinierte Bereitstellungen fest. In der Regel stellt die automatische Erkennung die beste Wahl dar.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Standardanwendungskatalog-Website zur Internet Explorer-Zone der vertrauenswürdigen Sites hinzufügen

> [!Important]  
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Wenn diese Option auf **Ja** festgelegt wurde, fügt der Client die aktuelle URL der Website des Anwendungskatalogs automatisch zur Zone der vertrauenswürdigen Websites von Internet Explorer hinzugefügt.  

Durch diese Einstellung wird sichergestellt, dass die Internet Explorer-Einstellung für den geschützten Modus nicht aktiviert wird. Ist der geschützte Modus aktiviert, können vom Configuration Manager-Client möglicherweise keine Anwendungen aus dem Anwendungskatalog installiert werden. Die Zone der vertrauenswürdigen Sites unterstützt standardmäßig auch die Benutzeranmeldung beim Anwendungskatalog, für die die Windows-Authentifizierung erforderlich ist.  

Wenn Sie diese Option bei **Nein** belassen, können Configuration Manager-Clients möglicherweise keine Anwendungen aus dem Anwendungskatalog installieren. Eine alternative Methode besteht im Konfigurieren dieser Internet Explorer-Eigenschaften für die URL des Anwendungskatalogs, die Clients verwenden, in einer anderen Zone.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen

> [!Important]  
> Silverlight wird vom Client nicht automatisch installiert.
>
> Ab Version 1806 wird die **Silverlight-Benutzeroberfläche** für den Anwendungskatalog-Websitepunkt nicht mehr unterstützt. Benutzer sollten das neue Softwarecenter verwenden. Weitere Informationen finden Sie unter [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Diese Einstellung muss auf **Ja** festgelegt sein, damit der Anwendungskatalog von Benutzern verwendet werden kann.  

Eine Änderung dieser Einstellung wird wirksam, wenn Benutzer ihren Browser das nächste Mal laden oder das gegenwärtig geöffnete Browserfenster aktualisieren.  

Weitere Informationen zu dieser Einstellung finden Sie unter [Zertifikate für Microsoft Silverlight 5 und für den Anwendungskatalog erforderlicher Modus mit höherer Vertrauensstellung](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Im Softwarecenter angezeigter Organisationsname

Geben Sie den Namen ein, den Benutzer im Softwarecenter sehen. Diese Branding-Informationen helfen den Benutzern, diese Anwendung als vertrauenswürdige Quelle zu identifizieren. Weitere Informationen zur Wichtigkeit dieser Einstellung finden Sie unter [Branding im Softwarecenter](../../../apps/plan-design/plan-for-software-center.md#branding-software-center).  

### <a name="use-new-software-center"></a>Verwenden des neuen Softwarecenters

Der Standardwert für diese Einstellung ist **Ja**.

Wenn Sie diese Einstellung auf **Ja** festlegen, verwenden alle Clientcomputer das Softwarecenter. Im Softwarecenter werden Software, Softwareupdates und Tasksequenzen angezeigt, die Sie für Benutzer oder Geräte bereitstellen.

### <a name="enable-communication-with-health-attestation-service"></a>Aktivieren Sie die Kommunikation mit dem Integritätsnachweisdienst.

Legen Sie diese Option auf **Ja** fest, damit Windows 10-Geräte den [Integritätsnachweis](../../servers/manage/health-attestation.md) verwenden. Wenn Sie diese Einstellung aktivieren, kann folgende Einstellung ebenfalls konfiguriert werden.

### <a name="use-on-premises-health-attestation-service"></a>Lokalen Integritätsnachweisdienst verwenden

Legen Sie diese Option auf **Ja** fest, damit Geräte einen lokalen Dienst verwenden. Legen Sie die Einstellung auf **Nein** fest, damit Geräte den cloudbasierten Microsoft-Dienst verwenden.  

### <a name="install-permissions"></a>Berechtigungen installieren

Konfigurieren Sie, wie Benutzer Software, Softwareupdates und Tasksequenzen installieren können:  

- **Alle Benutzer:** Benutzer mit einer beliebigen Berechtigung, außer „Gast“.  

- **Nur Administratoren:** Benutzer müssen zu den lokalen Administratoren gehören.  

- **Nur Administratoren und primäre Benutzer:** Benutzer müssen zu den lokalen Administratoren gehören oder primäre Benutzer des Computers sein.  

- **Keine Benutzer:** Keiner der Benutzer, die sich bei einem Clientcomputer angemeldet haben, kann Software, Softwareupdates und Tasksequenzen installieren. Erforderliche Bereitstellungen für den Computer werden immer am Stichtag installiert. Benutzer können Software nicht über das Softwarecenter installieren.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Bitlocker-PIN-Eingabe bei Neustart anhalten

Wenn die Computer eine BitLocker-PIN-Eingabe erfordern, kann mit dieser Option die notwendige Eingabe einer PIN umgangen werden, wenn der Computer nach der Installation von Software neu gestartet wird.  

- **Immer:** Configuration Manager hält BitLocker nach der Installation von Software, für die ein Neustart erforderlich ist, vorübergehend an und startet den Computer neu. Diese Einstellung wird nur angewendet, wenn Configuration Manager den Computer neu startet. Wenn der Benutzer den Computer neu startet, ist es trotz dieser Einstellung weiterhin erforderlich, die BitLocker-PIN einzugeben. Die BitLocker-Anforderung zur Eingabe einer PIN wird nach dem Start von Windows wieder eingesetzt.

- **Nie:** BitLocker wird von Configuration Manager nach der Installation von Software, für die ein Neustart erforderlich ist, nicht angehalten. In diesem Fall kann die Softwareinstallation erst abgeschlossen werden, wenn der Benutzer die PIN eingibt, um den Standardstartvorgang abzuschließen und Windows zu laden.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Bereitstellung von Anwendungen und Softwareupdates wird von zusätzlicher Software verwaltet

Aktivieren Sie diese Option nur, wenn eine der folgenden Bedingungen zutrifft:  

- Sie verwenden eine Anbieterlösung, für die diese Einstellung aktiviert werden muss.  

- Sie verwalten Client-Agent-Benachrichtigungen und die Installation von Anwendungen und Softwareupdates mit dem Configuration Manager SDK (Software Development Kit).  

> [!WARNING]  
> - Wenn Sie diese Option auswählen, obwohl keine dieser Bedingungen erfüllt ist, installiert der Client keine Softwareupdates und keine erforderlichen Anwendungen. Durch diese Einstellung wird nicht verhindert, dass Benutzer verfügbare Software aus dem Softwarecenter installieren (dies gilt für Anwendungen, Pakete und Tasksequenzen).  
> -  Wenn Sie diese Einstellung aktivieren, werden auf Clients keine Popupbenachrichtigungen für neue oder erforderliche Software angezeigt. <!--6347668-->

### <a name="powershell-execution-policy"></a>PowerShell-Ausführungsrichtlinie

Konfigurieren Sie, wie Windows PowerShell-Skripts von Configuration Manager-Clients ausgeführt werden können. Sie können diese Skripts zur Erkennung von Konformitätseinstellungen in Konfigurationselementen einsetzen. Sie können die Skripts auch in einer Bereitstellung als Standardskript senden.  

- **Umgehen:** Die Windows PowerShell-Konfiguration auf dem Clientcomputer wird vom Konfigurations-Manager-Client umgangen, sodass nicht signierte Skripts ausgeführt werden können.  

- **Eingeschränkt:** Der Konfigurations-Manager-Client verwendet die aktuelle PowerShell-Konfiguration auf dem Clientcomputer. Diese Konfiguration bestimmt, ob nicht signierte Skripts ausgeführt werden können.  

- **Alle signiert:** Nur die von einem vertrauenswürdigen Herausgeber signierten Skripts werden vom Konfigurations-Manager-Client ausgeführt. Diese Einschränkung gilt unabhängig von der aktuellen PowerShell-Konfiguration auf dem Clientcomputer.  

Für diese Option ist mindestens Windows PowerShell 2.0 erforderlich. Der Standardwert ist **Alle Signiert**.  

> [!TIP]  
> Wenn nicht signierte Skripts wegen dieser Clienteinstellung nicht ausgeführt werden können, wird dieser Fehler von Configuration Manager wie folgt gemeldet:  
>
> - Der Arbeitsbereich **Überwachung** in der Konsole zeigt die Fehler-ID **0x87D00327** für den Bereitstellungsstatus an. Die Beschreibung **Das Skript wurde nicht signiert.** wird ebenfalls angezeigt.  
> - Berichte zeigen den Fehlertyp **Ermittlungsfehler** an. Berichte zeigen entweder den Fehlercode **0x87D00327** und die Beschreibung **Das Skript wurde nicht signiert.** oder den Fehlercode **0x87D00320** und die Beschreibung **Der Skripthost wurde noch nicht installiert.** an. Beispiel für einen Bericht: **Details zu Fehlern von Konfigurationselementen in einer Konfigurationsbaseline für eine Ressource**.  
> - Die Datei **DcmWmiProvider.log** zeigt die Meldung **Das Skript wurde nicht signiert. (Fehler: 87D00327; Quelle: CCM)** an.  

### <a name="show-notifications-for-new-deployments"></a>Benachrichtigung für neue Bereitstellungen anzeigen

Wählen Sie **Ja** aus, um eine Benachrichtigung für Bereitstellungen anzuzeigen, die seit weniger als einer Woche verfügbar sind. Diese Nachricht wird jedes Mal angezeigt, wenn der Client-Agent gestartet wird.

### <a name="disable-deadline-randomization"></a>Zufällige Stichtaganordnung deaktivieren

Nach dem Stichtag der Bereitstellung bestimmt diese Einstellung, ob der Client eine Aktivierungsverzögerung von bis zu zwei Stunden verwendet, um erforderliche Softwareupdates zu installieren. Die Aktivierungsverzögerung ist standardmäßig deaktiviert.  

Bei Szenarios für virtuelle Desktopinfrastrukturen (VDI) können durch diese Verzögerung die Prozessorauslastung und die Datenübertragung für einen Hostcomputer auf mehrere virtuelle Computer verteilt werden. Auch wenn Sie keine VDI verwenden, kann das gleichzeitige Installieren der gleichen Updates auf vielen Clients die CPU-Nutzung auf dem Standortserver in negativem Sinne steigern. Außerdem kann es durch dieses Verhalten zu einer Verlangsamung der Verteilungspunkte und einer erheblichen Verringerung der verfügbaren Netzwerkbandbreite kommen.  

Wenn Clients erforderliche Softwareupdates zum Stichtag der Bereitstellung ohne Verzögerung installieren müssen, legen Sie diese Einstellung auf **Ja** fest.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)

Wenn Sie den Benutzern mehr Zeit zum Installieren erforderlicher Anwendungs- oder Softwareupdatebereitstellungen nach der Frist gewähren möchten, legen Sie einen Wert für diese Option fest. Diese Toleranzperiode gilt für einen Computer, der für einen längeren Zeitraum ausgeschaltet ist, und für den der Benutzer viele Anwendungs- oder Updatebereitstellungen installieren muss. Diese Einstellung kann sehr nützlich sein, damit beispielsweise ein Benutzer, der aus dem Urlaub zurückkehrt, nicht lange warten muss, während der Client überfällige Anwendungsbereitstellungen installiert.

Legen Sie eine Karenzzeit von 0 bis 120 Stunden fest. Verwenden Sie diese Einstellung mit der Bereitstellungseigenschaft **Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen innerhalb der Karenzzeit verzögern, die in den Clienteinstellungen definiert ist**. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).

## <a name="computer-restart"></a>Computerneustart

Weitere Informationen zu diesen Einstellungen finden Sie unter [Benachrichtigungen zum Geräteneustart](device-restart-notifications.md).<!-- 7182335 -->

## <a name="delivery-optimization"></a>Übermittlungsoptimierung

<!-- 1324696 -->
Sie verwenden Configuration Manager-Begrenzungsgruppen, um die Inhaltsverteilung über Ihr gesamtes Unternehmensnetzwerk und Remotebüros hinweg zu definieren und zu regulieren. [Windows-Übermittlungsoptimierung](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) ist eine cloudbasierte Peer-zu-Peer-Technologie zum gemeinsamen Nutzen von Inhalten auf Windows 10-Geräten. Konfigurieren Sie die Übermittlungsoptimierung so, dass bei der Freigabe von Inhalten für Peers Ihre Begrenzungsgruppen verwendet werden.

> [!Note]
> - Die Übermittlungsoptimierung ist nur auf Windows 10-Clients verfügbar.
> - Der Internetzugriff auf den Clouddienst Übermittlungsoptimierung ist eine Anforderung für den Einsatz der Peer-zu-Peer-Funktionalität. Informationen zu den erforderlichen Internetendpunkten finden Sie unter [Häufig gestellte Fragen zur Übermittlungsoptimierung](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - Bei der Verwendung eines CMG zum Speichern von Inhalten werden die Inhalte für Updates für Drittanbietersoftware nicht auf Clients heruntergeladen, wenn die [Clienteinstellung](#allow-clients-to-download-delta-content-when-available) **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** aktiviert ist. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Verwenden von Configuration Manager-Begrenzungsgruppen zum Festlegen der Gruppen-ID für die Übermittlungsoptimierung

Klicken Sie auf **Ja**, um die Begrenzungsgruppen-ID als Gruppen-ID für die Übermittlungsoptimierung auf dem Client festzulegen. Wenn der Client mit dem Übermittlungsoptimierungs-Clouddienst kommuniziert, wird diese ID zum Ermitteln von Peers verwendet, auf denen sich die Inhalte befinden. Wenn Sie diese Einstellung aktivieren, wird auf Zielclients auch der Downloadmodus für die Übermittlungsoptimierung auf die Option „Gruppe (2)“ festgelegt.

> [!Note]
> Microsoft empfiehlt, dass der Client die Möglichkeit haben sollte, diese Einstellung über eine lokale Richtlinie anstelle einer Gruppenrichtlinie zu konfigurieren. So kann die Begrenzungsgruppen-ID als Gruppen-ID für die Übermittlungsoptimierung auf dem Client festgelegt werden. Weitere Informationen finden Sie unter [Übermittlungsoptimierung](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Ermöglichen der Verwendung von Microsoft Connected Cache-Servern für Inhaltsdownloads für die von Configuration Manager verwalteten Geräte

<!--3555764-->
Klicken Sie auf **Ja**, um Clients das Herunterladen von Inhalten von einem lokalen Verteilungspunkt zu gestatten, den Sie als Microsoft Connected Cache-Server aktivieren. Weitere Informationen finden Sie unter [Microsoft Connected Cache in Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> Zusätzlich zu den folgenden Informationen finden Sie weitere Details zur Verwendung der Endpoint Protection-Clienteinstellungen unter [Beispielszenario: Verwenden von Endpoint Protection zum Schutz von Computern vor Schadsoftware](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Verwalten des Endpoint Protection-Clients auf Clientcomputern

Wählen Sie **Ja** aus, wenn Sie vorhandene Endpoint Protection- und Windows Defender-Clients auf den Computern in Ihrer Hierarchie verwalten möchten.  

Wählen Sie diese Option aus, wenn der Endpoint Protection-Client bereits installiert ist und Sie ihn mit Configuration Manager verwalten möchten. Diese separate Installation umfasst einen skriptgesteuerten Prozess, der eine Anwendung oder ein Paket und ein Programm von Configuration Manager verwendet. Für Windows 10-Geräte muss der Endpoint Protection-Agent nicht installiert werden. Für diese Geräte muss jedoch weiterhin die Einstellung **Endpoint Protection-Client auf Clientcomputern verwalten** aktiviert sein. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Installieren des Endpoint Protection-Clients auf Clientcomputern

Wählen Sie **Ja** aus, um den Endpoint Protection-Client auf Clientcomputern zu installieren und zu aktivieren, auf denen der Client noch nicht ausgeführt wird. Für Windows 10-Clients muss der Endpoint Protection-Agent nicht installiert werden.  

> [!NOTE]  
> Wenn der Endpoint Protection-Client bereits installiert ist, wird dieser durch die Auswahl von **Nein** nicht deinstalliert. Legen Sie zum Deinstallieren des Endpoint Protection-Clients die Clienteinstellung **Endpoint Protection-Client auf Clientcomputern verwalten** auf **Nein** fest. Stellen Sie dann ein Paket und Programm zum Deinstallieren des Endpoint Protection-Clients bereit.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Endpoint Protection-Clientinstallation und Neustarts außerhalb der Wartungsfenster zulassen. Wartungsfenster müssen für die Clientinstallation mindestens 30 Minuten lang sein.

Legen Sie diese Option auf **Ja** fest, um typische Installationsverhaltensweisen mit Wartungsfenstern außer Kraft zu setzen. Diese Einstellung entspricht den geschäftlichen Anforderungen für die Priorität der Systemwartung aus Sicherheitsgründen.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Für Windows Embedded-Geräte mit Schreibfiltern Commit für Endpoint Protection-Clientinstallation ausführen (hierdurch werden Neustarts erforderlich)

Wählen Sie **Ja** aus, um den Schreibfilter auf dem Windows Embedded-Gerät zu deaktivieren und das Gerät neu zu starten. Hierdurch wird für die Installation auf dem Gerät ein Commit ausgeführt.  

Wenn Sie diese Einstellung auf **Nein** festlegen, führt der Client die Installation auf einer temporären Überlagerung durch, die bei einem Neustart des Geräts gelöscht wird. In diesem Szenario wird der Endpoint Protection-Client nicht vollständig installiert, bis eine andere Installation Änderungen an das Gerät committet. Dies ist die Standardkonfiguration.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Erforderliche Neustarts nach der Installation des Endpoint Protection-Clients unterdrücken

Wählen Sie **Ja** aus, um einen Computerneustart nach der Installation des Endpoint Protection-Clients zu unterdrücken.  

> [!IMPORTANT]  
> Wenn der Endpoint Protection-Client einen Computerneustart erfordert und diese Einstellung auf **Nein** festgelegt ist, startet der Computer unabhängig von den konfigurierten Wartungsfenstern neu.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Zulässiges Zeitintervall (Stunden), um das Benutzer einen für den Abschluss der Installation von Endpoint Protection erforderlichen Neustart verschieben können

Wenn ein Neustart nach der Installation eines Endpoint Protection-Clients erforderlich ist, gibt diese Einstellung an, um wie viele Stunden der Benutzer den erforderlichen Neustart verschieben kann. Für diese Einstellung muss die folgende Einstellung deaktiviert werden: **Erforderliche Neustarts nach der Installation des Endpoint Protection-Clients unterdrücken**.

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Alternative Quellen (wie z.B. Microsoft Windows Update, Microsoft Windows Server Update Services oder UNC-Freigaben) für das erste Definitionsupdate auf Clientcomputern deaktivieren

Wählen Sie **Ja** aus, wenn durch Configuration Manager nur das erste Definitionsupdate auf Clientcomputern installiert werden soll. Diese Einstellung kann hilfreich sein, um bei der ersten Installation des Definitionsupdates überflüssige Netzwerkverbindungen zu vermeiden und die Auslastung der Netzwerkbandbreite zu verringern.  



## <a name="enrollment"></a>Anmeldung

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Abrufintervall für Legacyclients mobiler Geräte

Wählen Sie **Intervall festlegen** aus, um die Zeitdauer in Minuten oder Stunden festzulegen, während der ältere mobile Geräte Richtlinien abrufen. Zu diesen Geräten zählen Plattformen wie Windows CE, macOS und Unix oder Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Abrufintervall für moderne Geräte (Minuten)

Geben Sie die Anzahl von Minuten ein, für die moderne Geräte Richtlinien abrufen. Diese Einstellung gilt für Windows 10-Geräte, die über die lokale Verwaltung mobiler Geräte verwaltet werden.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Benutzern die Registrierung von mobilen Geräten und Macintosh-Computern gestatten

Um die benutzerbasierte Registrierung älterer Geräte zu aktivieren, legen Sie diese Option auf **Ja** fest, und konfigurieren Sie die folgende Einstellung:

- **Registrierungsprofil**: Wählen Sie **Profil festlegen** aus, um ein Registrierungsprofil zu erstellen oder auszuwählen. Weitere Informationen finden Sie unter [Configure client settings for enrollment (Konfigurieren der Clienteinstellungen für die Registrierung)](deploy-clients-to-macs.md#configure-client-settings).

### <a name="allow-users-to-enroll-modern-devices"></a>Benutzern ermöglichen, moderne Geräte anzumelden

Um die benutzerbasierte Registrierung moderner Geräte zu aktivieren, legen Sie diese Option auf **Ja** fest, und konfigurieren Sie die folgende Einstellung:

- **Registrierungsprofil für modernes Gerät**: Wählen Sie **Profil festlegen** aus, um ein Registrierungsprofil zu erstellen oder auszuwählen. Weitere Informationen finden Sie unter [Erstellen Sie ein Registrierungsprofil, mit dem Benutzer moderne Geräte registrieren können](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Hardwareinventur  

### <a name="enable-hardware-inventory-on-clients"></a>Hardwareinventur auf Clients aktivieren

Diese Einstellung ist standardmäßig auf **Ja** festgelegt. Weitere Informationen finden Sie unter [Einführung in die Hardwareinventur](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Hardwareinventur-Zeitplan

Wählen Sie **Zeitplan** aus, um die Häufigkeit anzupassen, mit der Clients den Hardwareinventurzyklus ausführen. Standardmäßig erfolgt dieser Zyklus alle sieben Tage.

### <a name="maximum-random-delay-minutes"></a>Maximale zufällige Verzögerung (Minuten)

Geben Sie die maximale Anzahl von Minuten für den Konfigurations-Manager-Client an, um den Hardwareinventurzyklus abweichend vom definierten Zeitplan zufällig festzulegen. Durch diese zufällige Anordnung für alle Clients wird ein Lastenausgleich für die Verarbeitung der Inventur auf dem Standortserver unterstützt. Sie können jeden Wert zwischen 0 und 480 Minuten angeben. Standardmäßig ist dieser Wert auf 240 Minuten (4 Stunden) festgelegt.

### <a name="maximum-custom-mif-file-size-kb"></a>Maximale benutzerdefinierte MIF-Dateigröße (KB)

Geben Sie die maximale zulässige Größe einer einzelnen benutzerdefinierten MIF-Datei (Management Information Format) in Kilobyte (KB) an, die ein Client während eines Hardwareinventurzyklus sammelt. Der Hardwareinventur-Agent von Configuration Manager verarbeitet keine benutzerdefinierten MIF-Dateien, die diese Größe überschreiten. Sie können eine Größe von 1 bis 5.120 KB angeben. Standardmäßig ist diese Option auf 250 KB festgelegt. Diese Einstellung wirkt sich nicht auf die Größe der regulären Hardwareinventur-Datendatei aus.  

> [!NOTE]  
> Diese Einstellung ist nur in den Clientstandardeinstellungen verfügbar.  

### <a name="hardware-inventory-classes"></a>Hardwareinventurklassen

Wählen Sie **Klassen festlegen** aus, um die von Clients gesammelten Hardwareinformationen ohne manuelles Bearbeiten der Datei „sms_def.mof“ zu erweitern. Weitere Informationen finden Sie unter [Konfigurieren der Hardwareinventur](../manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>MIF-Dateien sammeln

Mit dieser Einstellung können Sie angeben, ob bei der Hardwareinventur MIF-Dateien von Configuration Manager-Clients gesammelt werden sollen.  

Damit eine MIF-Datei durch die Hardwareinventur gesammelt werden kann, muss sie sich am korrekten Speicherort auf dem Clientcomputer befinden. Die Dateien befinden sich standardmäßig in folgendem Pfad:  

- **IDMIF-Dateien** sollten sich im Ordner „Windows\System32\CCM\Inventory\Idmif“ befinden.

- **NOIDMIF-Dateien** sollten sich im Ordner „Windows\System32\CCM\Inventory\Noidmif“ befinden.

> [!NOTE]  
> Diese Einstellung ist nur in den Clientstandardeinstellungen verfügbar.



## <a name="metered-internet-connections"></a>Getaktete Internetverbindungen  

Legen Sie fest, wie Computer unter Windows 8 und höher getaktete Internetverbindungen verwenden, um mit Configuration Manager zu kommunizieren. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

> [!NOTE]  
> Die konfigurierte Clienteinstellung wird in folgenden Szenarios nicht angewendet:  
>
> - Wenn der Computer eine Roamingdatenverbindung verwendet, führt der Konfigurations-Manager-Client keine Tasks aus, bei denen Daten an Configuration Manager-Standorte übertragen werden müssen.  
> - Wenn die Eigenschaften der Windows-Netzwerkverbindung als nicht getaktet konfiguriert wurden, verhält sich der Configuration Manager-Client so wie bei einer nicht getakteten Verbindung und überträgt Daten an den Standort.  

### <a name="client-communication-on-metered-internet-connections"></a>Clientkommunikation über getaktete Internetverbindungen

Wählen Sie eine der folgenden Optionen für diese Einstellung aus:  

- **Zulassen:** Die gesamte Clientkommunikation kann über die getaktete Internetverbindung stattfinden, es sei denn, vom Clientgerät wird eine Roamingdatenverbindung verwendet.  

- **Grenzwert:** Nur die folgende Clientkommunikation ist über die getaktete Internetverbindung zulässig:  

    - Clientrichtlinienabruf  

    - An den Standort zu sendende Meldungen zum Clientzustand  

    - Softwareinstallationsanforderungen aus dem Softwarecenter  

    - Erforderliche Bereitstellungen (bei Erreichen des Installationsstichtags)  

    Wenn der Client das Datenübertragungslimit der getakteten Internetverbindung erreicht, versucht er nicht mehr, mit Configuration Manager-Standorten zu kommunizieren.  

- **Blockieren:** Der Konfigurations-Manager-Client versucht nicht, mit Configuration Manager-Standorten zu kommunizieren, wenn eine getaktete Internetverbindung verwendet wird. Dies ist die Standardoption.  

> [!IMPORTANT]  
> Der Client lässt Softwareinstallationen über das Softwarecenter unabhängig von den Einstellungen für die getaktete Internetverbindung immer zu. Wenn der Benutzer eine Softwareinstallation anfordert, während sich das Gerät in einem getakteten Netzwerk befindet, wird die Absicht des Benutzers vom Software Center berücksichtigt.<!-- MEMDocs#285 -->


## <a name="power-management"></a>Energieverwaltung  

### <a name="allow-power-management-of-devices"></a>Energieverwaltung von Geräten zulassen

Legen Sie diese Option auf **Ja** fest, um die Energieverwaltung für Clients zu aktivieren. Weitere Informationen finden Sie unter [Einführung in die Energieverwaltung](../manage/power/introduction-to-power-management.md).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Benutzern das Ausschließen ihres Geräts aus der Energieverwaltung gestatten

Wählen Sie **Ja** aus, damit Softwarecenter-Benutzer ihre Computer von den konfigurierten Energieverwaltungseinstellungen ausschließen können.  

### <a name="allow-network-wake-up"></a>Netzwerkreaktivierung zulassen

Wenn Sie diese Einstellung aktivieren, konfiguriert der Client die Energieeinstellungen auf dem Computer so, dass der Netzwerkadapter das Gerät reaktivieren kann. Wenn Sie die Einstellung deaktivieren, kann der Computer nicht von seinem Netzwerkadapter reaktiviert werden.

### <a name="enable-wake-up-proxy"></a>Aktivierungsproxy zulassen

Geben Sie **Ja** an, um die Wake-On-LAN-Einstellung des Standorts zu ergänzen, wenn diese für Unicastpakete konfiguriert ist.  

Weitere Informationen zum Aktivierungsproxy finden Sie unter [Planen der Clientaktivierung](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Machen Sie sich mit der Funktionsweise eines Aktivierungsproxys vertraut, und bewerten Sie ihn in einer Testumgebung, bevor Sie ihn in einem Produktionsnetzwerk aktivieren.  

Konfigurieren Sie dann bei Bedarf folgende zusätzliche Einstellungen:

- **Portnummer für Aktivierungsproxy (UDP):** Die Portnummer, die Clients verwenden, um Aktivierungspakete an Computer im Energiesparmodus zu senden. Behalten Sie den Standardport 25536 bei, oder ersetzen Sie die Nummer durch einen beliebigen Wert.  

- **Wake-On-LAN-Portnummer (UDP):** Behalten Sie den Standardwert 9 bei, es sei denn, Sie haben die Wake-On-LAN-Portnummer (UDP) in den **Eigenschaften** des Standorts auf der Registerkarte **Ports** geändert.  

    > [!IMPORTANT]  
    > Dieser Wert muss mit dem Wert in den **Eigenschaften**des Standorts übereinstimmen. Wenn Sie den Wert an einem Ort ändern, wird er am anderen Ort nicht automatisch aktualisiert.  

- **Windows Defender Firewall-Ausnahme für Aktivierungsproxy:** Der Konfigurations-Manager-Client konfiguriert die Portnummer des Aktivierungsproxys automatisch auf Geräten, die Windows Defender Firewall ausführen. Wählen Sie **Konfigurieren** aus, um die Firewallprofile anzugeben.  

    Falls auf Clients eine andere Firewall ausgeführt wird, konfigurieren Sie diese manuell so, dass die **Portnummer des Aktivierungsproxy (UDP)** zugelassen wird.  

- **IPv6-Präfixe, sofern für DirectAccess oder andere zwischengeschaltete Netzwerkgeräte erforderlich. Verwenden Sie ein Komma, um mehrere Einträge anzugeben:** Geben Sie die notwendigen IPv6-Präfixe für den Aktivierungsproxy ein, damit dieser in Ihrem Netzwerk funktioniert.



## <a name="remote-tools"></a>Remotetools  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Remotesteuerung auf Clients aktivieren/Firewallausnahmeprofile

Wählen Sie **Konfigurieren** aus, um die Remotesteuerungsfunktion von Configuration Manager zu aktivieren. Konfigurieren Sie optional die Firewall-Einstellungen zum Zulassen der Remotesteuerung auf Clientcomputern.  

Die Remotesteuerung ist standardmäßig deaktiviert.  

> [!IMPORTANT]  
> Wenn Sie die Firewall-Einstellungen nicht konfigurieren, funktioniert die Remotesteuerung möglicherweise nicht ordnungsgemäß.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Benutzer können Richtlinien- oder Benachrichtigungseinstellungen im Softwarecenter ändern

Wählen Sie aus, ob Benutzer die Remotesteuerungsoptionen im Softwarecenter ändern können.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Remotesteuerung eines unbeaufsichtigten Computers zulassen

Wählen Sie aus, ob ein Administrator die Remotesteuerung verwenden kann, um auf einen abgemeldeten oder gesperrten Computer zuzugreifen. Wenn diese Option deaktiviert ist, können nur angemeldete und nicht gesperrte Computer remote gesteuert werden.  

### <a name="prompt-user-for-remote-control-permission"></a>Benutzer zur Vergabe der Berechtigung für Remotesteuerung auffordern

Wählen Sie aus, ob vom Clientcomputer eine Meldung angezeigt werden soll, in der die Zustimmung des Benutzers angefordert wird, bevor eine Remotesteuerungssitzung zugelassen wird.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Benutzer zum Erteilen der Berechtigung zur Übertragung von Inhalten aus der freigegebenen Zwischenablage auffordern

Geben Sie Benutzern die Möglichkeit, Datenübertragungen zu akzeptieren oder zu verweigern, bevor Inhalt aus der freigegebenen Zwischenablage in einer Remotesteuerungssitzung übertragen wird. Benutzer müssen diese Berechtigung nur einmal pro Sitzung erteilen. Viewer können sich selbst keine Berechtigung zur Datenübertragung erteilen.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Der lokalen Administratorgruppe Berechtigung zur Remotesteuerung gewähren

Wählen Sie aus, ob lokale Administratoren auf dem Server, von dem die Remotesteuerungsverbindung gestartet wurde, Remotesteuerungssitzungen mit Clientcomputern erstellen können.  

### <a name="access-level-allowed"></a>Zulässige Zugriffsstufe

Geben Sie die zulässige Zugriffsstufe für die Remotesteuerung an. Wählen Sie eine der folgenden Einstellungen aus:  

- **Kein Zugriff**
- **Nur anzeigen**
- **Vollzugriff**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Zugelassene Viewer für Remotesteuerung und Remoteunterstützung

Wählen Sie **Betrachter festlegen** aus, um die Namen der Windows-Benutzer anzugeben, die Remotesteuerungssitzungen auf Clientcomputern herstellen können.  

### <a name="show-session-notification-icon-on-taskbar"></a>Benachrichtigungssymbol für Sitzung auf Taskleiste anzeigen

Legen Sie diese Einstellung auf **Ja** fest, um ein Symbol für eine aktive Remotesteuerungssitzung auf der Windows-Taskleiste des Clients anzuzeigen.  

### <a name="show-session-connection-bar"></a>Sitzungsverbindungsleiste anzeigen

Legen Sie diese Option auf **Ja** fest, um eine deutlich sichtbare Sitzungsverbindungsleiste auf Clients anzuzeigen, die auf eine aktive Remotesteuerungssitzung hinweist.  

### <a name="play-a-sound-on-client"></a>Sound auf Client wiedergeben

Wählen Sie diese Option aus, damit über einen Sound angegeben wird, dass eine Remotesteuerungssitzung auf einem Clientcomputer aktiv ist. Wählen Sie eine der folgenden Optionen aus:

- **Kein Sound**
- **Am Anfang und Ende der Sitzung** (Standardeinstellung)
- **Wiederholt während der Sitzung**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Einstellungen für nicht angeforderte Remoteunterstützung verwalten

Legen Sie diese Einstellung auf **Ja** fest, um die Verwaltung nicht angeforderter Remoteunterstützungssitzungen durch Configuration Manager zuzulassen.  

Bei nicht angeforderten Remoteunterstützungssitzungen hat der Benutzer am Clientcomputer keine Unterstützung zum Starten der Sitzung angefordert.  

### <a name="manage-solicited-remote-assistance-settings"></a>Einstellungen für angeforderte Remoteunterstützung verwalten

Legen Sie diese Option auf **Ja** fest, um die Verwaltung angeforderter Remoteunterstützungssitzungen durch Configuration Manager zuzulassen.  

Bei angeforderten Remoteunterstützungssitzungen hat der Benutzer am Clientcomputer Unterstützung zum Initiieren einer Sitzung angefordert.  

### <a name="level-of-access-for-remote-assistance"></a>Zugriffsstufe für Remoteunterstützung

Wählen Sie die Zugriffsstufe für Remoteunterstützungssitzungen aus, die über die Configuration Manager-Konsole gestartet werden. Wählen Sie eine der folgenden Optionen aus:

- **Keine** (Standard)
- **Remoteansicht**
- **Vollzugriff**

> [!NOTE]  
> Vor jeder Remoteunterstützungssitzung muss der Benutzer am Clientcomputer dafür die Berechtigung gewähren.  

### <a name="manage-remote-desktop-settings"></a>Einstellungen für Remotedesktop verwalten

Legen Sie diese Option auf **Ja** fest, um die Verwaltung von Remotedesktopsitzungen für Computer durch Configuration Manager zuzulassen.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Zugelassenen Betrachtern das Herstellen einer Verbindung über Remotedesktopverbindung erlauben

Legen Sie diese Option auf **Ja** fest, um Benutzer, die in der Liste der zugelassenen Betrachter angegeben sind, zur lokalen Remotedesktop-Benutzergruppe auf Clients hinzuzufügen.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Bei Computern mit Windows Vista oder höher Authentifizierung auf Netzwerkebene verlangen

Legen Sie diese Option auf **Ja** fest, um die Authentifizierung auf Netzwerkebene (Network Level Authentication, NLA) zum Herstellen von Remotedesktopverbindungen mit Clientcomputern zu verwenden. Die NLA erfordert anfangs weniger Remotecomputerressourcen, da die Benutzerauthentifizierung abgeschlossen ist, bevor eine Remotedesktopverbindung hergestellt wird. Die Verwendung von NLA stellt eine sicherere Konfiguration dar. Durch NLA kann der Computer vor böswilligen Benutzern oder Schadsoftware besser geschützt werden, und das Risiko von DoS-Angriffen wird verringert.  



## <a name="software-center"></a>Software Center

### <a name="select-these-new-settings-to-specify-company-information"></a>Wählen Sie diese neuen Einstellungen aus, um Unternehmensinformationen anzugeben.

Legen Sie diese Option auf **Ja** fest, und geben Sie dann folgende Einstellungen an, um das Softwarecenter mit den Markeninformationen Ihrer Organisation zu versehen:

- **Firmenname:** Geben Sie den Namen der Organisation ein, der Benutzern im Softwarecenter angezeigt wird.  

- **Farbschema für Softwarecenter:** Klicken Sie auf **Farbe auswählen**, um die vom Softwarecenter verwendete primäre Farbe zu definieren.  

- **Logo für Softwarecenter auswählen:** Klicken Sie auf **Durchsuchen**, um ein Bild auszuwählen, das im Softwarecenter angezeigt werden soll. Das Logo muss eine JPEG-, PNG oder BMP-Datei mit 400 × 100 Pixeln und einer Größe von maximal 750 KB sein. Der Dateiname des Logos darf keine Leerzeichen enthalten.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a> Nicht genehmigte Anwendungen im Softwarecenter ausblenden

Wenn Sie diese Option aktivieren, werden Anwendungen, die zwar für den Benutzer verfügbar sind, für die aber eine Genehmigung benötigt wird, im Softwarecenter ausgeblendet.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a> Installierte Anwendungen im Softwarecenter ausblenden

Wenn Sie diese Option aktivieren, werden bereits installierte Anwendungen nicht mehr auf der Registerkarte „Anwendungen“ angezeigt. Diese Option ist als Standard festgelegt, wenn Sie Configuration Manager installieren oder ein Upgrade durchführen. Installierte Anwendungen können weiterhin auf der Registerkarte „Installationsstatus“ überprüft werden. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a> Link zum Anwendungskatalog im Softwarecenter ausblenden

Geben Sie die Sichtbarkeit des Links zur Anwendungskatalog-Website im Softwarecenter an. Wenn diese Option festgelegt ist, wird Benutzern der Link zur Anwendungskatalog-Website im Knoten „Installationsstatus“ des Softwarecenters nicht mehr angezeigt. <!--1358214-->

> [!Important]  
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  

### <a name="software-center-tab-visibility"></a>Sichtbarkeit der Registerkarten im Softwarecenter

#### <a name="starting-in-version-1906"></a>Ab Version 1906
<!--4063773-->

Wählen Sie aus, welche Registerkarten im Softwarecenter angezeigt werden sollen. Verschieben Sie eine Registerkarte mithilfe der Schaltfläche **Hinzufügen** in **Visible tabs** (Sichtbare Registerkarten). Verschieben Sie sie mithilfe der Schaltfläche **Entfernen** in die Liste **Hidden tabs** (Ausgeblendete Registerkarten). Ordnen Sie die Registerkarten mithilfe der Schaltflächen **Nach oben** und **Nach unten**. 

Verfügbare Registerkarten:
- **Anwendungen**
- **Updates**
- **Betriebssysteme**
- **Installationsstatus**
- **Gerätekonformität**
- **Optionen**
- Fügen Sie bis zu fünf benutzerdefinierte Registerkarten hinzu, indem Sie auf die Schaltfläche **Registerkarte hinzufügen** klicken.
  - Geben Sie **Registerkartenname** und **Inhalts-URL** für die benutzerdefinierte Registerkarte an.
  - Wählen Sie **Registerkarte löschen** aus, um eine benutzerdefinierte Registerkarte zu entfernen.  

  >[!Important]  
  > - Einige Websitefunktionen können bei Verwendung als benutzerdefinierte Registerkarte im Softwarecenter möglicherweise nicht verwendet werden. Daher sollten Sie die Ergebnisse vor der Bereitstellung für Clients testen. <!--519659-->
  > - Geben Sie nur vertrauenswürdige oder Intranet-Websiteadressen an, wenn Sie eine benutzerdefinierte Registerkarte hinzufügen.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Version 1902 und früher

Legen Sie die zusätzlichen Einstellungen in dieser Gruppe auf **Ja** fest, um folgende Registerkarten im Softwarecenter anzuzeigen:

- **Anwendungen**
- **Updates**
- **Betriebssysteme**
- **Installationsstatus**
- **Gerätekonformität**
- **Optionen**
- **Angeben einer benutzerdefinierten Registerkarte für das Softwarecenter** <!--1358132-->
    - **Registerkartenname**
    - **Inhalts-URL**

    >[!Important]  
    > Einige Websitefunktionen können bei Verwendung als benutzerdefinierte Registerkarte im Softwarecenter möglicherweise nicht verwendet werden. Daher sollten Sie die Ergebnisse vor der Bereitstellung für Clients testen. <!--519659-->
    >
    > Geben Sie nur vertrauenswürdige oder Intranet-Websiteadressen an, wenn Sie eine benutzerdefinierte Registerkarte hinzufügen.<!--SCCMDocs issue 1575-->

Wenn Ihre Organisation beispielsweise keine Konformitätsrichtlinien verwendet und Sie die Registerkarte „Gerätekonformität“ im Softwarecenter ausblenden möchten, legen Sie die Einstellung **Registerkarte „Gerätekonformität“ aktivieren** auf **Nein** fest.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a> Konfigurieren von Standardansichten im Softwarecenter
<!--3612112-->
*(Eingeführt in Version 1902)*

- Legen Sie für den **Standardanwendungsfilter** entweder **alle** oder nur **erforderliche** Anwendungen fest.  

  - Im Softwarecenter werden immer Ihre Standardeinstellungen verwendet. Benutzer können diesen Filter ändern, im Softwarecenter werden deren Einstellungen jedoch nicht beibehalten.  

- Legen Sie für die **Standardanwendungsansicht** entweder die **Kachelansicht** oder die **Listenansicht** fest.

  - Wenn ein Benutzer diese Konfiguration ändert, werden die Benutzereinstellungen zukünftig im Softwarecenter beibehalten.


## <a name="software-deployment"></a>Softwarebereitstellung  

### <a name="schedule-re-evaluation-for-deployments"></a>Erneute Auswertung für Bereitstellungen planen

Konfigurieren Sie einen Zeitplan für die erneute Auswertung der Anforderungsregeln für alle Bereitstellungen durch Configuration Manager. Diese erfolgt standardmäßig alle sieben Tage.  

> [!IMPORTANT]  
> Diese Einstellung wirkt sich mehr auf den lokalen Client als auf das Netzwerk oder den Standortserver aus. Ein aggressiverer Zeitplan für die erneute Auswertung wirkt sich negativ auf die Leistung Ihrer Netzwerk- und Clientcomputer aus. Es wird nicht empfohlen, einen niedrigeren Wert als den Standardwert einzustellen. Wenn Sie diesen Wert ändern, sollten Sie die Leistung genau überwachen.  

Starten Sie diese Aktion auf einem Client, indem Sie in der **Configuration Manager**-Systemsteuerung auf der Registerkarte **Aktionen** die Option **Evaluationszyklus für die Anwendungsbereitstellung** auswählen.  



## <a name="software-inventory"></a>Softwareinventur  

### <a name="enable-software-inventory-on-clients"></a>Softwareinventur auf Clients aktivieren

Standardmäßig ist diese Option auf **Ja** festgelegt. Weitere Informationen finden Sie unter [Einführung in die Softwareinventur](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Softwareinventur- und Dateisammlung planen

Klicken Sie auf **Zeitplan**, um die Häufigkeit anzupassen, mit der Clients die Softwareinventur- und Dateisammlungszyklen ausführen. Standardmäßig erfolgt dieser Zyklus alle sieben Tage.

### <a name="inventory-reporting-detail"></a>Inventurberichtsdetail

Geben Sie eine der folgenden Ebenen der zu inventarisierenden Dateiinformationen an:

- **Nur Datei**
- **Nur Produkt**
- **Vollständige Details** (Standardeinstellung)

### <a name="inventory-these-file-types"></a>Diese Dateitypen inventarisieren

Wenn Sie die Typen der zu inventarisierenden Dateien festlegen möchten, klicken Sie auf **Typen festlegen**, und konfigurieren Sie dann folgende Optionen:  

> [!NOTE]  
> Wenn mehr als eine benutzerdefinierte Clienteinstellung auf einen Computer angewendet wurde, werden die von allen Einstellungen zurückgegebenen Inventare zusammengeführt.  

- Wählen Sie **Neu** aus, um einen neuen Dateityp zum Inventar hinzuzufügen. Geben Sie anschließend im Dialogfeld **Eigenschaften für inventarisierte Datei(en)** die folgenden Informationen an:  

    - **Name:** Geben Sie einen Namen für die Datei an, die Sie inventarisieren möchten. Verwenden Sie ein Sternchen (`*`) als Platzhalter, um eine beliebige Textzeichenfolge darzustellen, und ein Fragezeichen (`?`), um ein beliebiges einzelnes Zeichen darzustellen. Geben Sie als Dateinamen z. B. `*.doc` an, um alle Dateien mit der Erweiterung „.doc“ zu inventarisieren.  

    - **Speicherort:** Wählen Sie **Festlegen** aus, um das Dialogfeld **Pfadeigenschaften** zu öffnen. Konfigurieren Sie die Softwareinventur so, dass alle Clientfestplatten nach der angegebenen Datei, nach einem angegebenen Pfad (z. B. `C:\Folder`) oder nach einer angegebenen Variablen (z. B. `%windir%`) durchsucht werden. Sie können auch alle Unterordner unter dem angegebenen Pfad durchsuchen.  

    - **Verschlüsselte und komprimierte Dateien ausschließen:** Wenn Sie diese Option auswählen, werden keine komprimierten oder verschlüsselten Dateien inventarisiert.  

    - **Dateien im Windows-Ordner ausschließen:** Wenn Sie diese Option auswählen, werden keine Dateien im Windows-Ordner und in dessen Unterordnern inventarisiert.  

    Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften für inventarisierte Datei(en)** zu schließen. Fügen Sie alle zu inventarisierenden Dateien hinzu, und klicken Sie dann auf **OK**, um das Dialogfeld **Clienteinstellung konfigurieren** zu schließen.  

### <a name="collect-files"></a>Dateien sammeln

Wenn Sie Dateien von Clientcomputern sammeln möchten, klicken Sie auf **Dateien festlegen**, und konfigurieren Sie dann folgende Einstellungen:  

> [!NOTE]  
> Wenn mehr als eine benutzerdefinierte Clienteinstellung auf einen Computer angewendet wurde, werden die von allen Einstellungen zurückgegebenen Inventare zusammengeführt.  

- Klicken Sie im Dialogfeld **Clienteinstellung konfigurieren** auf das Symbol **Neu**, um eine zu sammelnde Datei hinzuzufügen.  

- Geben Sie im Dialogfeld **Eigenschaften für gesammelte Datei(en)** die folgenden Informationen an:  

    - **Name:** Geben Sie einen Namen für die Datei an, die Sie sammeln möchten. Verwenden Sie ein Sternchen (`*`) als Platzhalter, um eine beliebige Textzeichenfolge darzustellen, und ein Fragezeichen (`?`), um ein beliebiges einzelnes Zeichen darzustellen.  

    - **Speicherort:** Wählen Sie **Festlegen** aus, um das Dialogfeld **Pfadeigenschaften** zu öffnen. Konfigurieren Sie die Softwareinventur so, dass alle Clientfestplatten nach der zu sammelnden Datei, nach einem angegebenen Pfad (z. B. `C:\Folder`) oder nach einer angegebenen Variable (z. B. `%windir%`) durchsucht werden. Sie können auch alle Unterordner unter dem angegebenen Pfad durchsuchen.  

    - **Verschlüsselte und komprimierte Dateien ausschließen:** Wenn Sie diese Option auswählen, werden keine komprimierten oder verschlüsselten Dateien gesammelt.  

    - **Dateisammlung beenden, wenn die Gesamtgröße der Dateien folgenden Wert (KB) überschreitet:** Geben Sie die Dateigröße in Kilobyte (KB) an, ab der der Client das Sammeln der angegebenen Dateien beendet.  

    > [!NOTE]  
    > Die fünf zuletzt geänderten Versionen von gesammelten Dateien werden vom Standortserver gesammelt und im Verzeichnis `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` gespeichert. Wenn eine Datei seit dem letzten Softwareinventurzyklus nicht geändert wurde, wird die Datei nicht noch einmal gesammelt.  
    >
    > Dateien mit mehr als 20 MB werden von der Softwareinventur nicht gesammelt.  
    >
    > Im Dialogfeld **Clienteinstellung konfigurieren** wird mit dem Wert **Maximale Größe aller gesammelten Dateien (KB)** die maximale Größe für alle gesammelten Dateien angezeigt. Wenn diese Größe erreicht ist, wird die Dateisammlung beendet. Alle bereits gesammelten Dateien werden beibehalten und an den Standortserver gesendet.  

    > [!IMPORTANT]
    > Wenn Sie die Softwareinventur so konfigurieren, dass viele große Dateien gesammelt werden, kann diese Konfiguration sich nachteilig auf die Leistung des Netzwerks und Standortservers auswirken.  

    Informationen zum Anzeigen gesammelter Dateien finden Sie unter [Anzeigen des Softwareinventars mit dem Ressourcen-Explorer](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften für gesammelte Datei(en)** zu schließen. Fügen Sie alle zu sammelnden Dateien hinzu, und klicken Sie dann auf **OK**, um das Dialogfeld **Clienteinstellung konfigurieren** zu schließen.  

### <a name="set-names"></a>Namen festlegen

Der Softwareinventur-Agent ruft die Hersteller- und Produktnamen aus den Headerinformationen der Datei ab. Diese Namen sind in den Headerinformationen der Datei nicht immer standardisiert. Wenn Sie die Softwareinventur im Ressourcen-Explorer anzeigen, können verschiedene Versionen des gleichen Hersteller- oder Produktnamens auftreten. Um diese Anzeigenamen zu standardisieren, wählen Sie **Namen festlegen** aus und konfigurieren die folgenden Einstellungen:  

- **Namenstyp:** Von der Softwareinventur werden Informationen zu Herstellern und Produkten gesammelt. Wählen Sie aus, ob Sie die Anzeigenamen für einen **Hersteller** oder für ein **Produkt** konfigurieren möchten.  

- **Anzeigename:** Legt den Anzeigenamen fest, den Sie anstelle der Namen in der Liste **Inventarisierte Namen** verwenden möchten. Wählen Sie **Neu** aus, um einen neuen Anzeigenamen anzugeben.  

- **Inventarisierte Namen:** Wählen Sie **Neu** aus, um einen inventarisierten Namen hinzuzufügen. Dieser Name wird in der Softwareinventur durch den Namen ersetzt, der in der Liste **Anzeigename** ausgewählt wurde. Sie können mehrere Namen hinzufügen, die ersetzt werden sollen.  



## <a name="software-metering"></a>Softwaremessung

### <a name="enable-software-metering-on-clients"></a>Softwaremessung auf Clients aktivieren

Diese Einstellung ist standardmäßig auf **Ja** festgelegt. Weitere Informationen finden Sie unter [Softwaremessung](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Datensammlung planen

Wählen Sie **Zeitplan** aus, um die Häufigkeit anzupassen, mit der Clients den Softwaremessungszyklus ausführen. Standardmäßig erfolgt dieser Zyklus alle sieben Tage.



## <a name="software-updates"></a>Softwareupdates  

### <a name="enable-software-updates-on-clients"></a>Softwareupdates auf Clients aktivieren

Verwenden Sie diese Einstellung, um Softwareupdates auf Configuration Manager-Clients zu aktivieren. Wenn Sie diese Einstellung deaktivieren, werden die vorhandenen Bereitstellungsrichtlinien von Configuration Manager von Clients entfernt. Wenn Sie diese Einstellung wieder aktivieren, wird vom Client die aktuelle Bereitstellungsrichtlinie heruntergeladen.  

> [!IMPORTANT]  
> Wenn Sie diese Einstellung deaktivieren, funktionieren Konformitätsrichtlinien nicht mehr, die auf Softwareupdates basieren.  

### <a name="software-update-scan-schedule"></a>Zeitplan für Softwareupdateprüfung

Wählen Sie **Zeitplan** aus, um anzugeben, wie oft der Client eine Konformitätsbewertung startet. Bei dieser Überprüfung wird der Zustand von Softwareupdates auf dem Client (z.B. „Erforderlich“ oder „Installiert“) bestimmt. Weitere Informationen zur Konformitätsbewertung finden Sie unter [Software updates compliance assessment (Bewertung der Konformität von Softwareupdates)](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Diese Überprüfung verwendet standardmäßig einen einfachen Zeitplan, bei dem die Bewertung alle sieben Tage gestartet wird. Sie können einen benutzerdefinierten Zeitplan erstellen. Dabei können Sie einen exakten Starttag und eine exakte Startzeit angeben, die koordinierte Weltzeit (Universal Coordinated Time, UTC) oder die lokale Zeit verwenden und das Wiederholungsintervall für einen bestimmten Wochentag konfigurieren.  

> [!NOTE]  
> Wenn Sie ein Intervall von weniger als einem Tag angeben, wird in Configuration Manager automatisch der Standardwert von einem Tag festgelegt.  

> [!WARNING]  
> Die tatsächliche Startzeit auf Clientcomputern ist die Startzeit zuzüglich eines zufälligen Zeitraums von maximal zwei Stunden. Durch diese zufällige Anordnung wird verhindert, dass Clientcomputer die Überprüfung initiieren und gleichzeitig eine Verbindung mit dem aktiven Softwareupdatepunkt herstellen.  

### <a name="schedule-deployment-re-evaluation"></a>Bereitstellungsneuauswertung planen

Wählen Sie **Zeitplan** aus, um zu konfigurieren, wie häufig der Client-Agent für Softwareupdates den Installationsstatus der Softwareupdates auf Configuration Manager-Clientcomputern neu auswertet. Wenn bereits installierte Softwareupdates nicht mehr auf Clientcomputern vorhanden, aber weiterhin erforderlich sind, werden diese durch den Client erneut installiert.

Passen Sie diesen Zeitplan gemäß Ihrer Unternehmensrichtlinie für die Konformität von Softwareupdates an, und legen Sie fest, ob Benutzer Softwareupdates deinstallieren können. Jeder Zyklus für eine Neuauswertung der Bereitstellung führt zu Aktivitäten des Netzwerks und des Prozessors des Clientcomputers. Diese Einstellung verwendet standardmäßig einen einfachen Zeitplan, bei dem die Überprüfung zur Neuauswertung für die Bereitstellung alle sieben Tage gestartet wird.  

> [!NOTE]  
> Wenn Sie ein Intervall von weniger als einem Tag angeben, wird in Configuration Manager automatisch der Standardwert von einem Tag festgelegt.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Wenn der Stichtag für eine beliebige Softwareupdatebereitstellung erreicht wird, auch alle anderen Softwarebereitstellungen mit Stichtag innerhalb eines angegebenen Zeitraums installieren

Legen Sie diese Option auf **Ja** fest, um alle Softwareupdates von erforderlichen Bereitstellungen zu installieren, deren Stichtage innerhalb eines angegebenen Zeitraums liegen. Wenn der Stichtag für eine erforderliche Bereitstellung eines Softwareupdates erreicht ist, startet der Client die Installation der Softwareupdates in der Bereitstellung. Diese Einstellung bestimmt, ob Softwareupdates von anderen erforderlichen Bereitstellungen installiert werden sollen, deren Stichtag innerhalb der angegebenen Zeit liegt.  

Verwenden Sie diese Einstellung, um die Installation von erforderlichen Softwareupdates zu beschleunigen. Diese Einstellung kann potenziell auch die Clientsicherheit erhöhen, die Anzahl von Benachrichtigungen an den Benutzer verringern und die Anzahl von Clientneustarts reduzieren. Standardmäßig ist die Priorität auf den Wert **Nein**eingestellt.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Alle anstehenden Bereitstellungen mit Stichtag in diesem Zeitraum werden auch installiert

Verwenden Sie diese Einstellung, um den Zeitraum für die vorherige Einstellung anzugeben. Sie können einen Wert von 1 bis 23 Stunden und von 1 bis 365 Tagen eingeben. Standardmäßig ist diese Einstellung auf sieben Tage festgelegt.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)

*(Eingeführt in Version 1902)*

Legen Sie diese Option auf **Ja** fest, um Clients das Verwenden von Deltainhaltsdateien zu ermöglichen. Mit dieser Einstellung kann der Windows Update-Agent auf dem Gerät bestimmen, welche Inhalte benötigt werden, und diese selektiv herunterladen. 

- Vergewissern Sie sich vor dem Aktivieren dieser Clienteinstellung, dass die Übermittlungsoptimierung ordnungsgemäß für Ihre Umgebung konfiguriert ist. Weitere Informationen finden Sie unter [Windows-Übermittlungsoptimierung](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) und in der [Clienteinstellung für die Übermittlungsoptimierung](#delivery-optimization).
 - Diese Einstellung ersetzt **Installation von Express-Installationsdateien auf Clients aktivieren**. Legen Sie diese Option auf **Ja** fest, um Clients das Verwenden von Express-Installationsdateien zu ermöglichen. Weitere Informationen finden Sie unter [Verwalten von Expressinstallationsdateien für Windows 10-Updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - Ab Version 1910 von Configuration Manager wird bei dieser Option Delta Download nicht nur für Schnellinstallationsdateien, sondern auch für Windows-Updateinstallationsdateien verwendet.
    - Bei der Verwendung eines CMG zum Speichern von Inhalten werden die Inhalte für Updates für Drittanbietersoftware nicht auf Clients heruntergeladen, wenn die Clienteinstellung **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** aktiviert ist. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Von Clients verwendeter Port zum Empfang von Anforderungen für Deltainhalte

*(Eingeführt in Version 1902)*

Diese Einstellung konfiguriert den lokalen Port dafür, dass Deltainhalte durch den HTTP-Listener heruntergeladen werden können. Standardmäßig ist die Einstellung auf 8005 festgelegt. Sie müssen diesen Port nicht in der Clientfirewall öffnen. 

> [!NOTE]
>Diese Clienteinstellung ersetzt **Port zum Herunterladen von Inhalten für Express-Installationsdateien**.


### <a name="enable-management-of-the-office-365-client-agent"></a>Verwaltung des Office 365-Client-Agents aktivieren

Wenn diese Option auf **Ja** festgelegt ist, ermöglicht sie die Konfiguration von Office 365-Installationseinstellungen. Sie ermöglicht zudem das Herunterladen von Dateien aus Office Content Delivery Networks (CDNs) und das Bereitstellen der Dateien als Anwendung in Configuration Manager. Weitere Informationen finden Sie unter [Verwalten von Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a> Installation von Softwareupdates im Wartungsfenster "Alle Bereitstellungen" aktivieren, wenn das Wartungsfenster "Softwareupdate" verfügbar ist

Wenn Sie diese Option auf **Ja** festlegen und für den Client mindestens ein Wartungsfenster für „Softwareupdate“ definiert ist, werden Softwareupdates während eines Wartungsfensters „Alle Bereitstellungen“ installiert.

Standardmäßig ist die Priorität auf den Wert **Nein**eingestellt. Dieser Wert führt zum gleichen Verhalten wie zuvor: Wenn beide Typen vorhanden sind, wird das Fenster ignoriert. <!--2839307-->

> [!NOTE]
> Diese Einstellung gilt auch für Wartungsfenster, die Sie so konfigurieren, dass sie auf **Tasksequenzen** angewendet werden.<!-- SCCMDocs-pr #4596 -->
>
> Wenn für den Client nur ein Fenster **Alle Bereitstellungen** verfügbar ist, werden Softwareupdates oder Tasksequenzen weiterhin in diesem Fenster installiert.

#### <a name="maintenance-window-example"></a>Beispiel für Wartungsfenster

Sie konfigurieren beispielsweise die folgenden Wartungsfenster:

- **Alle Bereitstellungen:** 02:00–04:00 Uhr
- **Softwareupdates:** 04:00–06:00 Uhr

Der Client installiert standardmäßig nur Softwareupdates im zweiten Wartungsfenster. Er ignoriert in diesem Szenario das Wartungsfenster für alle Bereitstellungen. Wenn Sie diese Einstellung in **Ja** ändern, installiert der Client Softwareupdates zwischen 02:00 Uhr und 06:00 Uhr.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a> Threadpriorität für Featureupdates angeben

<!--3734525-->
Ab Configuration Manager, Version 1902, können Sie die Priorität anpassen, mit der Windows 10-Clients, Version 1709 oder höher, ein Featureupdate über [Windows 10-Wartung](../../../osd/deploy-use/manage-windows-as-a-service.md) installieren. Diese Einstellung hat keine Auswirkungen auf Tasksequenzen für ein direktes Windows 10-Upgrade.

Diese Clienteinstellung bietet die folgenden Optionen:

- **Nicht konfiguriert**: Configuration Manager ändert nicht die Einstellung. Administratoren können ihre eigene „setupconfig.ini“-Datei vorab bereitstellen. Dieser Wert ist die Standardeinstellung.

- **Normal**: Das Windows Setup verbraucht mehr Systemressourcen und führt Updates schneller aus. Durch den höheren Verbrauch von Prozessorzeit ist zwar die Installationszeit insgesamt kürzer, aber die Unterbrechung für den Benutzer länger.  

    - Konfiguriert die Datei „setupconfig.ini“ auf dem Gerät mit der [Windows-Befehlszeilenoption für Setup](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options), `/Priority Normal`.

- **Niedrig:** Sie können weiterhin mit dem Gerät arbeiten, während der Download und die Updates im Hintergrund ausgeführt werden. Die gesamte Installationszeit ist länger, aber dafür ist die Unterbrechung für den Benutzer kürzer. Möglicherweise müssen Sie die maximale Laufzeit von Updates verlängern, um bei Verwendung dieser Option ein Timeout zu vermeiden.  

    - Entfernt die [Windows-Befehlszeilenoption für Setup](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options), `/Priority`, aus der Datei „setupconfig.ini“.


### <a name="enable-third-party-software-updates"></a>Aktivieren von Softwareupdates von Drittanbietern

Wenn Sie diese Option auf **Ja** festlegen, wird die Richtlinie für das **Zulassen signierter Updates für einen Intranet-Speicherort für den Microsoft-Updatedienst** festgelegt, und das Signaturzertifikat im Speicher für vertrauenswürdige Herausgeber auf dem Client installiert.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Dynamisches Update für Featureupdates aktivieren
<!--4062619-->
Ab Configuration Manager, Version 1906 können Sie [Dynamisches Update für Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) konfigurieren. „Dynamisches Update“ installiert Language Packs, Features bei Bedarf, Treiber und kumulative Updates während des Windows-Setups, indem der Client zum Download der betreffenden Updates aus dem Internet weitergeleitet wird. Wenn diese Einstellung auf **Ja** oder **Nein** festgelegt ist, ändert Configuration Manager die Datei [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options), die während der Installation von Featureupdates verwendet wird.

- **Nicht konfiguriert**: Der Standardwert. Die Datei „setupconfig“ wird nicht geändert.
  - „Dynamisches Update“ ist in allen unterstützten Versionen von Windows 10 standardmäßig aktiviert.
    - Für Windows 10, Version 1803 und früher, überprüft „Dynamisches Update“ den WSUS-Server des Geräts auf genehmigte dynamische Updates. In Configuration Manager-Umgebungen werden dynamische Updates nie direkt auf dem WSUS-Server genehmigt, daher werden sie von diesen Geräten nicht installiert.
    - Ab Windows 10, Version 1809 ruft „Dynamisches Update“ über die Internetverbindung des Geräts dynamische Updates von Microsoft Update ab. Diese dynamischen Updates werden nicht für die Verwendung durch WSUS veröffentlicht.
- **Ja**: „Dynamisches Update“ wird aktiviert.
- **Nein**: „Dynamisches Update“ wird deaktiviert.


## <a name="state-messaging"></a>Zustandsmeldung

### <a name="state-message-reporting-cycle-minutes"></a>Zustandsmeldungs-Berichtszyklus (Minuten)

Gibt an, wie häufig Clients Zustandsmeldungen ausgeben. Diese Einstellung ist standardmäßig auf 15 Minuten festgelegt.



## <a name="user-and-device-affinity"></a>Affinität zwischen Benutzer und Gerät  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät

Geben Sie die Nutzungsdauer in Minuten an, nach der von Configuration Manager eine Affinität zwischen Benutzer und Gerät erstellt wird. Standardmäßig ist dieser Wert auf 2880 Minuten (zwei Tage) festgelegt.

### <a name="user-device-affinity-usage-threshold-days"></a>Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät

Geben Sie die Anzahl von Tagen an, über die der Client den Schwellenwert für Affinität zwischen Benutzer und Gerät misst. Standardmäßig beträgt dieser Wert 30 Tage.

> [!NOTE]  
> Legen Sie beispielsweise den **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät** auf **60** Minuten und den **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** auf **5** Tage fest. Dann muss der Benutzer das Gerät über einen Zeitraum von fünf Tagen jeweils 60 Minuten lang verwenden, um eine automatische Affinität mit dem Gerät zu erstellen.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren

Wählen Sie **Ja** aus, um eine automatische Affinität zwischen Benutzer und Gerät zu erstellen, die auf den von Configuration Manager gesammelten Verwendungsinformationen basiert.  

### <a name="allow-user-to-define-their-primary-devices"></a>Benutzer das Festlegen primärer Geräte gestatten
<!--3485366-->
Wenn diese Einstellung auf **Ja** festgelegt ist, können Benutzer eigene primäre Geräte im Softwarecenter identifizieren. Weitere Informationen finden Sie im [Benutzerleitfaden für Softwarecenter](../../understand/software-center.md#work-information).

## <a name="windows-analytics"></a>Windows Analytics

> [!Important]  
> Der Windows Analytics-Dienst wurde am 31. Januar 2020 eingestellt. Weitere Informationen finden Sie unter [KB 4521815: Windows Analytics-Deaktivierung am 31. Januar 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics ist die Weiterentwicklung von Windows Analytics. Weitere Informationen finden Sie unter [Was ist Desktop Analytics?](../../../desktop-analytics/overview.md)
