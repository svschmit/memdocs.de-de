---
title: Internetbasierte Clientverwaltung
titleSuffix: Configuration Manager
description: Erstellen Sie einen Plan für die Verwaltung internetbasierter Clients in Configuration Manager.
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 93c6f5166a26db9da1026191f8b07aa88a6f0cfd
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076746"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Planen der internetbasierten Clientverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe der internetbasierten Clientverwaltung (IBCM) können Sie Configuration Manager-Clients verwalten, wenn diese nicht mit Ihrem Unternehmensnetzwerk, sondern standardmäßig mit dem Internet verbunden sind. Diese Möglichkeit bietet eine Reihe von Vorteilen, einschließlich geringerer Kosten, da keine VPNs (Virtuelle Private Netzwerke) ausgeführt werden müssen und Softwareupdates umgehend bereitgestellt werden können.  

 Für die Verwaltung von Clientcomputern in einem öffentlichen Netzwerk gelten höhere Sicherheitsanforderungen. Bei der internetbasierten Clientverwaltung müssen sowohl von den Clients, als auch von den Standortsystemservern, mit denen von den Clients eine Verbindung hergestellt wird, PKI-Zertifikate verwendet werden. Hierdurch wird gewährleistet, dass Verbindungen von einer unabhängigen Stelle authentifiziert und Daten bei der Übertragung von und zu diesen Standortsystemen mit Secure Sockets Layer (SSL) verschlüsselt werden.  

 In den folgenden Abschnitten wird die Planung der internetbasierten Clientverwaltung eingehender erörtert.  

##  <a name="features-that-are-not-supported-on-the-internet"></a>Features, die im Internet nicht unterstützt werden  
 Einige Clientverwaltungsfunktionen eignen sich nicht für das Internet und werden daher bei der Clientverwaltung im Internet nicht unterstützt. Viele Features, die bei der internetbasierten Verwaltung nicht unterstützt werden, sind auf die Active Directory Domain Services angewiesen oder für ein öffentliches Netzwerk ungeeignet, wie z.B. Netzwerkermittlung und Wake-On-LAN (WOL).  

 Die folgenden Features werden bei Clientverwaltung im Internet nicht unterstützt:  

- Clientbereitstellung über das Internet, wie Clientpush und die auf Softwareupdates basierende Clientbereitstellung. Verwenden Sie stattdessen die manuelle Clientinstallation.  

- Automatische Standortzuweisung  

- Wake-On-LAN  

- Betriebssystembereitstellung Sie können aber Tasksequenzen bereitstellen, mit denen kein Betriebssystem bereitgestellt wird. Dazu gehören beispielsweise Tasksequenzen zur Ausführung von Skripts und Wartungstasks auf Clients.  

- Remotesteuerung  

- Softwarebereitstellung für Benutzer, es sei denn, der Benutzer kann vom internetbasierten Verwaltungspunkt in den Active Directory Domain Services mit der Windows-Authentifizierung (Kerberos oder NTLM) authentifiziert werden. Dies ist möglich, wenn die Gesamtstruktur, in der das Benutzerkonto sich befindet, vom internetbasierten Verwaltungspunkt als vertrauenswürdig eingestuft wird.  

  Im Übrigen wird von der internetbasierten Clientverwaltung kein Roaming unterstützt. Mithilfe von Roaming kann von Clients immer der nächstgelegene Verteilungspunkt zum Herunterladen von Inhalt ermittelt werden. Bei den im Internet verwalteten Clients erfolgt die Kommunikation mit Standortsystemen über den jeweils zugewiesenen Standort. Dies ist nur möglich, wenn diese Standortsysteme zur Verwendung eines Internet-FQDN konfiguriert wurden und Clientverbindungen aus dem Internet von den Standortsystemrollen gestattet werden. Eines der internetbasierten Standortsysteme wird auf nicht deterministische Weise und unabhängig von der Bandbreite oder vom physischen Standort von den Clients ausgewählt.  

  Softwareupdatepunkte, von denen Verbindungen aus dem Internet akzeptiert werden, werden jetzt immer von internetbasierten Configuration Manager-Clients geprüft. Auf diese Weise wird festgestellt, welche Softwareupdates erforderlich sind. Allerdings wird von internetbasierten Clients immer zuerst versucht, die Softwareupdates von Microsoft Update herunterzuladen, anstatt von einem internetbasierten Verteilungspunkt. Nur wenn dies nicht möglich ist, wird versucht, die erforderlichen Softwareupdates von einem internetbasierten Verteilungspunkt herunterzuladen. Softwareupdates werden von Clients, die nicht für die internetbasierte Clientverwaltung konfiguriert sind, immer über Configuration Manager-Verteilungspunkte und nie von Microsoft Update heruntergeladen.  
 
