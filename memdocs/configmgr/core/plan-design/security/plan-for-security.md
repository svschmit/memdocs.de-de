---
title: Planen der Sicherheit
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über bewährte Methoden für die Sicherheit in Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b15b3017dd49c75f4281a3c0bfd1c8a695ab8bae
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87525997"
---
# <a name="plan-for-security-in-configuration-manager"></a>Planen der Sicherheit in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel beschreibt die Konzepte, die Sie bei der Planung der Sicherheit Ihrer Configuration Manager-Implementierung berücksichtigen sollten. Er enthält folgende Abschnitte:  

- [Planen von Zertifikaten (selbstsigniert und PKI)](#BKMK_PlanningForCertificates)  
  - [Cryptography: Next Generation-Zertifikate (CNG)](#bkmk_plan-cng)  
  - [Erweitertes HTTP](#bkmk_plan-ehttp)  
  - [Zertifikate für CMG und CDP](#bkmk_plan-cmgcdp)  
  - [Planen des Signaturzertifikats für den Standortserver (selbstsigniert)](#bkmk_plansitesign)  
  - [Widerrufen von PKI-Zertifikaten](#BKMK_PlanningForCRLs)  
  - [Die vertrauenswürdigen PKI-Stammzertifikate und Zertifikataussteller](#BKMK_PlanningForRootCAs)  
  - [Auswählen des PKI-Clientzertifikats](#BKMK_PlanningForClientCertificateSelection)  
  - [Übergangsstrategie für PKI-Zertifikate und internetbasierte Clientverwaltung](#BKMK_PlanningForPKITransition)  

- [Planen des vertrauenswürdigen Stammschlüssels](#BKMK_PlanningForRTK)  

- [Planen von Signierung und Verschlüsselung](#BKMK_PlanningForSigningEncryption)  

- [Planen der rollenbasierten Verwaltung](#BKMK_PlanningForRBA)  

- [Erstellen von Plänen für Azure Active Directory](#bkmk_planazuread)  

- [Planen der Authentifizierung von SMS-Anbietern](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Planen von Zertifikaten (selbstsigniert und PKI)  

Von Configuration Manager wird eine Kombination von selbstsignierten Zertifikaten und PKI-Zertifikaten (Public Key-Infrastruktur) verwendet.  

Verwenden Sie nach Möglichkeit immer PKI-Zertifikate. Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../network/pki-certificate-requirements.md). Wenn die PKI-Zertifikate von Configuration Manager bei der Registrierung mobiler Geräte angefordert werden, müssen Sie Active Directory Domain Services und eine Unternehmenszertifizierungsstelle verwenden. Alle anderen PKI-Zertifikate werden unabhängig von Configuration Manager bereitgestellt und verwaltet. 

PKI-Zertifikate sind erforderlich, wenn Clientcomputer eine Verbindung mit internetbasierten Standortsystemen herstellen. Für einige Szenarios mit Cloudverwaltungsgateways und Cloudverteilungspunkten sind ebenfalls PKI-Zertifikate erforderlich. Weitere Informationen finden Sie unter [Verwalten von Clients im Internet](../../clients/manage/manage-clients-internet.md).

Wenn Sie eine PKI verwenden, können Sie auch IPsec verwenden, um die Kommunikation zwischen den Servern der Standortsysteme innerhalb eines Standorts, zwischen Standorten sowie beim Übertragen anderer Daten zwischen Computern zu sichern. Die Implementierung von IPsec erfolgt unabhängig von Configuration Manager.  

Wenn keine PKI-Zertifikate verfügbar sind, generiert Configuration Manager automatisch selbstsignierte Zertifikate. Einige Zertifikate in Configuration Manager sind immer selbstsigniert. In den meisten Fällen werden die selbstsignierten Zertifikate von Configuration Manager automatisch verwaltet, sodass Sie keine zusätzlichen Aktionen ausführen müssen. Ein Beispiel hierfür stellt das Signaturzertifikat des Standortservers dar. Dieses Zertifikat ist immer selbstsigniert. Dadurch wird sichergestellt, dass die Richtlinien, die Clients vom Verwaltungspunkt herunterladen, vom Standortserver gesendet und nicht manipuliert wurden.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a> Cryptography: Next Generation-Zertifikate (CNG)  

Configuration Manager unterstützt CNG-Zertifikate (Cryptography Next Generation). Configuration Manager-Clients können das PKI-Clientauthentifizierungszertifikat mit dem privaten Schlüssel im CNG-Schlüsselspeicheranbieter (KSP) verwenden. Dank der KSP-Unterstützung unterstützen Configuration Manager-Clients hardwarebasierte private Schlüssel, wie z. B. TPM KSP für PKI-Clientauthentifizierungszertifikate. Weitere Informationen finden Sie in der [Übersicht über CNG-Zertifikate](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a> Erweitertes HTTP  

Die HTTPS-Kommunikation wird für alle Configuration Manager-Kommunikationspfade empfohlen, ist jedoch wegen der aufwändigen Verwaltung von PKI-Zertifikaten für einige Kunden schwer umsetzbar. Die Einführung der Integration von Azure Active Directory (Azure AD) reduziert einige der Zertifikatanforderungen, aber nicht alle. Ab Version 1806 können Sie **Erweitertes HTTP** für Standorte aktivieren. Durch diese Konfiguration wird HTTPS auf Standortsystemen unterstützt, indem eine Kombination aus selbstsignierten Zertifikaten und Azure AD verwendet wird. PKI-Zertifikate sind nicht erforderlich. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../hierarchy/enhanced-http.md).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a> Zertifikate für CMG und CDP

Wenn Sie Clients im Internet mithilfe von Cloudverwaltungsgateways und Cloudverteilungspunkten verwalten möchten, müssen Sie Zertifikate verwenden. Die Anzahl und die Art der Zertifikate hängen vom jeweiligen Szenario ab. Weitere Informationen finden Sie in den folgenden Artikeln:
- [Zertifikate für das Cloudverwaltungsgateway](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Zertifikate für den Cloudverteilungspunkt](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a> Planen des Signaturzertifikats für den Standortserver (selbstsigniert)  

Kopien des Signaturzertifikat des Standortservers können auf sichere Art von den Active Directory-Domänendiensten und einer Clientpushinstallation an die Clients übermittelt werden. Wenn Clients durch diese Mechanismen keine Kopie des Zertifikats erstellen können, installieren Sie das Zertifikat bei der Installation des Clients. Dieser Vorgang ist besonders dann wichtig, wenn die erste Kommunikation des Clients mit dem Standort über einen internetbasierten Verwaltungspunkt erfolgt. Da dieser Server mit einem nicht vertrauenswürdigen Netzwerk verbunden ist, ist er anfälliger für Angriffe. Wenn Sie diesen zusätzlichen Schritt nicht durchführen, wird von den Clients automatisch eine Kopie des Signaturzertifikats des Standortservers vom Verwaltungspunkt heruntergeladen.  

In folgenden Szenarios ist ein sicheres Herunterladen einer Kopie des Standortserverzertifikats durch Clients nicht möglich:  

- Sie installieren den Client nicht mit Clientpush.  

  - Sie haben das Active Directory-Schema für Configuration Manager nicht erweitert.  

  - Sie haben den Clientstandort nicht in Active Directory Domain Services veröffentlicht.  

  - Der Client befindet sich in einer nicht vertrauenswürdigen Gesamtstruktur oder einer Arbeitsgruppe.  

- Sie verwenden die internetbasierte Clientverwaltung und installieren den Client, wenn dieser online ist.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>So installieren Sie Clients mit einer Kopie des Signaturzertifikats des Standortservers  

1.  Suchen Sie das Signaturzertifikat des Standortservers auf dem primären Standortserver. Das Zertifikat ist unter Windows im Zertifikatspeicher **SMS** gespeichert. Es weist den Antragstellernamen **Site Server** und den Anzeigenamen **Site Server Signing Certificate** auf.  

2.  Exportieren Sie das Zertifikat ohne den privaten Schlüssel, speichern Sie es an einem sicheren Ort, und greifen Sie nur über gesicherte Kanäle darauf zu.  

3.  Installieren Sie den Client mit der folgenden client.msi-Eigenschaft: `SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Planen der PKI-Zertifikatsperrung  

Wenn Sie PKI-Zertifikate mit Configuration Manager verwenden, planen Sie die Verwendung einer Zertifikatsperrliste (Certificate Revocation List, CRL). Geräte verwenden die Zertifikatsperrliste, um das Zertifikat auf dem Computer zu überprüfen, der eine Verbindung herstellt. Bei der Zertifikatsperrliste handelt es sich um eine Datei, die von der Zertifizierungsstelle erstellt und signiert wird. Diese Datei enthält eine Liste der Zertifikate, die die Zertifizierungsstelle zwar ausgestellt hat, die aber gesperrt wurden. Wenn ein Zertifikatadministrator Zertifikate widerruft, wird dessen Fingerabdruck zur Zertifikatsperrliste hinzugefügt. Dies kann beispielsweise eintreten, wenn bekannt ist oder vermutet wird, dass ein ausgestelltes Zertifikat gefährdet ist.

> [!IMPORTANT]  
> Der Speicherort der Zertifikatssperrliste wird einem Zertifikat bei dessen Ausstellung durch die Zertifizierungsstelle hinzugefügt. Deshalb müssen Sie Ihre Sperrliste planen, bevor Sie PKI-Zertifikate bereitstellen, die von Configuration Manager verwendet werden.  

Die Zertifikatsperrliste wird von IIS stets auf Clientzertifikate hin überprüft. Diese Konfiguration können Sie in Configuration Manager nicht ändern. Die Zertifikatssperrliste für Standortsysteme wird von Configuration Manager-Clients standardmäßig geprüft. Deaktivieren Sie diese Einstellung, indem Sie eine Standorteigenschaft und eine CCMSetup-Eigenschaft angeben.  

Wenn die Zertifikatsperrprüfung von Computern verwendet wird, aber keine Zertifikatssperrliste gefunden wird, reagieren die Clients wie bei einer Sperrung aller Zertifikate in der Zertifikatkette. Dieses Verhalten ist darauf zurückzuführen, dass nicht überprüft werden kann, ob sich die Zertifikate in der Zertifikatssperrliste befinden. In diesem Szenario kommt es für alle Verbindungen zu Fehlern, die Zertifikate erfordern und eine Überprüfung der Zertifikatssperrliste einschließen. Bei der Überprüfung, ob Ihre Zertifikatsperrliste über den HTTP-Standort zugänglich ist, muss beachtet werden, dass der Configuration Manager-Client als LOCAL SYSTEM ausgeführt wird. Daher kann die Überprüfung der Zugänglichkeit der Zertifikatssperrliste erfolgreich sein, wenn hierzu ein Webbrowser mit Ausführung im Benutzerkontext verwendet wird. Beim Versuch einer HTTP-Verbindungsherstellung mit derselben Zertifikatsperrlisten-URL wird das Computerkonto jedoch möglicherweise durch die interne Webfilterlösung blockiert. In dieser Situation kann es erforderlich sein, die Zertifikatssperrlisten-URL für vorhandene Webfilterlösungen in die Whitelist aufzunehmen.

Das Überprüfen der Zertifikatsperrliste, wenn ein Zertifikat verwendet wird, ist sicherer als ein gesperrtes Zertifikat zu verwenden. Dadurch entsteht jedoch eine Verzögerung bei der Verbindung, und es müssen zusätzliche Verarbeitungsvorgänge bei dem Client ausgeführt werden. Ihre Organisation benötigt diese zusätzliche Sicherheitsprüfung möglicherweise für Clients, die sich im Internet oder in einem nicht vertrauenswürdigen Netzwerk befinden.  

Wenden Sie sich an Ihre PKI-Administratoren, bevor Sie festlegen, ob die Konfigurations-Manager-Clients die Zertifikatsperrliste überprüfen müssen. Wenn alle folgenden Bedingungen erfüllt sind, sollte diese Option in Configuration Manager aktiviert bleiben:  

- Ihre PKI-Infrastruktur unterstützt eine Zertifikatsperrliste, und diese wurde an einem Speicherort veröffentlicht, der für alle Konfigurations-Manager-Clients zugänglich ist. Zu diesen Clients können Geräte im Internet oder in nicht vertrauenswürdigen Gesamtstrukturen zählen.  

- Es ist wichtiger, die Zertifikatsperrliste bei jeder Verbindung mit einem Standortsystem zu überprüfen, das für die Verwendung von PKI-Zertifikaten konfiguriert ist, als folgende Anforderungen zu erfüllen:  
  - Schnellere Verbindungen  
  - Effiziente Verarbeitung auf dem Client  
  - Das Risiko, dass Clients keine Verbindung mit den Servern herstellen können, wenn die Zertifikatsperrliste nicht gefunden werden kann  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Planen von vertrauenswürdigen PKI-Stammzertifikaten und der Liste der Zertifikataussteller  

Wenn von Ihren IIS-Standortsystemen PKI-Clientzertifikate zur Clientauthentifizierung über HTTP oder zur Clientauthentifizierung und Verschlüsselung über HTTPS verwendet werden, müssen Sie möglicherweise die Stammzertifikate der Zertifizierungsstelle als Standorteigenschaft importieren. Die folgenden beiden Szenarios sind möglich:  

- Sie stellen Betriebssysteme mithilfe von Configuration Manager bereit, und von den Verwaltungspunkten werden nur HTTPS-Clientverbindungen akzeptiert.  

- Sie verwenden PKI-Clientzertifikate, die nicht mit ein Stammzertifikat verkettet sind, dem der Verwaltungspunkt vertraut.  

  > [!NOTE]  
  > Wenn Sie PKI-Clientzertifikate aus der gleichen Zertifizierungsstellenhierarchie ausstellen, von der auch die Serverzertifikate ausgestellt werden, die Sie für Verwaltungspunkte verwenden, müssen Sie dieses Stammzertifikat der Zertifizierungsstelle nicht angeben. Wenn Sie jedoch mehrere Zertifizierungsstellenhierarchien verwenden und nicht sicher sind, ob diese voneinander als vertrauenswürdig eingestuft werden, importieren Sie die Stammzertifizierungsstelle der Zertifizierungsstellenhierarchie des Clients.  

Wenn Sie Stamm-Zertifizierungsstellenzertifikate für Configuration Manager importieren müssen, exportieren Sie sie von der ausstellenden Zertifizierungsstelle oder vom Clientcomputer. Wenn Sie das Zertifikat von der ausstellenden Zertifizierungsstelle exportieren, die auch die Stammzertifizierungsstelle ist, dann achten Sie darauf, dass der private Schlüssel nicht exportiert wird. Speichern Sie die exportierte Zertifikatsdatei an einem sicheren Ort, um Manipulationen zu verhindern. Beim Einrichten des Standorts benötigen Sie Zugriff auf diese Datei. Wenn Sie über das Netzwerk auf die Datei zugreifen, vergewissern Sie sich, dass die Kommunikation durch IPsec vor Manipulationen geschützt ist.  

Wenn ein importiertes Stamm-Zertifizierungsstellenzertifikat erneuert wird, müssen Sie das erneuerte Zertifikat importieren.  

Aus diesen importierten Stamm-Zertifizierungsstellenzertifikaten sowie aus den Stamm-Zertifizierungsstellenzertifikaten jedes Verwaltungspunkts wird die Liste der Zertifikataussteller erstellt, die von Configuration Manager-Computern auf folgende Arten verwendet wird:  

- Wenn Clients Verbindungen mit Verwaltungspunkten herstellen, wird durch die Verwaltungspunkte überprüft, ob das Clientzertifikat mit einem vertrauenswürdigen Stammzertifikat auf der Standortliste der Zertifikataussteller verkettet ist. Wenn dies nicht der Fall ist, wird das Zertifikat abgelehnt, und die PKI-Verbindung kann nicht hergestellt werden.  

- Wenn von Clients ein PKI-Zertifikat ausgewählt wird und für die Clients eine Liste der Zertifikataussteller verfügbar ist, wird ein Zertifikat ausgewählt, das mit einem vertrauenswürdigen Stammzertifikat in dieser Liste verkettet ist. Wenn keine Übereinstimmung vorhanden ist, wird vom Client kein PKI-Zertifikat ausgewählt. Weitere Informationen finden Sie unter [Planen der Auswahl des PKI-Clientzertifikats](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planen der Auswahl des PKI-Clientzertifikats  

Wenn von Ihren IIS-Standortsystemen PKI-Clientzertifikate zur Clientauthentifizierung über HTTP oder zur Clientauthentifizierung und Verschlüsselung über HTTPS verwendet wird, sollten Sie planen, auf welche Art das Zertifikat zur Verwendung in Configuration Manager von den Windows-Clients ausgewählt werden soll.  

> [!NOTE]  
> Nicht alle Geräte unterstützen eine Zertifikatauswahlmethode. Stattdessen wird das erste Zertifikat ausgewählt, das die Zertifikatanforderungen erfüllt. Von Clients auf Mac-Computern und mobilen Geräten wird beispielsweise keine Zertifikatauswahlmethode unterstützt.  

In vielen Fällen sind Standardkonfiguration und Standardverhalten ausreichend. Vom Configuration Manager-Client auf Windows-Computern werden mehrere Zertifikate anhand der folgenden Kriterien in der angegebenen Reihenfolge gefiltert:  

1.  Liste der Zertifikataussteller: Das Zertifikat ist mit einem Stamm-Zertifizierungsstellenzertifikat verkettet, das vom Verwaltungspunkt als vertrauenswürdig eingestuft wird.  

2.  Das Zertifikat befindet sich im Standardzertifikatspeicher **Persönlich**.  

3.  Das Zertifikat ist gültig. Es ist nicht gesperrt und nicht abgelaufen. Die Gültigkeitsüberprüfung stellt ebenfalls sicher, dass auf den privaten Schlüssel zugegriffen werden kann.  

4.  Das Zertifikat verfügt über die Möglichkeit der Clientauthentifizierung.

5.  Das Antragstellername des Zertifikats enthält den Namen des lokalen Computers als Substring.  

6.  Das Zertifikat weist die längste Gültigkeitsdauer auf.  

Konfigurieren Sie Clients mithilfe der folgenden Mechanismen dafür, die Liste der Zertifikataussteller zu verwenden:  

- Veröffentlichen Sie diese mit Configuration Manager-Standortinformationen in Active Directory Domain Services.  

- Installieren Sie Clients mithilfe von Clientpush.  

- Clients, die ihrem Standort erfolgreich zugewiesen wurden, laden die Liste vom Verwaltungspunkt herunter.  

- Geben Sie diese während der Clientinstallation als „CCMSetup client.msi“-Eigenschaft von CCMCERTISSUERS an.  

Clients, deren Erstinstallation ohne die Liste der Zertifikataussteller erfolgt und die dem Standort noch nicht zugewiesen sind, überspringen diesen Schritt. Wenn für die Clients eine Liste der Zertifikataussteller verfügbar ist, aber kein PKI-Zertifikat vorhanden ist, das mit einem vertrauenswürdigen Stammzertifikat in dieser Liste verkettet ist, schlägt die Zertifikatauswahl fehl. Die Clients fahren nicht mit den anderen Kriterien für die Zertifikatauswahl fort.  

In den meisten Fällen wird vom Configuration Manager-Client ein eindeutiges und angemessenes PKI-Zertifikat korrekt identifiziert. Wenn dies jedoch nicht der Fall ist, können Sie die folgenden alternativen Auswahlmethoden einrichten, anstatt das Zertifikat anhand der Clientauthentifizierungsfunktion auszuwählen:  

- Suche nach teilweise übereinstimmenden Zeichenfolgen im Antragstellernamen des Clientzertifikats. Bei dieser Methode wird die Groß-/Kleinschreibung nicht berücksichtigt. Sie kann eingesetzt werden, wenn Sie den vollständig qualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) eines Computers im Feld für den Antragstellernamen verwenden und eine Zertifikatauswahl auf Basis des Domänensuffixes anstreben, beispielsweise **contoso.com**. Sie können diese Auswahlmethode jedoch auch verwenden, um nach einer beliebigen Zeichenfolge im Antragstellernamen des Zertifikats zu suchen, mit der Sie das gewünschte Zertifikat von den anderen Zertifikaten im Clientzertifikatspeicher unterscheiden können.  

  > [!NOTE]
  > Sie können die teilweise übereinstimmenden Zeichenfolgen nicht mit dem alternativen Antragstellernamen (Subject Alternative Name, SAN) als Standorteinstellung verwenden. Sie können zwar mithilfe von CCMSetup eine teilweise übereinstimmende Zeichenfolge für den SAN angeben, doch diese wird in den folgenden Szenarios von den Standorteigenschaften überschrieben:  
  > 
  > - Von Clients werden Standortinformationen abgerufen, die in den Active Directory Domain Services veröffentlicht sind.  
  >   - Clients werden mithilfe einer Clientpushinstallation installiert.  
  > 
  >   Verwenden Sie teilweise Übereinstimmungen beim SAN nur dann, wenn Sie Clients manuell installieren und von den Clients keine Standortinformationen aus Active Directory Domain Services abgerufen werden. Beispielsweise gelten diese Bedingungen für Clients, die mit der Einstellung „Nur Internetverbindungen zulassen“ konfiguriert sind.  

- Eine Suche nach Übereinstimmungen bei den Attributwerten für „Antragstellername“ oder „Alternativer Antragstellername“ im Clientzertifikat Bei dieser Methode wird die Groß-/Kleinschreibung berücksichtigt. Sie kann eingesetzt werden, wenn Sie einen X500-DN (Distinguished Name) oder entsprechende Objektbezeichner (OID) gemäß RFC 3280 verwenden und die Zertifikatauswahl auf den Attributwerten basieren soll. Sie können nur die Attribute und deren Werte angeben, die zur eindeutigen Identifizierung oder Überprüfung der Gültigkeit des Zertifikats erforderlich sind und das Zertifikat von den anderen Zertifikaten im Zertifikatspeicher unterscheiden.  

In der folgenden Tabelle sind die Attributwerte aufgeführt, die von Configuration Manager bei den Auswahlkriterien für Clientzertifikate unterstützt werden.  

|OID-Attribut|DN-Attribut (Distinguished Name)|Attributdefinition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domänenkomponente|  
|1.2.840.113549.1.9.1|E oder E-mail|E-Mail-Adresse|  
|2.5.4.3|CN|Allgemeiner Name|  
|2.5.4.4|SN|Antragstellername|  
|2.5.4.5|SERIALNUMBER|Seriennummer|  
|2.5.4.6|C|Ländercode|  
|2.5.4.7|L|Ort|  
|2.5.4.8|S oder ST|Name des Bundeslands bzw. des Kantons|  
|2.5.4.9|STREET|Straße|  
|2.5.4.10|O|Organisationsname|  
|2.5.4.11|OU|Organisationseinheit|  
|2.5.4.12|T oder Title|Titel|  
|2.5.4.42|G oder GN oder GivenName|Vorname|  
|2.5.4.43|I oder Initials|Initialen|  
|2.5.29.17|(kein Wert)|Alternativer Antragstellername| 

  > [!NOTE]
  > Wenn Sie eine der oben genannten alternativen Zertifikatsauswahlmethoden konfigurieren, muss der Antragstellername des Zertifikats nicht den lokalen Computernamen enthalten.

Falls nach der Anwendung der Auswahlkriterien mehrere geeignete Zertifikate gefunden werden, können Sie die Standardkonfiguration außer Kraft setzen, laut der das Zertifikat mit der längsten Gültigkeitsdauer ausgewählt wird, und stattdessen festlegen, dass kein Zertifikat ausgewählt werden soll. In diesem Fall kann die Kommunikation des Clients mit IIS-Standortsystemen nicht über ein PKI-Zertifikat erfolgen. Vom Client wird eine Fehlermeldung an den ihm zugewiesenen Fallbackstatuspunkt gesendet, um Sie über den Fehler bei der Zertifikatauswahl zu informieren und Ihnen die Gelegenheit zu geben, die Zertifikatauswahlkriterien zu ändern oder zu optimieren. Das Verhalten des Clients richtet sich dann danach, ob die fehlerhafte Verbindung über HTTPS oder HTTP hergestellt wurde:  

- Falls die fehlerhafte Verbindung über HTTPS erfolgte, wird vom Client versucht, eine Verbindung über HTTP herzustellen. Dabei wird das selbstsignierte Zertifikat verwendet.  

- Falls die fehlerhafte Verbindung über HTTP erfolgte, wird vom Client versucht, eine weitere Verbindung über HTTP herzustellen. Dabei wird das selbstsignierte Clientzertifikat verwendet.  

Sie können die Identifizierung eines eindeutigen PKI-Clientzertifikats erleichtern, indem Sie für den **Computerspeicher** anstelle der Standardeinstellung **Persönlich** einen benutzerdefinierten Speicher angeben. Sie müssen diesen Speicher jedoch unabhängig von Configuration Manager erstellen. Zudem müssen Sie in der Lage sein, Zertifikate für diesen benutzerdefinierten Speicher bereitzustellen und zu erneuern, bevor deren Gültigkeit abläuft.  

Weitere Informationen finden Sie unter [Konfigurieren von Einstellungen für PKI-Clientzertifikate](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Planen einer Übergangsstrategie für PKI-Zertifikate und internetbasierte Clientverwaltung  

Mithilfe der flexiblen Konfigurationsoptionen in Configuration Manager können Sie Clients und den Standort allmählich auf PKI-Zertifikate umstellen und so für sichere Clientendpunkte sorgen. PKI-Zertifikate bieten nicht nur eine größere Sicherheit, sondern ermöglichen auch die Verwaltung von Clients im Internet.  

Dank der zahlreichen Konfigurationsmöglichkeiten in Configuration Manager gibt es mehrere Methoden, sämtliche Clients eines Standorts auf HTTPS-Verbindungen umzustellen. Unabhängig von der ausgewählten Methode können Sie die folgenden Schritte als Richtlinie verwenden:  

1. Installieren Sie den Configuration Manager-Standort, und konfigurieren Sie ihn so, dass von den Standortsystemen Clientverbindungen über HTTPS und HTTP akzeptiert werden.  

2. Wählen Sie in den Standorteigenschaften auf der Registerkarte **Kommunikation mit Clientcomputern** unter **Einstellungen des Standortsystems** die Option **HTTP oder HTTPS** aus, und aktivieren Sie das Kontrollkästchen **PKI-Clientzertifikat (Clientauthentifizierungsfunktion) verwenden, sofern dieses verfügbar ist**.  Weitere Informationen finden Sie unter [Konfigurieren von Einstellungen für PKI-Clientzertifikate](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > Ab Version 1906 heißt diese Registerkarte **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->  

3. Führen Sie PKI im Rahmen eines Pilotversuchs für Clientzertifikate ein. Ein Beispiel für eine Bereitstellung finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. Installieren Sie Clients mithilfe der Clientpushinstallation. Weitere Informationen finden Sie unter [Installieren von Konfigurations-Manager-Clients mithilfe von Clientpush](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

5. Überwachen Sie Clientbereitstellung und -status mithilfe der Berichte und Informationen in der Configuration Manager-Konsole.  

6. Verfolgen Sie über die Spalte **Clientzertifikat** im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Geräte** , von wie vielen Clients ein Client-PKI-Zertifikat verwendet wird.  

    Sie können das Configuration Manager-Tool zur Überprüfung der HTTPS-Bereitschaft (**cmHttpsReadiness.exe**) ebenfalls auf Computern bereitstellen. Verwenden Sie anschließend die Berichte, um anzuzeigen, wie viele Computer ein PKI-Clientzertifikat mit Configuration Manager verwenden können.  

   > [!NOTE]
   >  Bei der Installation des Konfigurations-Manager-Clients wird das Tool **CMHttpsReadiness.exe** im Ordner `%windir%\CCM` installiert. Folgende Befehlszeilenoptionen sind bei der Ausführung dieses Tools verfügbar:  
   > 
   > - `/Store:<name>`: Diese Option entspricht der client.msi-Eigenschaft **CCMCERTSTORE**.  
   > - `/Issuers:<list>`: Diese Option entspricht der client.msi-Eigenschaft **CCMCERTISSUERS**.    
   > - `/Criteria:<criteria>`: Diese Option entspricht der client.msi-Eigenschaft **CCMCERTSEL**.    
   > - `/SelectFirstCert`: Diese Option entspricht der client.msi-Eigenschaft **CCMFIRSTCERT**.    
   > 
   >   Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../clients/deploy/about-client-installation-properties.md).  

7. Wenn Sie sicher sind, dass von genügend Clients das eigene PKI-Clientzertifikat erfolgreich für die Authentifizierung über HTTP verwendet wird, gehen Sie wie folgt vor:  

   1.  Stellen Sie ein PKI-Webserverzertifikat auf einem Mitgliedsserver bereit, von dem ein zusätzlicher Verwaltungspunkt für den Standort ausgeführt wird. Konfigurieren Sie dieses Zertifikat in den IIS. Weitere Informationen finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Installieren Sie die Verwaltungspunktrolle auf diesem Server, und konfigurieren Sie in den Verwaltungspunkteigenschaften unter **HTTPS** die Option **Clientverbindungen**.  

8. Überwachen und überprüfen Sie, ob der neue Verwaltungspunkt von Clients mit einem PKI-Zertifikat mithilfe von HTTPS verwendet wird. Verwenden Sie die IIS-Protokollierung oder Leistungsindikatoren.  

9. Konfigurieren Sie andere Standortsystemrollen so neu, dass von ihnen HTTPS-Client-Verbindungen verwendet werden. Wenn Sie Clients im Internet verwalten möchten, sollten Sie sicherstellen, dass die Standortsysteme über einen vollqualifizierten Domänennamen verfügen. Konfigurieren Sie einzelne Verwaltungspunkte und Verteilungspunkte dafür, Clientverbindungen über das Internet zu akzeptieren.  

    > [!IMPORTANT]  
    > Prüfen Sie die Planungsinformationen und Voraussetzungen für die internetbasierte Clientverwaltung, bevor Sie die Standortsystemrollen so einrichten, dass von ihnen Verbindungen aus dem Internet akzeptiert werden. Weitere Informationen finden Sie unter [Datenübertragungen zwischen Endpunkten](../hierarchy/communications-between-endpoints.md).  

10. Erweitern Sie das Rollout von PKI-Zertifikaten auf Clients und Standortsysteme, die IIS ausführen. Richten Sie die Standortsystemrollen nach Bedarf für HTTPS-Clientverbindungen und Internetverbindungen ein.  

11. Zur Gewährleistung eines Höchstmaßes an Sicherheit legen Sie in den Standorteigenschaften die ausschließliche Verwendung von HTTPS fest, wenn Sie sicher sind, dass von allen Clients für die Authentifizierung und Verschlüsselung ein Client-PKI-Zertifikat verwendet wird.  

    Mit diesem Plan werden PKI-Zertifikate für die ausschließliche Authentifizierung über HTTP und für die anschließende Authentifizierung und Verschlüsselung über HTTPS eingeführt. Wenn Sie diesen Plan verwenden, um die Zertifikate schrittweise einzuführen, wird das Risiko reduziert, dass Clients nicht mehr verwaltet werden. Darüber hinaus profitieren Sie von der höchsten Sicherheit, die Configuration Manager unterstützt.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Planen des vertrauenswürdigen Stammschlüssels  

Mit dem vertrauenswürdigen Stammschlüssel von Configuration Manager kann von Konfigurations-Manager-Clients überprüft werden, ob Standortsysteme ihrer Hierarchie angehören. Von jedem Standortserver wird ein Standortaustauschschlüssel für die Kommunikation mit anderen Standorten generiert. Der Standortaustauschschlüssel des Standorts auf der obersten Ebene einer Hierarchie wird als vertrauenswürdiger Stammschlüssel bezeichnet.  

Die Funktion des vertrauenswürdigen Stammschlüssels in Configuration Manager ähnelt der eines Stammzertifikats in einer Public Key-Infrastruktur. Alle Komponenten, die mit dem privaten Schlüssel des vertrauenswürdigen Stammschlüssels signiert sind, werden auch weiter unten in der Hierarchie als vertrauenswürdig betrachtet. Clients speichern eine Kopie des vertrauenswürdigen Stammschlüssels des Standorts im WMI-Namespace **root\ccm\locationservices**. 

Der Standort stellt beispielsweise ein Zertifikat für den Verwaltungspunkt aus, der dieses mit dem privaten Schlüssel des vertrauenswürdigen Stammschlüssels signiert. Der Standort gibt den öffentlichen Schlüssel seines vertrauenswürdigen Stammschlüssels für die Clients frei. Clients können anschließend zwischen den Verwaltungspunkten unterscheiden, die sich in deren Hierarchie befinden oder nicht befinden.   

Die öffentliche Kopie des vertrauenswürdigen Stammschlüssels werden von Clients mithilfe der folgenden zwei Methoden automatisch abgerufen:  

- Erweitern Sie das Active Directory-Schema für Configuration Manager, und veröffentlichen Sie den Standort in Active Directory Domain Services. Clients rufen diese Standortinformationen anschließend vom globalen Katalogserver ab. Weitere Informationen finden Sie unter [Vorbereiten von Active Directory für die Veröffentlichung eines Standorts](../network/extend-the-active-directory-schema.md).  

- Installieren Sie Clients mithilfe der Clientpushinstallation. Weitere Informationen finden Sie unter [Clientpushinstallation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

Falls der vertrauenswürdige Stammschlüssel nicht anhand einer dieser Methoden von Clients abgerufen werden kann, wird der vertrauenswürdige Stammschlüssel des ersten Verwaltungspunkts, mit dem eine Kommunikation hergestellt werden kann, von den Clients als vertrauenswürdig eingestuft. In diesem Fall könnte ein Client an den Verwaltungspunkt eines Angreifers fehlgeleitet werden und Richtlinien von diesem nicht autorisierten Verwaltungspunkt erhalten. Hierfür muss der Angreifer sehr erfahren sein. Dieser Angriff kann nur in dem kurzen Zeitfenster stattfinden, bevor der Client den vertrauenswürdigen Stammschlüssel von einem gültigen Verwaltungspunkt abruft. Um das Risiko zu reduzieren, dass Clients von einem Angreifer an einen nicht autorisierten Verwaltungspunkt fehlgeleitet werden, sollten Sie für den Client im Voraus einen vertrauenswürdigen Stammschlüssel bereitstellen.  

Anhand der folgenden Methoden können Sie einem Configuration Manager-Client den vertrauenswürdigen Stammschlüssel vorab bereitstellen und diesen Schlüssel prüfen:  

- [Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client mithilfe einer Datei](#bkmk_trk-provision-file)  

- [Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client ohne eine Datei](#bkmk_trk-provision-nofile)  

- [Überprüfung des vertrauenswürdigen Stammschlüssels auf einem Client](#bkmk_trk-verify)  

- [Entfernen oder Ersetzen des vertrauenswürdigen Stammschlüssels](#bkmk_trk-reset)  

  > [!NOTE]  
  > Wenn Clients den vertrauenswürdigen Stammschlüssel von Active Directory Domain Services oder mithilfe von Clientpush abrufen können, müssen Sie diesen nicht vorab bereitstellen. 
  > 
  > Wenn Clients über HTTPS mit Verwaltungspunkten kommunizieren, müssen Sie den vertrauenswürdigen Stammschlüssel nicht vorab bereitstellen. Die Vertrauensstellung wird mithilfe der PKI-Zertifikate hergestellt.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a> Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client mithilfe einer Datei  

1.  Öffnen Sie auf dem Standortserver folgende Datei in einem Text-Editor: `<Configuration Manager install directory>\bin\mobileclient.tcf`.  

2.  Suchen Sie den Eintrag **SMSPublicRootKey=** . Kopieren Sie den in dieser Zeile stehenden Schlüssel, und schließen Sie die Datei, ohne Änderungen zu speichern.  

3.  Erstellen Sie eine neue Textdatei, und fügen Sie den in der Datei „mobileclient.tcf“ kopierten Schlüssel ein.  

4.  Speichern Sie die Datei an einem Speicherort, auf den alle Computer Zugriff haben, aber an dem sie vor Manipulationen geschützt ist.  

5.  Installieren Sie den Client mit einer beliebigen Methode, von der client.msi-Eigenschaften akzeptiert werden. Geben Sie die folgende Eigenschaft an: `SMSROOTKEYPATH=<full path and file name>`.  

    > [!IMPORTANT]  
    > Wenn Sie den vertrauenswürdigen Stammschlüssel während der Installation des Clients angeben, geben Sie ebenfalls den Standortcode an. Verwenden Sie folgende client.msi-Eigenschaft: `SMSSITECODE=<site code>`.   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a> Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client ohne eine Datei  

1.  Öffnen Sie auf dem Standortserver folgende Datei in einem Text-Editor: `<Configuration Manager install directory>\bin\mobileclient.tcf`.  

2.  Suchen Sie den Eintrag **SMSPublicRootKey=** . Kopieren Sie den in dieser Zeile stehenden Schlüssel, und schließen Sie die Datei, ohne Änderungen zu speichern.  

3.  Installieren Sie den Client mit einer beliebigen Methode, von der client.msi-Eigenschaften akzeptiert werden. Geben Sie die client.msi-Eigenschaft `SMSPublicRootKey=<key>` an, bei der `<key>` der Zeichenfolge entsprechen sollte, die Sie aus „mobileclient.tcf“ kopiert haben.  

    > [!IMPORTANT]  
    >  Wenn Sie den vertrauenswürdigen Stammschlüssel während der Installation des Clients angeben, geben Sie ebenfalls den Standortcode an. Verwenden Sie folgende client.msi-Eigenschaft: `SMSSITECODE=<site code>`.   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a> Überprüfung des vertrauenswürdigen Stammschlüssels auf einem Client  

1. Öffnen Sie eine Windows PowerShell-Konsole als Administrator.  

2. Führen Sie den folgenden Befehl aus:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

Bei der zurückgegebenen Zeichenfolge handelt es sich um den vertrauenswürdigen Stammschlüssel. Überprüfen Sie, ob diese mit dem Wert **SMSPublicRootKey** in der Datei „mobileclient.tcf“ auf dem Standortserver übereinstimmt.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a> Entfernen oder Ersetzen des vertrauenswürdigen Stammschlüssels  

Entfernen Sie den vertrauenswürdigen Stammschlüssel aus einem Client, indem Sie die client.msi-Eigenschaft **RESETKEYINFORMATION=TRUE** verwenden. 

Installieren Sie den Client erneut mit dem neuen vertrauenswürdigen Stammschlüssel, um den vertrauenswürdigen Stammschlüssel zu ersetzen. Verwenden Sie beispielweise die Clientpushmethode, oder geben Sie die client.msi-Eigenschaft **SMSPublicRootKey** an.  

Weitere Informationen zu diesen Installationseigenschaften finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation](../../clients/deploy/about-client-installation-properties.md).



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Planen von Signierung und Verschlüsselung  
 
Wenn für die gesamte Clientkommunikation PKI-Zertifikate verwendet werden, ist es nicht notwendig, zum Schutz der übermittelten Daten deren Signierung und Verschlüsselung zu planen. Wenn Sie Standortsysteme mit IIS dafür eingerichtet haben, HTTP-Clientverbindungen zuzulassen, sollten Sie zum Schutz der Clientkommunikation an diesem Standort entsprechende Maßnahmen ergreifen.  

Beispielsweise können Sie zum Schutz der Daten, die von Clients an Verwaltungspunkte gesendet werden, festlegen, dass diese signiert sein müssen. Sie können ebenfalls den SHA-256-Algorithmus für die Signierung festlegen. Diese Konfiguration ist sicherer, aber Sie sollten die Verwendung von SHA-256 nur erzwingen, wenn alle Clients diesen Algorithmus unterstützen. Viele Betriebssysteme bieten zwar eine native Unterstützung dafür, aber für ältere Betriebssysteme ist möglicherweise ein Update oder ein Hotfix erforderlich. 

Durch das Signieren werden Daten vor Manipulationen geschützt, und durch die Verschlüsselung wird die Veröffentlichung von Informationen verhindert. Sie können für die Inventurdaten und Zustandsmeldungen, die von Clients an Verwaltungspunkte des Standorts gesendet werden, die 3DES-Verschlüsselung aktivieren. Sie müssen nicht alle Updates auf den Clients installieren, damit diese Option unterstützt wird. Für die Ver- und Entschlüsselung benötigen Clients und Verwaltungspunkte zusätzliche CPU-Auslastung.  

Weitere Informationen zum Konfigurieren der Signatur- und Verschlüsselungseinstellungen finden Sie unter [Konfigurieren von Signierung und Verschlüsselung](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Planen der rollenbasierten Verwaltung  

Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a> Erstellen von Plänen für Azure Active Directory

Configuration Manager ist in Azure Active Directory (Azure AD) integriert, damit der Standort und die Clients eine moderne Authentifizierungsmethode verwenden können. Durch die Integration Ihres Standorts in Azure AD werden folgende Configuration Manager-Szenarios unterstützt:

**Client**  

- [Das Verwalten von Clients im Internet über Cloudverwaltungsgateways](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Das Verwalten von mit Clouddomänen verknüpften Geräten](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Die Co-Verwaltung](../../../comanage/overview.md)  

- [Das Bereitstellen von für Benutzer verfügbaren Apps](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Online-Apps aus dem Microsoft Store für Unternehmen](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Das Reduzieren der Infrastrukturanforderungen, indem [Softwarecenter beispielsweise den Verwaltungspunkt](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) anstelle des App-Katalogs verwenden.  

- [Verwalten von Microsoft 365 Apps for Enterprise](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Server**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [Community Hub](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Cloudverteilungspunkte](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Benutzerermittlung](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Weitere Informationen zum Verbinden Ihres Standorts mit Azure AD finden Sie unter [Konfigurieren von Azure-Diensten](../../servers/deploy/configure/azure-services-wizard.md).


Weitere Informationen zu Azure AD finden Sie in der [Dokumentation zu Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a>Planen der Authentifizierung von SMS-Anbietern
<!--1357013--> 

Ab Version 1810 können Sie die mindestens erforderliche Authentifizierungsebene für den Administratorzugriff auf Configuration Manager-Standorte angeben. Diese Funktion verpflichtet Administratoren dazu, sich mit der erforderlichen Ebene bei Windows anzumelden. Dies gilt für alle Komponenten, die auf den SMS-Anbieter zugreifen. Dazu gehören beispielswiese die Configuration Manager-Konsole, SDK-Methoden und Windows PowerShell-Cmdlets. 

Diese Konfiguration entspricht einer Einstellung für die gesamte Hierarchie. Überprüfen Sie vor dem Ändern dieser Einstellung, ob sich alle Configuration Manager-Administratoren mit der erforderlichen Authentifizierungsebene bei Windows anmelden können. 

Die folgenden Ebenen sind verfügbar:

- **Windows-Authentifizierung:** Hiermit ist eine Authentifizierung mit Active Directory-Domänenanmeldeinformationen erforderlich.   

- **Zertifikatauthentifizierung:** Hiermit ist einer Authentifizierung mit einem gültigen Zertifikat erforderlich, das von einer vertrauenswürdigen PKI-Zertifizierungsstelle ausgestellt wurde.  

- **Windows Hello for Business-Authentifizierung:** Hiermit ist eine Authentifizierung mit starker zweistufiger Authentifizierung erforderlich, die an ein Gerät gebunden ist und biometrische Daten oder eine PIN verwendet.  

Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). 



## <a name="see-also"></a>Weitere Informationen:
- [Sicherheit und Datenschutz für Konfigurations-Manager-Clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurieren der Sicherheit](configure-security.md)  

- [Datenübertragungen zwischen Endpunkten](../hierarchy/communications-between-endpoints.md)  

- [Technische Referenz für kryptografische Steuerelemente](cryptographic-controls-technical-reference.md)  

- [PKI-Zertifikatanforderungen](../network/pki-certificate-requirements.md)  

