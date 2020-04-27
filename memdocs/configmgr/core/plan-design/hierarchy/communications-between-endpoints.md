---
title: Datenübertragungen zwischen Endpunkten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Configuration Manager-Standortsysteme und -Komponenten über ein Netzwerk kommunizieren.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf22bbf8b0660f598f65cf73d0035e6223a52d1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703648"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Datenübertragungen zwischen Endpunkten in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel wird beschrieben, wie Configuration Manager-Standortsysteme und -Clients über Ihr Netzwerk kommunizieren. Er enthält folgende Abschnitte:  

- [Kommunikation zwischen Standortsystemen in einem Standort](#Planning_Intra-site_Com)  
    - [Kommunikation zwischen Standortserver und Verteilungspunkt](#bkmk_site2dp)  

- [Kommunikation von Clients mit Standortsystemen und Diensten](#Planning_Client_to_Site_System)  
    - [Kommunikation zwischen Client und Verwaltungspunkt](#bkmk_client2mp)  
    - [Kommunikation zwischen Client und Verteilungspunkt](#bkmk_client2dp)  
    - [Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur](#BKMK_clientspan)  
    - [Informationen zu Standortsystemen mit Internetzugriff](#bkmk_internetfacing)  

- [Kommunikation zwischen Active Directory-Gesamtstrukturen](#Plan_Com_X-Forest)  
    - [Unterstützen von Domänencomputern in einer Gesamtstruktur, die für die Gesamtstruktur Ihres Standortservers nicht vertrauenswürdig ist](#bkmk_noforesttrust)  
    - [Unterstützen von Computern in einer Arbeitsgruppe](#bkmk_workgroup)  
    - [Szenarien zum Unterstützen eines Standorts oder einer Hierarchie, der oder die sich über mehrere Domänen und Gesamtstrukturen erstreckt](#bkmk_span)  



##  <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> Kommunikation zwischen Standortsystemen in einem Standort  

 Wenn Configuration Manager-Standortsysteme oder -Komponenten über das Netzwerk mit anderen Standortsystemen oder Komponenten kommunizieren, wird abhängig von der Standortkonfiguration eines der folgenden Protokolle verwendet:  

-   Server Message Block (SMB)  

-   HTTP  

-   HTTPS  

Die Kommunikation zwischen den Servern an einem Standort kann jederzeit auftreten. Dies trifft nicht auf die Kommunikation zwischen dem Standortserver und einem Verteilungspunkt zu. Für diese Kommunikationen wird keine Steuerung der Netzwerkbandbreite verwendet. Da Sie die Kommunikation zwischen Standortsystemen nicht steuern können, stellen Sie sicher, dass Sie die Standortsystemserver an Orten mit schnellen Netzwerken und guter Verbindung installieren.  


### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a> Kommunikation zwischen Standortserver und Verteilungspunkt 

Für die Verwaltung der Inhaltsübertragung vom Standortserver zu Verteilungspunkten stehen die folgenden Vorgehensweisen zur Verfügung:  

-   Konfigurieren Sie den Verteilungspunkt für die Steuerung und Planung der Netzwerkbandbreite. Diese Steuerelemente ähneln den von standortübergreifenden Adressen verwendeten Konfigurationen. Häufig können Sie diese Konfiguration verwenden, anstatt einen weiteren Configuration Manager-Standort zu installieren, falls die Übertragung von Inhalt an Remotenetzwerkorte bei der Bandbreite Priorität hat.  

-   Sie können einen Verteilungspunkt als vorab bereitgestellten Verteilungspunkt installieren. Mithilfe eines vorab bereitgestellten Verteilungspunkts können Sie Inhalt verwenden, der auf dem Verteilungspunktserver manuell abgelegt wird. Die Notwendigkeit, Inhaltsdateien über das Netzwerk zu übertragen, entfällt damit.  

Weitere Informationen finden Sie unter [Verwalten von Netzwerk-Bandbreite für das Content Management in System Center Configuration Manager](manage-network-bandwidth.md).



##  <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> Kommunikation von Clients mit Standortsystemen und Diensten  

Clients initiieren die Kommunikation mit Standortsystemrollen, Active Directory-Domänendiensten und Onlinediensten. Damit diese Kommunikation möglich ist, müssen die Firewalls den Netzwerkdatenverkehr zwischen Clients und dem Endpunkt der Kommunikation zulassen. Weitere Informationen zu Ports und Protokollen, die von Clients verwendet werden, wenn diese mit den Endpunkten kommunizieren, finden Sie unter [In Configuration Manager verwendete Ports](ports.md).  

Bevor ein Client mit einer Standortsystemrolle kommunizieren kann, verwendet der Client die Dienstidentifizierung, um nach einer Rolle zu suchen, die das Protokoll des Clients (HTTP oder HTTPS) unterstützt. Clients verwenden standardmäßig die sicherste Methode, die ihnen zur Verfügung steht. Weitere Informationen finden Sie unter [Understand how clients find site resources and services (Informationen zur Suche nach Standortressourcen und -diensten durch Clients)](understand-how-clients-find-site-resources-and-services.md).  

Konfigurieren Sie eine der folgenden Optionen, um HTTPS zu verwenden:  

- Verwenden Sie eine PKI (Public Key-Infrastruktur), und installieren Sie PKI-Zertifikate auf den Clients und Servern. Informationen zum Verwenden von Zertifikaten finden Sie unter [PKI-Zertifikatanforderungen](../network/pki-certificate-requirements.md).  

- Konfigurieren Sie für den Standort ab Version 1806 die Einstellung **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden**. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](enhanced-http.md).  

Wenn Sie eine Standortsystemrolle bereitstellen, die Internetinformationsdienst (IIS) verwendet und die Kommunikation von Clients unterstützt, müssen Sie angeben, ob Clients eine Verbindung mit dem Standortsystem über HTTP oder HTTPS herstellen. Falls Sie sich für HTTP entscheiden, müssen Sie auch Signierungs- und Verschlüsselungsoptionen erwägen. Weitere Informationen finden Sie unter [Planen von Signierung und Verschlüsselung](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  


### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a> Kommunikation zwischen Client und Verwaltungspunkt

Bei der Kommunikation eines Clients mit einem Verwaltungspunkt gibt es zwei Phasen: Authentifizierung (Transport) und Autorisierung (Nachricht). Dieser Prozess variiert anhand der folgenden Faktoren: 
- Standortkonfiguration: Nur HTTPS, gestattet HTTP oder HTTPS oder gestattet HTTP oder HTTPS mit aktiviertem erweiterten HTTP
- Verwaltungspunktkonfiguration: HTTPS oder HTTP
- Geräteidentität für geräteorientierte Szenarios
- Benutzeridentität für benutzerorientierte Szenarios

In der folgenden Tabelle wird verdeutlicht, wie dieser Prozess funktioniert:  

| Verwaltungspunkttyp  | Clientauthentifizierung  | Clientautorisierung<br>Geräteidentität  | Clientautorisierung<br>Benutzeridentität  |
|----------|---------|---------|---------|
| HTTP     | Anonym<br>Mit erweitertem HTTP überprüft der Standort das *Benutzer*- oder *Gerätetoken* von Azure AD. | Speicherortanforderung: Anonym<br>Clientpaket: Anonym<br>Registrierung mit einer der folgenden Methoden zum Bestätigen der Geräteidentität:<br> – Anonym (manuelle Genehmigung)<br> – in Windows integrierte Authentifizierung<br> – Azure AD-*Gerätetoken* (Erweitertes HTTP)<br>Nach der Registrierung verwendet der Client die Nachrichtensignierung zum Bestätigen der Geräteidentität. | Für benutzerorientierte Szenarios wird eine der folgenden Methoden zum Bestätigen der Benutzeridentität verwendet:<br> – in Windows integrierte Authentifizierung<br> – Azure AD-*Benutzertoken* (Erweitertes HTTP) |
| HTTPS    | Eine der folgenden Methoden wird verwendet:<br> – PKI-Zertifikat<br> – in Windows integrierte Authentifizierung<br> – Azure-AD-*Benutzer*- oder *Gerätetoken* | Speicherortanforderung: Anonym<br>Clientpaket: Anonym<br>Registrierung mit einer der folgenden Methoden zum Bestätigen der Geräteidentität:<br> – Anonym (manuelle Genehmigung)<br> – in Windows integrierte Authentifizierung<br> – PKI-Zertifikat<br> – Azure-AD-*Benutzer*- oder *Gerätetoken*<br>Nach der Registrierung verwendet der Client die Nachrichtensignierung zum Bestätigen der Geräteidentität. | Für benutzerorientierte Szenarios wird eine der folgenden Methoden zum Bestätigen der Benutzeridentität verwendet:<br> – in Windows integrierte Authentifizierung<br> – Azure AD-*Benutzertoken* |

> [!Tip]  
> Weitere Informationen zur Konfiguration des Verwaltungspunkts für verschiedene Geräteidentitätstypen mit Cloud Management Gateway finden Sie unter [Aktivieren des Verwaltungspunkts für HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  


### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a> Kommunikation zwischen Client und Verteilungspunkt

Wenn ein Client mit einem Verteilungspunkt kommuniziert, muss dieser sich nur vor dem Herunterladen des Inhalts authentifizieren. In der folgenden Tabelle wird verdeutlicht, wie dieser Prozess funktioniert:


| Verteilungspunkttyp  | Clientauthentifizierung  |
|----------|---------|
| HTTP     | – Anonym, wenn zulässig<br>– in Windows integrierte Authentifizierung mit Computerkonto oder Netzwerkzugriffskonto<br> – Zugriffstoken für den Inhalt (Erweitertes HTTP) |
| HTTPS    | – PKI-Zertifikat<br> – in Windows integrierte Authentifizierung mit Computerkonto oder Netzwerkzugriffskonto<br> – Zugriffstoken für den Inhalt |


###  <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a> Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur  

Die folgenden, an primären Standorten installierten Standortsystemrollen unterstützen Verbindungen von Clients, die sich an nicht vertrauenswürdigen Standorten wie dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur befinden. (Sekundäre Standorte unterstützen Clientverbindungen von nicht vertrauenswürdigen Standorten nicht.) 

-   Anwendungskatalog-Websitepunkt  

-   Configuration Manager-Richtlinienmodul (NDES) 

-   Verteilungspunkt   

-   Cloudbasierter Verteilungspunkt (erfordert HTTPS)

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt  

-   Softwareupdatepunkt  

-   Cloud Management Gateway (erfordert HTTPS)


### <a name="about-internet-facing-site-systems"></a><a name="bkmk_internetfacing"></a> Informationen zu Standortsystemen mit Internetzugriff

> [!Note]  
> Der folgende Abschnitt befasst sich mit internetbasierten Clientverwaltungsszenarios. Er gilt nicht für Cloud Management Gateway-Szenarios. Weitere Informationen finden Sie unter [Verwalten von Clients im Internet](../../clients/manage/manage-clients-internet.md).  

Eine Vertrauensstellung zwischen der Gesamtstruktur eines Clients und des Standortsystemservers ist nicht erforderlich. Wenn die Gesamtstruktur jedoch mit einem Standortsystem mit Internetzugriff der Gesamtstruktur vertraut, die die Benutzerkonten enthält, unterstützt diese Konfiguration benutzerbasierte Richtlinien für Geräte im Internet, wenn Sie die **Clientrichtlinie**-Clienteinstellung **Benutzerrichtlinienanforderungen von Internetclients aktivieren** aktivieren.  

Aus den nachstehenden Konfigurationsbeispielen geht hervor, unter welchen Umständen Benutzerrichtlinien für Geräte im Internet von der internetbasierten Clientverwaltung unterstützt werden:  

-   Der internetbasierte Verwaltungspunkt befindet sich im Umkreisnetzwerk, wo der Benutzer von einem schreibgeschützten Domänencontroller authentifiziert wird und Active Directory-Pakete von einer beteiligten Firewall zugelassen werden.  

-   Das Benutzerkonto befindet sich in Gesamtstruktur A (im Intranet) und der internetbasierte Verwaltungspunkt in Gesamtstruktur B (im Umkreisnetzwerk). Gesamtstruktur A wird von Gesamtstruktur B als vertrauenswürdig eingestuft, und die Authentifizierungspakete werden von einer beteiligten Firewall zugelassen.  

-   Das Benutzerkonto und der internetbasierte Verwaltungspunkt befinden sich in Gesamtstruktur A (im Intranet). Der Verwaltungspunkt wird über einen Webproxyserver im Internet veröffentlicht (z.B. Forefront Threat Management Gateway).  

> [!NOTE]  
>  Sollte die Kerberos-Authentifizierung nicht möglich sein, wird automatisch die Authentifizierung über NTLM versucht.  

Wie aus dem vorstehenden Beispiel hervorgeht, können Sie internetbasierte Standortsysteme im Intranet platzieren, wenn diese über einen Webproxyserver im Internet veröffentlicht werden. Sie können für diese Standortsysteme festlegen, dass Clientverbindungen nur aus dem Internet oder sowohl aus dem Intranet als auch aus dem Internet unterstützt werden. Einen Webproxyserver können Sie für SSL-zu-SSL-Bridging (Secure Sockets Layer) oder SSL-Tunneling wie folgt konfigurieren (wobei von Ersterem ein höheres Maß an Sicherheit geboten wird):  

-   **SSL-zu-SSL-Bridging:**    
    Wenn Sie Proxywebserver bei der internetbasierten Clientverwaltung einsetzen, ist SSL-zu-SSL-Bridging empfehlenswert, bei dem ein SSL-Tunnelabschluss mit Authentifizierung verwendet wird. Die Authentifizierung von Clientcomputern muss über die Computerauthentifizierung erfolgen. Die Authentifizierung der Legacyclients mobiler Geräte erfolgt über die Benutzerauthentifizierung. SSL-Bridging wird von mobilen Geräten, die mithilfe von Configuration Manager angemeldet wurden, nicht unterstützt.  

     Der SSL-Tunnelabschluss für den Proxywebserver hat den Vorteil, dass Pakete aus dem Internet überprüft werden, bevor sie an das interne Netzwerk weitergeleitet werden. Die vom Client eingehende Verbindung wird vom Proxywebserver authentifiziert und beendet, und dann wird eine neue authentifizierte Verbindung mit dem internetbasierten Standortsystem hergestellt. Wenn Configuration Manager-Clients einen Proxywebserver verwenden, wird die Clientidentität (Client-GUID) sicher als Bestandteil der Paketnutzdaten transportiert, sodass der Proxywebserver vom Verwaltungspunkt nicht als Client betrachtet wird. In Configuration Manager wird kein HTTP-zu-HTTPS- oder HTTPS-zu-HTTP-Bridging unterstützt.  

-   **Tunneling**:   
    Wenn die Anforderungen für SSL-Bridging vom Proxywebserver nicht erfüllt werden können oder Sie die Internetunterstützung für mobile Geräte konfigurieren möchten, die mithilfe von Configuration Manager registriert wurden, wird auch SSL-Tunneling unterstützt. Diese Option ist weniger sicher, da die SSL-Pakete aus dem Internet ohne SSL-Tunnelabschluss an die Standortsysteme weitergeleitet werden und daher nicht auf schädliche Inhalte überprüft werden können. Bei der Verwendung von SSL-Tunneling müssen vom Proxywebserver keine Zertifikatanforderungen erfüllt werden.  



##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> Kommunikation zwischen Active Directory-Gesamtstrukturen  

Configuration Manager unterstützt Standorte und Hierarchien, die mehrere Active Directory-Gesamtstrukturen umfassen. Auch Domänencomputer werden unterstützt, die sich nicht in der gleichen Active Directory-Gesamtstruktur wie der Standortserver befinden, sowie Computer in Arbeitsgruppen.  


### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a> Unterstützen von Domänencomputern in einer Gesamtstruktur, die für die Gesamtstruktur Ihres Standortservers nicht vertrauenswürdig ist 

-   Installieren von Standortsystemrollen in dieser nicht vertrauenswürdigen Gesamtstruktur mit der Option, Standortinformationen an diese Active Directory-Gesamtstruktur zu veröffentlichen  

-   Verwalten dieser Computer, als wären sie Arbeitsgruppencomputer  

Wenn Sie Standortsystemserver in einer nicht vertrauenswürdigen Active Directory-Gesamtstruktur installieren, erfolgt die Kommunikation zwischen Clients und Servern dieser Gesamtstruktur ausschließlich in der Gesamtstruktur, und Configuration Manager kann die Computer über Kerberos authentifizieren. Wenn Sie Standortinformationen in der Gesamtstruktur des Clients veröffentlichen, hat dies Vorteile für die Clients, denn Standortinformationen, beispielsweise eine Liste verfügbarer Verwaltungspunkte, werden aus ihrer Active Directory-Gesamtstruktur abgerufen und müssen nicht vom ihnen zugewiesenen Verwaltungspunkt heruntergeladen werden.  

> [!NOTE]  
>  Wenn Sie Geräte im Internet verwalten möchten, können Sie internetbasierte Standortsystemrollen in Ihrem Umkreisnetzwerk installieren, wenn sich die Standortsystemserver in einer Active Directory-Gesamtstruktur befinden. Für dieses Szenario ist keine bidirektionale Vertrauensstellung zwischen dem Umkreisnetzwerk und der Gesamtstruktur des Standortservers erforderlich.  


### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a> Unterstützen von Computern in einer Arbeitsgruppe  

-   Manuelles Genehmigen von Arbeitsgruppencomputern, wenn für diese HTTP-Clientverbindungen mit Standortsystemrollen verwendet werden. Configuration Manager kann diese Computer nicht über Kerberos authentifizieren.  

-   Konfigurieren von Arbeitsgruppenclients, sodass sie das Netzwerkzugriffskonto verwenden, damit diese Computer Inhalte vom Verteilungspunkt abrufen können.  

-   Bereitstellen eines alternativen Mechanismus für Arbeitsgruppenclients, über den sie nach Verwaltungspunkten suchen können. Verwenden Sie die DNS-Veröffentlichung, WINS oder weisen Sie einen Verwaltungspunkt direkt zu. Diese Clients können keine Standortinformationen aus Active Directory Domain Services abrufen.  

Weitere Informationen finden Sie in den folgenden Artikeln:  

-   [Verwalten von in Konflikt stehenden Datensätzen](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

-   [Netzwerkzugriffskonto](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

-   [Installieren von Configuration Manager-Clients auf Arbeitsgruppencomputern](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  


###  <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Szenarien zum Unterstützen eines Standorts oder einer Hierarchie, der oder die sich über mehrere Domänen und Gesamtstrukturen erstreckt  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Szenario 1: Kommunikation zwischen Standorten in einer Hierarchie, die mehrere Gesamtstrukturen umfasst:  
Dieses Szenario erfordert eine bidirektionale Vertrauensstellung, die die Kerberos-Authentifizierung unterstützt.  Falls keine bidirektionale Gesamtstrukturvertrauensstellung vorhanden ist, die die Kerberos-Authentifizierung unterstützt, wird von Configuration Manager kein untergeordneter Standort in der Remotegesamtstruktur unterstützt.  

Configuration Manager unterstützt das Installieren eines untergeordneten Standorts in einer Remotegesamtstruktur, die über die erforderliche bidirektionale Vertrauensstellung mit der Gesamtstruktur des übergeordneten Standorts verfügt. Beispiel: Sie können einen sekundären Standort in einer Gesamtstruktur platzieren, die nicht mit seinem übergeordneten primären Standort identisch ist, sofern die erforderliche Vertrauensstellung vorliegt.  

> [!NOTE]  
>  Bei einem untergeordneten Standort kann es sich um einen primären Standort (wobei der Standort der zentralen Verwaltung der übergeordnete Standort ist) oder um einen sekundären Standort handeln.  

Für die standortübergreifende Kommunikation werden in Configuration Manager die Datenbankreplikation und dateibasierte Übertragungen verwendet. Beim Installieren eines Standorts müssen Sie ein Konto angeben, mit dem Sie den Standort auf dem gewünschten Server installieren. Über dieses Konto wird auch die Kommunikation zwischen Standorten hergestellt und verwaltet. Nachdem der Standort erfolgreich installiert wurde und die dateibasierten Übertragungen sowie die Datenbankreplikation initiiert wurden, ist die Konfiguration der Kommunikation für diesen Standort abgeschlossen.  

Wenn eine bidirektionale Gesamtstrukturvertrauensstellung zwischen Gesamtstrukturen gegeben ist, sind in Configuration Manager keine weiteren Konfigurationsschritte erforderlich.  

Configuration Manager konfiguriert standardmäßig die folgenden Komponenten, wenn Sie einen neuen untergeordneten Standort installieren:  

-   Eine Route für die standortübergreifende, dateibasierte Replikation an jedem Standort, von der das Computerkonto des Standortservers verwendet wird. Configuration Manager fügt das Computerkonto jedes Computers zur Gruppe **SMS_SiteToSiteConnection_&lt;Standortcode\>** auf dem Zielcomputer hinzu.  

-   Datenbankreplikation zwischen SQL Server-Instanzen an jedem Standort  

Legen Sie außerdem die folgenden Konfigurationen fest:  

-   Die von Configuration Manager benötigten Netzwerkpakete müssen von beteiligten Firewalls und Netzwerkgeräten zugelassen werden.  

-   Die Namensauflösung muss zwischen den Gesamtstrukturen möglich sein.  

-   Zum Installieren eines Standorts oder einer Standortsystemrolle müssen Sie ein Konto mit lokalen Administratorrechten auf dem angegebenen Computer angeben.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Szenario 2: Kommunikation an einem Standort, der mehrere Gesamtstrukturen umfasst  
Dieses Szenario erfordert keine bidirektionale Gesamtstrukturvertrauensstellung.  

Primäre Standorte unterstützen die Installation von Standortsystemrollen auf Computern in Remotegesamtstrukturen.  

-   Der Anwendungskatalog-Webdienstpunkt ist die einzige Ausnahme.  Er wird nur in derselben Gesamtstruktur wie der Standortserver unterstützt.  

-   Wenn eine Standortsystemrolle Verbindungen aus dem Internet akzeptiert, besteht die bewährte Sicherheitsmethode darin, die Standortsystemrollen an einem Standort zu installieren, an dem die Gesamtstrukturgrenze Schutz für den Standortserver bereitstellt (z.B. in einem Umkreisnetzwerk).  

So installieren Sie eine Standortsystemrolle auf einem Computer in einer nicht vertrauenswürdigen Gesamtstruktur:  

- Geben Sie ein **Standortsystem-Installationskonto** an, das vom Standort verwendet werden soll, um die Standortsystemrolle zu installieren. (Dieses Konto benötigt lokale Administratoranmeldeinformationen für die Verbindung.) Danach installieren Sie Standortsystemrollen auf dem angegebenen Computer.  

- Aktivieren Sie die Standortsystemoption **Verbindungen mit diesem Standortsystem müssen vom Standortserver hergestellt werden**. Mit dieser Einstellung müssen Verbindungen vom Standortserver mit dem Standortsystemserver zum Übertragen von Daten hergestellt werden. Diese Konfiguration verhindert, dass der Computer am nicht vertrauenswürdigen Standort einen Kontakt mit dem Standortserver initiiert, der sich in Ihrem vertrauenswürdigen Netzwerk befindet. Diese Verbindungen verwenden das **Standortsystem-Installationskonto**.  

Wenn Sie eine Standortsystemrolle verwenden möchten, die in einer nicht vertrauenswürdigen Gesamtstruktur installiert war, müssen Firewalls den Netzwerkdatenverkehr auch dann zulassen, wenn der Standortserver die Datenübertragung initiiert.  

Außerdem benötigen die folgenden Standortsystemrollen einen direkten Zugriff auf die Standortdatenbank. Aus diesem Grund müssen Firewalls entsprechenden Datenverkehr aus der nicht vertrauenswürdigen Gesamtstruktur an den SQL Server des Standorts zulassen:  

-   Asset Intelligence-Synchronisierungspunkt  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Verwaltungspunkt  

-   Reporting Services-Punkt  

-   Zustandsmigrationspunkt  

Weitere Informationen finden Sie unter [In Configuration Manager verwendete Ports](ports.md).  

Möglicherweise müssen Sie Zugriff des Verwaltungspunkts und des Anmeldungspunkts auf die Standortdatenbank konfigurieren.

-   Beim Installieren dieser Rollen wird das Computerkonto des neuen Standortsystemservers von Configuration Manager standardmäßig als Verbindungskonto für die Standortsystemrolle konfiguriert. Anschließend wird dem Konto die entsprechende SQL Server-Datenbankrolle zugewiesen.  

-   Wenn Sie diese Standortsystemrollen in einer nicht vertrauenswürdigen Domäne installieren, konfigurieren Sie das Verbindungskonto der Standortsystemrolle, damit Informationen aus der Datenbank von der Standortsystemrolle abgerufen werden können.  

Wenn Sie ein Domänenbenutzerkonto so konfigurieren, dass es das Verbindungskonto für diese Standortsystemrollen ist, müssen Sie darauf achten, dass das Domänenbenutzerkonto über entsprechende Zugriffsrechte für die SQL Server-Datenbank am Standort verfügt:  

-   Verwaltungspunkt: **Verwaltungspunkt-Datenbankverbindungskonto**  

-   Anmeldungspunkt: **Anmeldungspunkt-Verbindungskonto**  

Erwägen Sie beim Planen von Standortsystemrollen in anderen Gesamtstrukturen auch die folgenden Punkte:  

-   Legen Sie bei Verwendung von Windows-Firewall in den entsprechenden Firewall-Profilen fest, dass die Kommunikation zwischen dem Standortdatenbankserver und Computern, auf den Remote-Standortsystemrollen installiert sind, zulässig ist.   

-   Wenn die Gesamtstruktur, die die Benutzerkonten enthält, von den internetbasierten Verwaltungspunkten als vertrauenswürdig eingestuft wird, werden Benutzerrichtlinien unterstützt. Wenn keine Vertrauensstellung vorhanden ist, werden nur Computerrichtlinien unterstützt.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Szenario 3: Kommunikation zwischen Clients und Standortsystemrollen, wenn die Clients nicht der gleichen Active Directory-Gesamtstruktur wie der zugehörige Standortserver angehören  
Configuration Manager unterstützt die folgenden Szenarios für Clients, die sich nicht in derselben Gesamtstruktur wie der Standortserver ihres Standorts befinden:  

-   Zwischen der Gesamtstruktur des Clients und der Gesamtstruktur des Standortservers besteht eine bidirektionale Vertrauensstellung.  

-   Der Standortsystemrollenserver befindet sich in der gleichen Gesamtstruktur wie der Client.  

-   Der Client befindet sich auf einem Domänencomputer ohne bidirektionale Vertrauensstellung mit der Gesamtstruktur des Standortservers, und es sind keine Standortsystemrollen in der Gesamtstruktur des Clients installiert.  

-   Der Client befindet sich auf einem Arbeitsgruppencomputer.  

Die Active Directory-Domänendienste können von Clients auf einem zur Domäne gehörenden Computer zur Dienstidentifizierung verwendet werden, sofern der entsprechende Standort in der Active Directory-Gesamtstruktur veröffentlicht wurde.  

So veröffentlichen Sie Standortinformationen in einer anderen Active Directory-Gesamtstruktur:  

-   Angeben der Gesamtstruktur und dann Aktivieren der Veröffentlichung in dieser Gesamtstruktur im Arbeitsbereich **Verwaltung** im Knoten **Active Directory-Gesamtstrukturen** .  

-   Konfigurieren jedes Standorts, sodass er seine Daten in Active Directory-Domänendiensten veröffentlicht. Von den Clients in dieser Gesamtstruktur können dann Standortinformationen abgerufen und Verwaltungspunkte gefunden werden. Für Clients, die Active Directory Domain Services nicht zur Dienstidentifizierung verwenden können, besteht die Möglichkeit, DNS, WINS oder den Verwaltungspunkt zu verwenden, der dem Client zugewiesen wurde.  


####  <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a> Szenario 4: Anordnen des Exchange Server-Connectors in einer Remotegesamtstruktur  

Stellen Sie sicher, dass die Namensauflösung zwischen Gesamtstrukturen funktioniert, um dieses Szenario zu unterstützen. Konfigurieren Sie beispielsweise DNS-Weiterleitungen. Geben Sie den vollqualifizierten Domänennamen des Intranets von Exchange Server beim Konfigurieren des Exchange Server-Connectors an. Weitere Informationen finden Sie unter [Verwalten von Mobilgeräten mit System Center Configuration Manager und Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  



## <a name="see-also"></a>Weitere Informationen:

- [Planen der Sicherheit](../security/plan-for-security.md)  

- [Sicherheit und Datenschutz für Konfigurations-Manager-Clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