> [!Tip]  
> Der Configuration Manager-Client bestimmt automatisch, ob er sich im Intranet oder im Internet befindet. Wenn der Client einen Domänencontroller oder einen lokalen Verwaltungspunkt kontaktieren kann, wird der Verbindungstyp auf „Derzeit Intranet“ festgelegt. Andernfalls schaltet er auf „Derzeit Internet“ um, und der Client verwendet die Verwaltungspunkte, Softwareupdatepunkte und Verteilungspunkte, die seinem Standort zu Kommunikationszwecken zugewiesen sind.

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>Überlegungen zur Clientkommunikation über das Internet oder eine nicht vertrauenswürdige Gesamtstruktur  
 Die folgenden, an primären Standorten installierten Standortsystemrollen unterstützen Verbindungen von Clients, die sich an nicht vertrauenswürdigen Standorten wie dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur befinden (sekundäre Standorte unterstützen keine Clientverbindungen von nicht vertrauenswürdigen Standorten):  

- Anwendungskatalog-Websitepunkt  

    > [!Important]  
    > Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Configuration Manager-Richtlinienmodul  

- Verteilungspunkt (HTTPS ist für cloudbasierte Verteilungspunkte erforderlich)  

- Anmeldungsproxypunkt  

- Fallbackstatuspunkt  

- Verwaltungspunkt  

- Softwareupdatepunkt  

  **Informationen zu Standortsystemen mit Internetzugriff:**    
  Es gibt zwar keine Voraussetzung, eine Vertrauensstellung zwischen der Gesamtstruktur eines Clients und der des Standortservers einzurichten, aber wenn die Gesamtstruktur mit einem Standortsystem mit Internetzugriff der Gesamtstruktur vertraut, die die Benutzerkonten enthält, unterstützt diese Konfiguration benutzerbasierte Richtlinien für Geräte im Internet, wenn Sie die **Clientrichtlinien**-Clienteinstellung **Benutzerrichtlinienanforderungen von Internetclients aktivieren** aktivieren.  

  Aus den nachstehenden Konfigurationsbeispielen geht hervor, unter welchen Umständen Benutzerrichtlinien für Geräte im Internet von der internetbasierten Clientverwaltung unterstützt werden:  

- Der internetbasierte Verwaltungspunkt befindet sich im Umkreisnetzwerk, wo der Benutzer von einem schreibgeschützten Domänencontroller authentifiziert wird und Active Directory-Pakete von einer beteiligten Firewall zugelassen werden.  

- Das Benutzerkonto befindet sich in Gesamtstruktur A (im Intranet) und der internetbasierte Verwaltungspunkt in Gesamtstruktur B (im Umkreisnetzwerk). Gesamtstruktur A wird von Gesamtstruktur B als vertrauenswürdig eingestuft, und die Authentifizierungspakete werden von einer beteiligten Firewall zugelassen.  

- Das Benutzerkonto und der internetbasierte Verwaltungspunkt befinden sich in Gesamtstruktur A (im Intranet). Der Verwaltungspunkt wird über einen Webproxyserver im Internet veröffentlicht (z.B. Forefront Threat Management Gateway).  

