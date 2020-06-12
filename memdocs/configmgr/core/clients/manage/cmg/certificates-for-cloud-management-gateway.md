---
title: CMG-Zertifikate
titleSuffix: Configuration Manager
description: Lernen Sie die unterschiedlichen digitalen Zertifikate kennen, die Sie mit dem Cloudverwaltungsgateway verwenden können.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 7e9602ef5ea784dd3e97578d5ff585f2ca662c1e
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347201"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Zertifikate für das Cloudverwaltungsgateway

*Gilt für: Configuration Manager (Current Branch)*

Zur Verwaltung von Clients im Internet mit dem Cloudverwaltungsgateway (cloud management gateway, CMG) benötigen Sie je nach Szenario mindestens eines der folgenden digitalen Zertifikate:  

- [CMG-Serverauthentifizierungszertifikat](#bkmk_serverauth)  
  - [Vertrauenswürdige CMG-Stammzertifikate für Clients](#bkmk_cmgroot)  
  - [Von einem öffentlichen Anbieter ausgestellte Serverauthentifizierungszertifikate](#bkmk_serverauthpublic)  
  - [Über eine Unternehmens-PKI ausgestellte Serverauthentifizierungszertifikate](#bkmk_serverauthpki)  

- [Clientauthentifizierungszertifikat](#bkmk_clientauth)  
  - [Vertrauenswürdige Clientstammzertifikate für CMG](#bkmk_clientroot)  

- [Aktivieren des Verwaltungspunkts für HTTPS](#bkmk_mphttps)  

- [Azure-Verwaltungszertifikat](#bkmk_azuremgmt)  

Weitere Informationen zu unterschiedlichen Szenarios finden Sie unter [Vorbereiten des Cloudverwaltungsgateways](plan-cloud-management-gateway.md).

## <a name="general-information"></a>Allgemeine Informationen

<!--SCCMDocs issue #779-->
Zertifikate für das Cloudverwaltungsgateway unterstützen die folgenden Konfigurationen:  

- Schlüssellänge von 2048 oder 4096 Bit.

- Schlüsselspeicheranbieter für private Zertifikatschlüssel. Weitere Informationen finden Sie in der [Übersicht über CNG-Zertifikate](../../../plan-design/network/cng-certificates-overview.md).  

- Wenn Sie Windows mit der folgenden Richtlinie konfigurieren: **Systemkryptografie: Verwenden von FIPS-konformen Algorithmen für Verschlüsselung, Hashing und Signatur**  

- **TLS 1.2**. Weitere Informationen finden Sie unter [Aktivieren von TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a> CMG-Serverauthentifizierungszertifikat

*Dieses Zertifikat ist für alle Szenarios erforderlich.*

Dieses Zertifikat stellen Sie beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Das CMG erstellt einen HTTPS-Dienst, mit dem internetbasierte Clients eine Verbindung herstellen. Der Server benötigt ein Serverauthentifizierungszertifikat, um einen sicheren Kanal aufbauen zu können. Sie müssen daher von einem öffentlichen Anbieter ein Zertifikat erwerben oder dieses über Ihre Public Key-Infrastruktur (PKI) ausstellen. Weitere Informationen finden Sie im Abschnitt [Vertrauenswürdige CMG-Stammzertifikate für Clients](#bkmk_cmgroot).

> [!NOTE]
> Das CMG-Serverauthentifizierungszertifikat unterstützt Platzhalter. Diese werden von einigen Zertifizierungsstellen bei der Ausstellung eines Zertifikat für den Hostnamen verwendet. Beispiel: `*.contoso.com`. Manche Organisationen verwenden Platzhalterzertifikate, um ihre PKI zu vereinfachen und Wartungskosten zu senken.<!--491233-->  
>
> Weitere Informationen zur Verwendung eines Platzhalterzertifikats mit einem CMG finden Sie unter [Einrichten eines CMG](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->  

Zur Identifizierung eines Diensts in Azure ist für dieses Zertifikat ein auf globaler Ebene eindeutiger Name erforderlich. Bevor Sie ein Zertifikat anfordern, bestätigen Sie, dass der gewünschte Azure-Domänenname eindeutig ist. Diesen Vorgang führen Sie im Folgenden beispielhaft für *GraniteFalls.CloudApp.Net* aus.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an.
1. Wählen Sie **Alle Ressourcen** und dann **Hinzufügen** aus.
1. Suchen Sie nach **Clouddienst**. Wählen Sie **Erstellen** aus.
1. Geben Sie im Feld **DNS-Name** das gewünschte Präfix ein, z.B. *GraniteFalls*. Auf der Benutzeroberfläche wird angezeigt, ob der Domänenname verfügbar ist oder bereits von einem anderen Dienst verwendet wird.

    > [!Important]  
    > Verwenden Sie diesen Vorgang nicht, um den Dienst im Portal zu erstellen, sondern nur, um die Verfügbarkeit des Namens zu überprüfen.

Wenn Sie auch das CMG für Inhalte aktivieren, überprüfen Sie, ob der CMG-Dienstname auch ein eindeutiger Name eines Azure-Speicherkontos ist. Wenn der Name des CMG-Clouddiensts eindeutig ist, der Kontoname jedoch nicht, kann Configuration Manager den Dienst nicht in Azure bereitstellen. Wiederholen Sie den oben beschriebenen Prozess im Azure-Portal mit folgenden Änderungen:

- Suchen Sie nach **Speicherkonto**.
- Testen Sie den gewünschten Namen im Feld **Speicherkontoname**.

Das DNS-Namenspräfix, z. B. *GraniteFalls*, muss eine Länge von 3 bis 24 Zeichen aufweisen, und es dürfen ausschließlich alphanumerische Zeichen verwendet werden. Verwenden Sie keine Sonderzeichen wie beispielsweise einen Bindestrich (`-`).<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a> Vertrauenswürdige CMG-Stammzertifikate für Clients

Clients sind auf vertrauenswürdige CMG-Stammzertifikate angewiesen. Dieses Vertrauen kann auf zwei Wegen sichergestellt werden:

- Verwenden Sie ein Zertifikat eines öffentlichen und global vertrauenswürdigen Zertifikatanbieters. Hierbei kann es sich beispielsweise um DigiCert, Thawte oder VeriSign handeln. Windows-Clients schließen vertrauenswürdige Stammzertifizierungsstellen von diesen Anbietern ein. Wenn Sie ein Serverauthentifizierungszertifikat von einem dieser Anbieter verwenden, vertrauen Ihre Clients automatisch dem Zertifikat.  

- Verwenden Sie ein Zertifikat, das von einer Unternehmenszertifizierungsstelle über Ihre PKI ausgestellt wird. Die meisten Unternehmens-PKI-Implementierungen integrieren vertrauenswürdige Stammzertifizierungsstellen in Windows-Clients. Ein Beispiel ist die Verwendung von Active Directory-Zertifikatdienste mit einer Gruppenrichtlinie. Wenn Sie das CMG-Serverauthentifizierungszertifikat über eine Zertifizierungsstelle ausstellen, der Ihre Clients nicht automatisch vertrauen, fügen Sie internetbasierten Clients ein vertrauenswürdiges Stammzertifikat der Zertifizierungsstelle hinzu.  

  - Sie können auch Configuration Manager-Zertifikatprofile verwenden, um Zertifikate für Clients bereitzustellen. Weitere Informationen finden Sie unter [Einführung in Zertifikatprofile](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).

  - Wenn Sie planen, [den Configuration Manager-Client über Intune zu installieren](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client), können Sie auch die Intune-Zertifikatprofile verwenden, um Zertifikate für Clients bereitzustellen. Weitere Informationen finden Sie unter [Konfigurieren eines Zertifikatprofils für Ihre Geräte in Microsoft Intune](https://docs.microsoft.com/intune/certificates-configure).

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a> Von einem öffentlichen Anbieter ausgestellte Serverauthentifizierungszertifikate

Ein Drittanbieter eines Zertifikats kann kein Zertifikat für CloudApp.net erstellen, da Microsoft diese Domäne besitzt. Sie können nur ein Zertifikat abrufen, das für eine Domäne ausgestellt wurde, die sich in Ihrem Besitz befindet. Die Tatsache, dass Ihre Kunden bereits dem Stammzertifikat eines Drittanbieters vertrauen, ist einer der Hauptgründe für das Nutzen eines Zertifikats dieses Anbieters.

Erstellen Sie mit den folgenden Schritten einen DNS-Alias:

1. Erstellen Sie einen CNAME-Eintrag für das öffentliche DNS Ihrer Organisation. Hierdurch wird für das CMG ein Alias erstellt, den Sie als Anzeigename im öffentlichen Zertifikat verwenden können.

    Der Name des Contoso-CMG lautet beispielsweise **GraniteFalls**. Dieser Name wird in Azure zu **GraniteFalls.CloudApp.Net**. Im öffentlichen DNS-Namespace von Contoso, „contoso.com“, erstellt der DNS-Administrator einen neuen CNAME-Eintrag für **GraniteFalls.Contoso.com** für den tatsächlichen Hostnamen **GraniteFalls.CloudApp.net**.  

2. Fordern Sie mithilfe des allgemeinen Namens (Common Name, CN) des CNAME-Alias ein Serverauthentifizierungszertifikat von einem öffentlichen Anbieter an.
Contoso verwendet als allgemeinen Namen des Zertifikats z.B. **GraniteFalls.Contoso.com**.  

3. Erstellen Sie mit diesem Zertifikat das CMG in der Configuration Manager-Konsole. Auf der Seite **Einstellungen** des Assistenten zum Erstellen von Cloudverwaltungsgateways werden folgende Aktionen ausgeführt:  

    - Der Assistent extrahiert als Dienstnamen den Hostnamen aus dem allgemeinen Namen des Zertifikats, sobald Sie das Serverzertifikat für diesen Clouddienst mit der Option **Zertifikatdatei** hinzufügen.  

    - Anschließend fügt der Assistent zur Erstellung des Diensts in Azure den Hostnamen als Dienst-FQDN an **cloudapp.net** oder **usgovcloudapp.net** für die Azure US Government Cloud an.  

    - Wenn Contoso beispielsweise das CMG erstellt, extrahiert Configuration Manager den Hostnamen **GraniteFalls** aus dem allgemeinen Namen des Zertifikats. Den eigentlichen Dienst erstellt Azure mit dem Namen **GraniteFalls.CloudApp.net**.  

Wenn Sie die CMG-Instanz in Configuration Manager erstellen und das Zertifikat über den Namen „GraniteFalls.Contoso.com“ verfügt, extrahiert Configuration Manager ausschließlich den Hostnamen, zum Beispiel „GraniteFalls“. Dieser Hostname wird dann an „CloudApp.net“ angehängt, was für Azure beim Erstellen eines Clouddienst benötigt wird. Der CNAME-Alias im DNS-Namespace für Ihre Domäne, Contoso.com, ordnet diese beiden FQDNs einander zu. Mit Configuration Manager erhalten Clients eine Richtlinie für den Zugriff auf dieses CMG-Gateway, und die DNS-Zuordnung verknüpft diese, sodass die Clients sicher auf den Dienst in Azure zugreifen können.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a> Über eine Unternehmens-PKI ausgestellte Serverauthentifizierungszertifikate

Erstellen Sie ein benutzerdefiniertes SSL-Zertifikat für das CMG, und gehen Sie dabei wie bei der Zertifikaterstellung für einen Cloudverteilungspunkt vor. Führen Sie die Anweisungen zum [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) durch, aber beachten Sie folgenden Unterschied:

- Geben Sie beim Anfordern des benutzerdefinierten Webserverzertifikats einen FQDN für den allgemeinen Namen des Zertifikats an. Bei diesem Namen kann es sich um einen öffentlichen Domänennamen handeln, der Ihnen gehört, oder um die Domäne „cloudapp.net“. Wenn Sie Ihre eigene öffentliche Domäne verwenden, finden Sie im oben beschriebenen Prozess Informationen zum Erstellen eines DNS-Alias im öffentlichen DNS Ihrer Organisation.  

- Wenn Sie die öffentliche Domäne „cloudapp.net“ für das CMG-Webserverzertifikat verwenden:  

  - Verwenden Sie in der öffentlichen Azure-Cloud einen Namen, der mit **cloudapp.net** endet.  

  - Verwenden Sie für die Azure Government-Cloud einen Namen, der mit **usgovcloudapp.net** endet.  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a> Clientauthentifizierungszertifikat

*Dieses Zertifikat ist für internetbasierte Clients erforderlich, auf denen Windows 8.1 ausgeführt wird, sowie für Windows 10-Geräte, die nicht in Azure Active Directory (Azure AD) eingebunden sind. Außerdem wird es für den CMG-Verbindungspunkt benötigt. Nicht erforderlich ist es hingegen für Windows 10-Clients, die in Azure AD eingebunden sind.*

Clients verwenden dieses Zertifikat, um sich bei dem CMG zu authentifizieren. Windows 10-Geräte, die in Hybrid-Azure AD oder in eine Clouddomäne eingebunden sind, benötigen dieses Zertifikat nicht, da sie Azure AD zur Authentifizierung verwenden.

Stellen Sie dieses Zertifikat außerhalb des Configuration Manager-Kontexts bereit. Beispielsweise können Sie mit Active Directory-Zertifikatdienste und einer Gruppenrichtlinie Clientauthentifizierungszertifikate ausstellen. Weitere Informationen finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

Zum sicheren Weiterleiten von Clientanforderungen benötigt der CMG-Verbindungspunkt ein Clientauthentifizierungszertifikat, das dem Serverauthentifizierungszertifikat im HTTPS-Verwaltungspunkt entspricht. Wenn Clients die Azure AD-Authentifizierung verwenden oder Sie den Verwaltungspunkt für erweitertes HTTP konfigurieren, ist dieses Zertifikat nicht erforderlich. Weitere Informationen finden Sie unter [Verwaltungspunkt für HTTPS aktivieren](#bkmk_mphttps).

> [!NOTE]
> Microsoft empfiehlt, Geräte zu Azure AD hinzuzufügen. Internetbasierte Geräte können Azure AD verwenden, um sich mit Configuration Manager zu authentifizieren. Außerdem werden sowohl Geräte- als auch Benutzerszenarios ermöglicht, unabhängig davon, ob das Gerät mit dem Internet oder dem internen Netzwerk verbunden ist. Weitere Informationen finden Sie unter [Installieren und Registrieren des Clients mithilfe einer Azure AD-Identität](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> Ab Version 2002 gilt Folgendes:<!--5686290--> Configuration Manager weitet seine Unterstützung auf internetbasierte Geräte aus, die nur selten eine Verbindung mit dem internen Netzwerk herstellen, die mit Azure Active Directory (Azure AD) nicht verknüpft werden können und die über keine Methode zum Installieren eines von der PKI ausgestellten Zertifikats verfügen. Weitere Informationen finden Sie unter [Tokenbasierte Authentifizierung für CMG](../../deploy/deploy-clients-cmg-token.md).

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a> Vertrauenswürdige Clientstammzertifikate für CMG

*Dieses Zertifikat ist bei der Verwendung von Clientauthentifizierungszertifikaten erforderlich. Wenn alle Clients Azure AD für die Authentifizierung nutzen, wird dieses Zertifikat nicht benötigt.*

Dieses Zertifikat stellen Sie beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Das CMG ist auf vertrauenswürdige Clientauthentifizierungszertifikate angewiesen. Dieses Vertrauen kann durch die Bereitstellung einer Vertrauenskette für Stammzertifikate sichergestellt werden. Stellen Sie sicher, dass alle Zertifikate zur Vertrauenskette hinzugefügt werden. Wenn beispielsweise das Clientauthentifizierungszertifikat von einer Zwischenzertifizierungsstelle ausgestellt wird, fügen Sie sowohl das Zwischenzertifikat als auch das Stammzertifikat der Zertifizierungsstellen hinzu.

> [!Note]  
> Wenn Sie ein CMG erstellen, müssen Sie auf der Seite „Einstellungen“ kein vertrauenswürdiges Stammzertifikat mehr angeben. Dieses Zertifikat ist nicht erforderlich, wenn Sie Azure Active Directory (Azure AD) für die Clientauthentifizierung verwenden. Früher war es im Assistenten erforderlich. Wenn Sie PKI-Clientauthentifizierungszertifikate verwenden, müssen Sie weiterhin ein vertrauenswürdiges Stammzertifikat für das Cloudverwaltungsgateway hinzufügen.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> In Version 1902 und früher können Sie nur zwei vertrauenswürdige Stammzertifizierungsstellen und vier Zwischenzertifizierungsstellen (untergeordnete Zertifizierungsstellen) hinzufügen.

#### <a name="export-the-client-certificates-trusted-root"></a>Exportieren der vertrauenswürdigen Stammzertifizierungsstellen eines Clientauthentifizierungszertifikats

Nachdem Sie ein Clientauthentifizierungszertifikat für einen Computer ausgestellt haben, können Sie mit den folgenden Schritten auf diesem Computer die vertrauenswürdigen Stammzertifizierungsstellen exportieren:

1. Öffnen Sie das Startmenü. Geben Sie „Ausführen“ ein, um das gleichnamige Fenster zu öffnen. Öffnen Sie `mmc`.  

2. Klicken Sie im Menü „Datei“ auf **Snap-In hinzufügen/entfernen**.  

3. Klicken Sie im Dialogfeld „Snap-Ins hinzufügen bzw. entfernen“ auf **Zertifikate** und anschließend auf **Hinzufügen**.  

    1. Klicken Sie im Dialogfeld für das Zertifikat-Snap-In zuerst auf **Computerkonto** und anschließend auf **Weiter**.  

    1. Klicken Sie im Dialogfeld „Computer auswählen“ zuerst auf **Lokaler Computer** und anschließend auf **Fertig stellen**.  

    1. Klicken Sie im Dialogfeld „Snap-Ins hinzufügen bzw. entfernen“ auf **OK**.  

4. Erweitern Sie die Knoten **Zertifikate** und **Eigene Zertifikate**, und klicken Sie anschließend auf **Zertifikate**.  

5. Wählen Sie ein Zertifikat aus, für das als „Beabsichtigter Zweck“ **Clientauthentifizierung** festgelegt ist.  

    1. Klicken Sie im Menü „Aktion“ auf **Öffnen**.  

    1. Wechseln Sie zur Registerkarte **Zertifizierungspfad**.  

    1. Klicken Sie in der Zertifikatskette zuerst auf das übergeordnete Zertifikat und anschließend auf **Zertifikat anzeigen**.  

6. Wechseln im neuen Dialogfeld „Zertifikat“ zur Registerkarte **Details**. Klicken Sie auf **In Datei kopieren...** .  

7. Schließen Sie den Zertifikatexportassistenten ab, indem Sie das Standardzertifikatformat **DER-codiert-binär X.509 (.CER)** verwenden. Notieren Sie sich den Namen und den Speicherort des exportierten Zertifikats.  

8. Exportieren Sie alle Zertifikate aus dem Zertifizierungspfad des ursprünglichen Clientauthentifizierungszertifikats. Notieren Sie sich, welche exportierten Zertifikate zu Zwischenzertifizierungsstellen und welche zu vertrauenswürdigen Stammzertifizierungsstellen gehören.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a> Aktivieren des Verwaltungspunkts für HTTPS

Stellen Sie dieses Zertifikat außerhalb des Configuration Manager-Kontexts bereit. Beispielsweise können Sie mit Active Directory-Zertifikatdiensten und einer Gruppenrichtlinie ein Webserverzertifikat ausstellen. Weitere Informationen finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md) und [Deploy the web server certificate for site systems that run IIS (Bereitstellen des Webserverzertifikats für Standortsysteme, auf denen IIS ausgeführt wird)](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

Bei Verwendung der Standortoption **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** kann der Verwaltungspunkt HTTP sein. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../../../plan-design/hierarchy/enhanced-http.md).

> [!Tip]  
> Wenn Sie kein erweitertes HTTP verwenden und in Ihrer Umgebung mehrere Verwaltungspunkte vorhanden sind, müssen Sie sie nicht alle als HTTPS-fähig für CMG konfigurieren. Konfigurieren Sie die CMG-fähigen Verwaltungspunkte als **Nur Internet**. Ihre lokalen Clients versuchen dann nicht, Sie zu verwenden.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Erweitertes HTTP-Zertifikat für Verwaltungspunkte

Wenn Sie „Erweitertes HTTP“ aktivieren, generiert der Standortserver ein selbstsigniertes Zertifikat mit dem Namen **SMS Role SSL Certificate** (SSL-Zertifikat für SMS-Rolle), das vom Stammzertifikat für die SMS-Ausstellung ausgestellt wird. Der Verwaltungspunkt fügt dieses Zertifikat der IIS-Standardwebsite hinzu, die an Port 443 gebunden ist.

### <a name="management-point-client-connection-mode-summary"></a>Zusammenfassung zum Clientverbindungsmodus für den Verwaltungspunkt

In den folgenden Tabellen wird zusammengefasst, ob HTTP oder HTTPS abhängig von Clienttyp und Standortversion für den Verwaltungspunkt erforderlich ist.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Für internetbasierte Clients, die mit dem Cloudverwaltungsgateway kommunizieren

Konfigurieren Sie einen lokalen Verwaltungspunkt, um Verbindungen zwischen dem CMG und einem der folgenden Clientverbindungsmodi zuzulassen:

| Clienttyp   | Verwaltungspunkt |
|------------------|------------------|
| Arbeitsgruppe        | E-HTTP<sup>[Hinweis 1](#bkmk_note1)</sup>, HTTPS |
| In AD-Domäne eingebunden | E-HTTP<sup>[Hinweis 1](#bkmk_note1)</sup>, HTTPS |
| In Azure AD eingebunden  | E-HTTP, HTTPS |
| Hybrid eingebunden    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Hinweis 1**: Für diese Konfiguration ist erforderlich, dass der Client über ein [Clientauthentifizierungszertifikat](#bkmk_clientauth) verfügt und nur geräteorientierte Szenarios unterstützt.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Für lokale Clients, die mit dem lokalen Verwaltungspunkt kommunizieren

Konfigurieren Sie einen lokalen Verwaltungspunkt mit einem der folgenden Clientverbindungsmodi:

| Clienttyp   | Verwaltungspunkt |
|------------------|------------------|
| Arbeitsgruppe        | HTTP, HTTPS |
| In AD-Domäne eingebunden | HTTP, HTTPS |
| In Azure AD eingebunden  | HTTPS       |
| Hybrid eingebunden    | HTTP, HTTPS |

> [!NOTE]  
> In AD-Domänen eingebundene Clients unterstützen sowohl geräteorientierte als auch benutzerorientierte Szenarios für die Kommunikation mit einem HTTP- oder HTTPS-Verwaltungspunkt.  
>
> In Azure AD und hybrid eingebundene Clients können für geräteorientierte Szenarios über HTTP kommunizieren, jedoch benötigen sie E-HTTP oder HTTPS für benutzerorientierte Szenarios. Andernfalls verhalten sie sich ähnlich wie Arbeitsgruppenclients.  

#### <a name="legend-of-terms"></a>Legende für Begriffe

- *Arbeitsgruppe*: Das Gerät ist nicht in eine Domäne oder in Azure AD eingebunden, verfügt jedoch über ein [Clientauthentifizierungszertifikat](#bkmk_clientauth).
- *In AD-Domäne eingebunden:* Sie binden das Gerät in eine lokale Active Directory-Domäne ein.
- *In Azure AD eingebunden:* Dies wird auch als „in eine Clouddomäne eingebunden“ bezeichnet. Sie verknüpfen das Gerät mit einem Azure Active Directory-Mandanten. Weitere Informationen finden Sie unter [In Azure AD eingebundene Geräte](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join).
- *Hybrid eingebunden:* Sie binden das Gerät in Ihre lokale Active Directory-Instanz ein und registrieren es in Azure Active Directory. Weitere Informationen finden Sie unter [In Azure AD eingebundene Hybridgeräte](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid).
- *HTTP*: In den Verwaltungspunkteigenschaften legen Sie **HTTP** für die Clientverbindungen fest.
- *HTTPS*: In den Verwaltungspunkteigenschaften legen Sie **HTTPS** für die Clientverbindungen fest.
- *E-HTTP*: Bei den Standorteigenschaften auf der Registerkarte **Kommunikation mit Clientcomputern** legen Sie **HTTPS oder HTTP** als Standortsystemeinstellung fest und aktivieren die Option **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden**. Sie konfigurieren den Verwaltungspunkt für HTTP. Der HTTP-Verwaltungspunkt ist für die HTTP- und HTTPS-Kommunikation (Tokenauthentifizierungsszenarios) bereit.

    > [!Note]
    > Ab Version 1906 heißt diese Registerkarte **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a> Azure-Verwaltungszertifikat

*Dieses Zertifikat ist für klassische Dienstbereitstellungen erforderlich. Für Azure Resource Manager-Bereitstellungen wird es nicht benötigt.*

> [!Important]  
> Klassische Dienstbereitstellungen in Azure sind ab Version 1810 in Configuration Manager veraltet. Verwenden Sie stattdessen Azure Resource Manager-Bereitstellungen für Cloud Management Gateway. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](plan-cloud-management-gateway.md#azure-resource-manager).
>
> Ab Configuration Manager Version 1902 ist Azure Resource Manager der einzige Mechanismus zur Bereitstellung neuer Instanzen des Cloudverwaltungsgateways. Dieses Zertifikat wird in Configuration Manager, Version 1902 und höher, nicht benötigt.<!-- 3605704 -->

Dieses Zertifikat stellen Sie im Azure-Portal und beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Zur Erstellung des CMG in Azure muss sich der Configuration Manager-Dienstverbindungspunkt zuerst bei Ihrem Azure-Abonnement authentifizieren. Bei Nutzung der klassischen Dienstbereitstellung wird von diesem das Azure-Verwaltungszertifikat für die Authentifizierung verwendet. Dieses Zertifikat wird von einem Azure-Administrator für Ihr Abonnement hochgeladen. Stellen Sie das Zertifikat beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Weitere Informationen und Anweisungen zum Hochladen eines Verwaltungszertifikats finden Sie unter den folgenden Artikeln in der Azure-Dokumentation:

- [Cloud services and management certificates (Clouddienste und Verwaltungszertifikate)](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Upload an Azure Service Management Certificate (Hochladen eines Verwaltungszertifikats für Azure-Dienste)](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie die Abonnement-ID kopieren, die dem Verwaltungszertifikat zugeordnet ist. Diese verwenden Sie zur Erstellung des CMG in der Configuration Manager-Konsole.

## <a name="next-steps"></a>Nächste Schritte

- [Einrichten des Cloudverwaltungsgateways](setup-cloud-management-gateway.md)  

- [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](cloud-management-gateway-faq.md)  

- [Sicherheit und Datenschutz für Cloud Management Gateway](security-and-privacy-for-cloud-management-gateway.md)  