> [!NOTE]  
>  Sollte die Kerberos-Authentifizierung nicht möglich sein, wird automatisch die Authentifizierung über NTLM versucht.  

 Wie aus dem vorstehenden Beispiel hervorgeht, können Sie internetbasierte Standortsysteme im Intranet platzieren, wenn diese über einen Webproxyserver wie ISA Server und Forefront Threat Management Gateway im Internet veröffentlicht werden. Sie können für diese Standortsysteme festlegen, dass Clientverbindungen nur aus dem Internet oder sowohl aus dem Intranet als auch aus dem Internet unterstützt werden. Einen Webproxyserver können Sie für SSL-zu-SSL-Bridging (Secure Sockets Layer) oder SSL-Tunneling konfigurieren (wobei von Ersterem ein höheres Maß an Sicherheit geboten wird):  

-   **SSL-zu-SSL-Bridging:**    
    Wenn Sie Proxywebserver bei der internetbasierten Clientverwaltung einsetzen, ist SSL-zu-SSL-Bridging empfehlenswert, bei dem ein SSL-Tunnelabschluss mit Authentifizierung verwendet wird. Die Authentifizierung von Clientcomputern muss über die Computerauthentifizierung erfolgen. Die Authentifizierung der Legacyclients mobiler Geräte erfolgt über die Benutzerauthentifizierung. SSL-Bridging wird von mobilen Geräten, die mithilfe von Configuration Manager angemeldet wurden, nicht unterstützt.  

     Der SSL-Tunnelabschluss für den Proxywebserver hat den Vorteil, dass Pakete aus dem Internet überprüft werden, bevor sie an das interne Netzwerk weitergeleitet werden. Die vom Client eingehende Verbindung wird vom Proxywebserver authentifiziert und beendet, und dann wird eine neue authentifizierte Verbindung mit dem internetbasierten Standortsystem hergestellt. Wenn von Configuration Manager-Clients ein Proxywebserver verwendet wird, wird die Clientidentität (Client-GUID) sicher als Bestandteil der Paketnutzdaten transportiert, sodass der Proxywebserver vom Verwaltungspunkt nicht als Client betrachtet wird. In Configuration Manager wird kein HTTP-zu-HTTPS- oder HTTPS-zu-HTTP-Bridging unterstützt.  
     
    > [!Note]  
    > Configuration Manager bietet keine Unterstützung, SSL-Bridgingkonfigurationen von Drittanbietern festzulegen. Beispiele: NetScaler von Citrix oder BIG-IP von F5. Wenden Sie sich an Hersteller Ihres Geräts, um es für die Verwendung mit Configuration Manager zu konfigurieren.  

-   **Tunneling**:   
    Falls die Anforderungen für SSL-Bridging vom Proxywebserver nicht erfüllt werden können oder falls Sie die Internetunterstützung für mobile Geräte, die mithilfe von Configuration Manager registriert wurden, konfigurieren möchten, wird auch SSL-Tunneling unterstützt. Diese Option ist weniger sicher, da die SSL-Pakete aus dem Internet ohne SSL-Tunnelabschluss an die Standortsysteme weitergeleitet werden und daher nicht auf schädliche Inhalte überprüft werden können. Bei der Verwendung von SSL-Tunneling müssen vom Proxywebserver keine Zertifikatanforderungen erfüllt werden.  

##  <a name="planning-for-internet-based-clients"></a>Planung für internetbasierte Clients  
 Sie müssen entscheiden, ob die Clientcomputer, die über das Internet verwaltet werden sollen, für die Verwaltung im Intranet und im Internet oder lediglich für die internetbasierte Clientverwaltung konfiguriert werden. Die Konfiguration der Clientverwaltungsoption ist nur während der Installation eines Clientcomputers möglich. Sollten Sie Ihre Meinung später ändern, müssen Sie den Client neu installieren.  

> [!NOTE]  
>  Wenn Sie einen internetfähigen Verwaltungspunkt konfigurieren, werden Clients, die eine Verbindung zu dem Verwaltungspunkt herstellen internetfähig, wenn sie als Nächstes die Liste der verfügbaren Verwaltungspunkte aktualisieren.  

> [!TIP]  
>  Sie müssen die Konfiguration der internetbasierten Clientverwaltung nicht auf das Internet beschränken, sondern können sie auch im Intranet einsetzen.  

 Bei Clients, die nur für die internetbasierte Clientverwaltung konfiguriert sind, ist die Kommunikation nur mit Standortsystemen möglich, die für Clientverbindungen aus dem Internet konfiguriert sind. Diese Konfiguration eignet sich für Computer, bei denen eine Verbindung mit dem Unternehmensintranet grundsätzlich ausgeschlossen werden kann, z. B. Point-of-Sale-Computer an Remotestandorten. Sie ist gegebenenfalls auch dann die richtige Lösung, wenn Sie die Clientkommunikation auf HTTPS beschränken möchten (z.B. zur Unterstützung von Firewall- und Sicherheitsrichtlinien). Denkbar ist ihre Verwendung auch, wenn Sie internetbasierte Standortsysteme in einem Umkreisnetzwerk installieren und diese Server mit dem Configuration Manager-Client verwalten möchten.  

 Wenn Sie Arbeitsgruppen im Internet verwalten möchten, müssen Sie bei der Installation angeben, dass von ihnen nur Internetverbindungen zugelassen werden.  

> [!NOTE]  
>  Clients für mobile Geräte werden automatisch nur für das Internet konfiguriert, wenn sie zur Verwendung eines internetbasierten Verwaltungspunkts konfiguriert sind.  

 Andere Clientcomputer können für die Clientverwaltung über das Internet oder das Intranet konfiguriert werden. Bei einer Netzwerkänderung ist ein automatischer Wechsel zwischen internet- und intranetbasierter Clientverwaltung möglich. Falls keine Verbindung mit einem für Clientverbindungen im Intranet konfigurierten Verwaltungspunkt möglich ist bzw. kein solcher Verwaltungspunkt gefunden wird, werden diese Clients als Intranetclients mit voller Configuration Manager-Verwaltungsfunktionalität verwaltet. Falls keine Verbindung mit einem für Clientverbindungen im Intranet konfigurierten Verwaltungspunkt möglich ist bzw. kein solcher Verwaltungspunkt gefunden wird, wird versucht, eine Verbindung mit einem internetbasierten Verwaltungspunkt herzustellen. Ist dies möglich, werden diese Clients von den internetbasierten Standortsystemen am zugewiesenen Standort verwaltet.  

 Der automatische Wechsel zwischen internet- und intranetbasierter Clientverwaltung bietet folgende Vorteile: Bei einer Verbindung mit dem Intranet stehen den Clientcomputern automatisch alle Configuration Manager-Features zur Verfügung, und bei einer Verbindung mit dem Internet werden wichtige Verwaltungsfunktionen weiterhin verwendet. Außerdem kann ein im Internet begonnener Download nahtlos im Intranet fortgeführt werden und umgekehrt.  

##  <a name="prerequisites-for-internet-based-client-management"></a>Voraussetzungen für die internetbasierte Clientverwaltung  
 Für die internetbasierte Clientverwaltung in Configuration Manager gelten die folgenden externen Abhängigkeiten:  

- Über das Internet verwaltete Clients müssen über eine Internetverbindung verfügen.  

   Von Configuration Manager werden vorhandene Internetverbindungen von Internetdienstanbietern (Internet Service Provider, ISP) verwendet, bei denen es sich um permanente oder temporäre Verbindungen handeln kann. Für mobile Clientgeräte muss es eine direkte Internetverbindung geben. Bei Clientcomputern hingegen ist eine direkte Internetverbindung oder eine Verbindung über einen Proxywebserver möglich.  

- Standortsysteme, von den die internetbasierte Clientverwaltung unterstützt wird, müssen eine Internetverbindung haben und sich in einer Active Directory-Domäne befinden.  

   Für internetbasierte Standortsysteme ist keine Vertrauensstellung mit der Active Directory-Gesamtstruktur des Standortservers erforderlich. Wenn aber die Authentifizierung des Benutzers mithilfe der Windows-Authentifizierung durch den internetbasierten Verwaltungspunkt möglich ist, werden Benutzerrichtlinien unterstützt. Falls bei der Windows-Authentifizierung ein Fehler auftritt, werden nur Computerrichtlinien unterstützt.  

  > [!NOTE]
  >  Zur Unterstützung von Benutzerrichtlinien müssen Sie die beiden folgenden Clienteinstellungen unter **Clientrichtlinie** auf **Wahr** festlegen:  
  > 
  > - **Benutzerrichtlinienabruf auf Clients aktivieren**  
  >   -   **Benutzerrichtlinienanforderungen von Internetclients aktivieren**  

   Bei einem internetbasierten Anwendungskatalog-Websitepunkt müssen Benutzer, deren Computer sich im Internet befinden, ebenfalls über die Windows-Authentifizierung authentifiziert werden. Diese Anforderung besteht unabhängig von Benutzerrichtlinien.  

- Sie benötigen eine Public Key-Infrastruktur (PKI) zur Bereitstellung und Verwaltung der Zertifikate, die für die Clients erforderlich sind und. Die Zertifikate müssen sowohl im Internet als auch auf den internetbasierten Standortsystemservern verwaltet werden.  

   Weitere Informationen zu den PKI-Zertifikaten finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

- Der internetgestützte, vollständig qualifizierte Domänenname (FQDN) von Standortsystemen, die die internetbasierte Clientverwaltung unterstützen, muss auf öffentlichen DNS-Servern als Hosteintrag registriert sein.  

- Beteiligte Firewalls oder Proxyserver müssen die mit internetbasierten Standortsystemen verbundene Clientkommunikation zulassen.  

   Anforderungen für die Clientkommunikation:  

  - Unterstützung von HTTP 1.1  

  - Zulassen des HTTP-Inhaltstyps mehrteiliger MIME-Anlagen (mehrteilige/gemischte und Anwendungs-/Oktettstream)  

  - Zulassen der folgenden Verben für den internetbasierten Verwaltungspunkt:  

    -   HEAD  

    -   CCM_POST  

    -   BITS_POST  

    -   GET  

    -   PROPFIND  

  - Zulassen der folgenden Verben für den internetbasierten Verteilungspunkt:  

    -   HEAD  

    -   GET  

    -   PROPFIND  

  - Zulassen der folgenden Verben für den internetbasierten Fallbackstatuspunkt:  

    -   POST  

  - Zulassen der folgenden Verben für den internetbasierten Anwendungskatalog-Websitepunkt:  

    -   POST  

    -   GET  

  - Zulassen der folgenden HTTP-Header für den internetbasierten Verwaltungspunkt:  

    -   Bereich:  

    -   CCMClientID:  

    -   CCMClientIDSignature:  

    -   CCMClientTimestamp:  

    -   CCMClientTimestampsSignature:  

  - Zulassen des folgenden HTTP-Headers für den internetbasierten Verwaltungspunkt:  

    -   Bereich:  

    Informationen zu diesen Anforderungen finden Sie in der Dokumentation zur Firewall oder zum Proxyserver.  

    Informationen zu ähnlichen Kommunikationsanforderungen bei Verwendung des Softwareupdatepunkts für Clientverbindungen über das Internet finden Sie in der Dokumentation zu Windows Server Update Services (WSUS). Informationen für WSUS auf Windows Server 2003 finden Sie beispielsweise in [Anhang D: Sicherheitseinstellungen](https://go.microsoft.com/fwlink/p/?LinkId=143368), dem Bereitstellungsanhang für Sicherheitseinstellungen.
