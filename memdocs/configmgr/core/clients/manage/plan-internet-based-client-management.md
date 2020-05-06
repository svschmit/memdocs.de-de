---
title: Internetbasierte Clientverwaltung
titleSuffix: Configuration Manager
description: Erstellen Sie einen Plan für die Verwaltung internetbasierter Clients in Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587222"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Planen der internetbasierten Clientverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die internetbasierte Clientverwaltung (IBCM), um Configuration Manager-Clients zu verwalten, wenn diese nicht mit Ihrem internen Netzwerk verbunden sind. Vorteile der Verwendung von IBCM:

- Vollständige Kontrolle über Server und Rollen, die den Dienst bereitstellen
- Keine Abhängigkeit von einem Clouddienst
- Möglicherweise wird kein virtuelles privates Netzwerk (VPN) benötigt
- Alle Kosten sind dem lokalen Dienst zugeordnet

Aufgrund der höheren Sicherheitsanforderungen für die Verwaltung von Clientcomputern in einem öffentlichen Netzwerk erfordert IBCM die Verwendung von PKI-Zertifikaten. Mit dieser Konfiguration wird sichergestellt, dass Verbindungen von einer unabhängigen Zertifizierungsstelle authentifiziert werden. Wenn IBCM-Clients und -Standortserver Daten senden, sind diese verschlüsselt und geschützt.  

## <a name="client-communications"></a>Clientkommunikation

Die folgenden Standortsystemrollen an primären Standorten unterstützen Verbindungen von Clients, die sich an nicht vertrauenswürdigen Standorten befinden:

> [!NOTE]
> Während IBCM den Fokus hauptsächlich auf internetbasierte Szenarios legt, wird das gleiche Verhalten auf Clients in einer nicht vertrauenswürdigen Active Directory-Gesamtstruktur angewandt. Sekundäre Standorte unterstützen keine Clientverbindungen von nicht vertrauenswürdigen Standorten.

- Zertifikatregistrierungspunkt für das Configuration Manager-Richtlinienmodul (NDES)

- Verteilungspunkt

- Cloudbasierter Verteilungspunkt

- Anmeldungsproxypunkt

- Fallbackstatuspunkt

- Verwaltungspunkt

- Softwareupdatepunkt

> [!NOTE]
> Die Unterstützung für die Anwendungskatalogrollen endete mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). Für Configuration Manager-Versionen 1906 und früher, die weiterhin unterstützt werden, kann der Anwendungskatalog-Websitepunkt Verbindungen von internetbasierten Clients akzeptieren.

### <a name="about-internet-facing-site-systems"></a>Informationen zu Standortsystemen mit Internetzugriff

Eine Vertrauensstellung zwischen der Gesamtstruktur eines Clients und des Standortsystemservers ist nicht erforderlich. Wenn die Gesamtstruktur jedoch mit einem Standortsystem mit Internetzugriff der Gesamtstruktur vertraut, die die Benutzerkonten enthält, unterstützt diese Konfiguration benutzerbasierte Richtlinien für Geräte im Internet, wenn Sie die **Clientrichtlinie**-Clienteinstellung **Benutzerrichtlinienanforderungen von Internetclients aktivieren** aktivieren.

Aus den nachstehenden Konfigurationsbeispielen geht hervor, unter welchen Umständen Benutzerrichtlinien für Geräte im Internet von der IBCM unterstützt werden:

- Der internetbasierte Verwaltungspunkt befindet sich im Umkreisnetzwerk. Dieses Netzwerk verfügt auch über einen schreibgeschützten Domänencontroller zum Authentifizieren des Benutzers. Eine Firewall zwischen dem Umkreisnetzwerk und den internen Netzwerken lässt Active Directory-Pakete zu.

- Das Benutzerkonto befindet sich in der intranetbasierten Gesamtstruktur. Der internetbasierte Verwaltungspunkt befindet sich in der umkreisbasierten Gesamtstruktur. Die Umkreisgesamtstruktur vertraut der internen Gesamtstruktur. Eine Firewall zwischen dem Umkreisnetzwerk und den internen Netzwerken lässt die Authentifizierungspakete zu.

- Das Benutzerkonto und der internetbasierte Verwaltungspunkt befinden sich in der intranetbasierten Gesamtstruktur. Sie veröffentlichen den Verwaltungspunkt über einen Webproxyserver im Internet.

### <a name="use-a-web-proxy-server"></a>Verwenden eines Webproxyservers

Sie können internetbasierte Standortsysteme im Intranet platzieren, wenn Sie diese über einen Webproxyserver im Internet veröffentlichen. Konfigurieren Sie diese Standortsysteme nur für Clientverbindungen aus dem Internet oder sowohl für Clientverbindungen aus dem Internet als auch für Clientverbindungen aus dem Intranet. Einen Webproxyserver können Sie für SSL-zu-SSL-Bridging (Secure Sockets Layer) oder SSL-Tunneling konfigurieren.

#### <a name="ssl-bridging-to-ssl"></a>SSL-zu-SSL-Bridging

SSL-zu-SSL-Bridging ist die empfohlene und sicherere Konfiguration, da die SSL-Beendigung mit Authentifizierung verwendet wird. Sie authentifiziert Clientcomputer mit der Computerauthentifizierung. SSL-Bridging wird von mobilen Geräten, die Sie mithilfe von Configuration Manager registriert haben, nicht unterstützt.

Mit SSL-Beendigung auf dem Proxy werden Pakete aus dem Internet überprüft, bevor diese zum internen Netzwerk weitergeleitet werden. Die vom Client eingehende Verbindung wird vom Proxy authentifiziert und beendet. Anschließend wird eine neue authentifizierte Verbindung mit dem internetbasierten Standortsystem hergestellt. Wenn Configuration Manager-Clients einen Proxy verwenden, ist dessen Identität (GUID) sicher im Client in der Paketnutzlast enthalten. Der Proxy wird vom Verwaltungspunkt nicht als Client angesehen. Configuration Manager unterstützt kein HTTP-zu-HTTPS- oder HTTPS-zu-HTTP-Bridging.

> [!NOTE]
> Configuration Manager bietet keine Unterstützung, SSL-Bridgingkonfigurationen von Drittanbietern festzulegen. Beispiele: NetScaler von Citrix oder BIG-IP von F5. Wenden Sie sich an Hersteller Ihres Geräts, um es für die Verwendung mit Configuration Manager zu konfigurieren.

#### <a name="tunneling"></a>Tunneling

Wenn von Ihrem Proxywebserver die Voraussetzungen für die Unterstützung von SSL-Bridging nicht erfüllt werden, steht Ihnen als weitere Möglichkeit die Verwendung von SSL-Tunneling mit Configuration Manager zur Verfügung. Sie können auch SSL-Tunneling verwenden, um mobile Geräte zu unterstützen, die Sie mit Configuration Manager registrieren. Diese Option ist weniger sicher, da der Proxy die SSL-Pakete aus dem Internet ohne SSL-Beendigung an die Standortsysteme weiterleitet. Der Proxy überprüft die Pakete nicht auf schädlichen Inhalt. Bei der Verwendung von SSL-Tunneling müssen vom Proxywebserver keine Zertifikatanforderungen erfüllt werden.

## <a name="plan-for-internet-based-clients"></a>Planen internetbasierter Clients

Entscheiden Sie sich, ob Sie Ihre internetbasierten Clients für die Verwaltung sowohl im Intranet als auch im Internet oder für die reine Internetverwaltung konfigurieren möchten. Sie können diese Verwaltungsoption nur bei der Clientinstallation konfigurieren. Wenn Sie diese später ändern möchten, müssen Sie den Client neu installieren.

> [!NOTE]
> Wenn Sie einen Verwaltungspunkt für die Unterstützung internetbasierter Clients konfigurieren, werden Clients, die eine Verbindung mit dem Verwaltungspunkt herstellen, internetfähig, sobald sie zum nächsten Mal ihre Liste der verfügbaren Verwaltungspunkte aktualisieren.
>
> Sie müssen die Konfiguration der reinen Internetclientverwaltung nicht auf das Internet beschränken. Sie können diese auch im Intranet verwenden.

Bei Clients, die Sie nur für die reine Internetverwaltung konfigurieren, ist die Kommunikation nur mit Standortsystemen möglich, die Sie für Clientverbindungen aus dem Internet konfigurieren. Verwenden Sie diese Konfiguration in den folgenden Szenarios:

- Wenn Sie wissen, dass ein Computer niemals eine Verbindung mit Ihrem Intranet herstellen wird. Dazu zählen beispielsweise POS-Computer (Point-of-Sale) an Remotestandorten.
- Wenn Sie die Clientkommunikation auf HTTPS beschränken möchten. Grund hierfür kann beispielsweise die Unterstützung von Firewallsicherheitsrichtlinien oder eingeschränkten Sicherheitsrichtlinien sein.
- Wenn Sie internetbasierte Standortsysteme in einem Umkreisnetzwerk installieren und diese Server als Configuration Manager-Clients verwalten möchten.

> [!NOTE]
> Wenn Sie Arbeitsgruppenclients im Internet verwalten möchten, konfigurieren Sie diese für die reine Internetverwaltung.
>
> Wenn Sie ein mobiles Gerät so konfigurieren, dass es einen internetbasierten Verwaltungspunkt verwendet, wird es automatisch für die reine Internetverwaltung konfiguriert.

Sie können andere Clients sowohl für die Internet- als auch für die Intranetclientverwaltung konfigurieren. Wenn diese eine Netzwerkveränderung erkennen, wechseln sie automatisch zwischen der IBCM und der Intranetclientverwaltung. Falls eine Verbindung mit einem Verwaltungspunkt möglich ist, der Clientverbindungen im Intranet unterstützt, bzw. ein solcher Verwaltungspunkt gefunden wird, werden diese Clients als Intranetclients verwaltet. Intranetclients verfügen über den vollständigen Configuration Manager-Funktionsumfang. Falls keine Verbindung mit einem Verwaltungspunkt möglich ist, der Clientverbindungen im Intranet unterstützt, bzw. kein solcher Verwaltungspunkt gefunden wird, versuchen die Clients, eine Verbindung mit einem internetbasierten Verwaltungspunkt herzustellen. Wenn Sie damit Erfolg haben, werden diese Clients fortan von den internetbasierten Standortsystemen an ihrem zugewiesenen Standort verwaltet.

Der Vorteil des automatischen Wechsels liegt darin, dass Clients alle Funktionen verwenden können, wenn sie eine Verbindung mit dem Intranet herstellen. Bei einer Verbindung mit dem Internet erhalten sie zudem Zugriff auf wichtige Verwaltungsfunktionen. Downloads von Inhalten, die im Internet starten, können nahtlos im Intranet fortgesetzt werden und umgekehrt.

## <a name="prerequisites"></a>Voraussetzungen

Für die IBCM in Configuration Manager gelten die folgenden Abhängigkeiten:

- Clients benötigen eine Internetverbindung. Configuration Manager verwendet die bestehende Internetverbindung des Geräts. Mobile Geräte müssen über eine direkte Internetverbindung verfügen. Vollständige Clientcomputer benötigen entweder eine direkte Internetverbindung oder müssen eine Verbindung über einen Proxywebserver herstellen.

- Standortsysteme, die IBCM unterstützen, benötigen eine Internetverbindung und müssen sich in einer Active Directory-Domäne befinden. Für internetbasierte Standortsysteme ist keine Vertrauensstellung mit der Active Directory-Gesamtstruktur des Standortservers erforderlich. Wenn jedoch die Authentifizierung des Benutzers mithilfe der Windows-Authentifizierung durch den internetbasierten Verwaltungspunkt möglich ist, werden Benutzerrichtlinien unterstützt. Wenn bei der Windows-Authentifizierung ein Fehler auftritt, werden nur Geräterichtlinien unterstützt.

    > [!NOTE]
    > Aktivieren Sie zusätzlich die folgenden Clienteinstellungen in der Gruppe **Clientrichtlinie**, um Benutzerrichtlinien zu unterstützen:
    >
    > - **Benutzerrichtlinienabruf auf Clients aktivieren**
    > - **Benutzerrichtlinienanforderungen von Internetclients aktivieren**  

- Eine Public Key-Infrastruktur (PKI) zum Bereitstellen und Verwalten der erforderlichen Zertifikate für internetbasierte Client und Standortsystemserver. Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../plan-design/network/pki-certificate-requirements.md).

- Registrieren öffentlicher DNS-Hosteinträge für die Internet-FQDNs (vollqualifizierte Domänennamen) von Standortsystemen, die IBCM unterstützen

### <a name="client-communication-requirements"></a>Anforderungen an die Clientkommunikation

Beteiligte Firewalls oder Proxyserver müssen die Clientkommunikation für internetbasierte Standortsysteme zulassen:

- Unterstützung von HTTP 1.1  

- Zulassen des HTTP-Inhaltstyps mehrteiliger MIME-Anlagen (mehrteilige/gemischte und Anwendungs-/Oktettstream)  

#### <a name="verbs"></a>Verben

Lassen Sie die folgenden Verben für die internetbasierten Standortsystem-Serverrollen zu:

| Role-Eigenschaft | Verben |
|------|-------|
| Verwaltungspunkt | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| Verteilungspunkt | - HEAD<br>- GET<br>- PROPFIND |
| Fallbackstatuspunkt | POST |
| Anwendungskatalog-Websitepunkt | -POST<br>-GET |

#### <a name="http-headers"></a>HTTP-Header

Lassen Sie die folgenden HTTP-Header für die internetbasierten Standortsystem-Serverrollen zu:

| Role-Eigenschaft | HTTP-Header |
|------|--------------|
| Verwaltungspunkt | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Verteilungspunkt | Bereich: |

Informationen zu ähnlichen Kommunikationsanforderungen bei Verwendung des Softwareupdatepunkts für Clientverbindungen über das Internet finden Sie in der Dokumentation zu Windows Server Update Services (WSUS).

## <a name="unsupported-features"></a>Nicht unterstützte Funktionen

Nicht alle Clientverwaltungsfunktionen sind für das Internet geeignet. Configuration Manager unterstützt einige Funktionen für Clients im Internet nicht. Diese nicht unterstützten Funktionen beruhen in der Regel auf Active Directory Domain Services oder sind für ein öffentliches Netzwerk nicht geeignet.

Die folgenden Funktionen werden bei der Verwaltung von Clients mit IBCM über das Internet nicht unterstützt:

- Clientbereitstellung über das Internet, wie Clientpush und die auf Softwareupdates basierende Clientbereitstellung. Verwenden Sie die manuelle Clientinstallation.

- Automatische Standortzuweisung

- Wake-On-LAN

- Bereitstellung des Betriebssystems. Allerdings können Sie Tasksequenzen bereitstellen, die kein Betriebssystem bereitstellen.

- Remotesteuerung

- Softwarebereitstellung für Benutzer. Diese Funktion basiert auf dem Anwendungskatalog, der veraltet ist.

- Clientroaming. Mithilfe von Roaming kann von Clients immer der nächstgelegene Verteilungspunkt zum Herunterladen von Inhalt ermittelt werden. Eines der internetbasierten Standortsysteme wird auf nicht deterministische Weise und unabhängig von der Bandbreite oder vom physischen Standort von den Clients ausgewählt.

Wenn Sie einen Softwareupdatepunkt dahingehend konfigurieren, dass er Verbindungen aus dem Internet akzeptiert, werden internetbasierte Clients immer mit diesem Softwareupdatepunkt überprüft. Auf diese Weise wird festgestellt, welche Softwareupdates erforderlich sind. Wenn diese Clients mit dem Internet verbunden sind, versuchen sie immer zuerst, die Softwareupdates über Microsoft Update herunterzuladen, anstatt über einen internetbasierten Verteilungspunkt. Wenn dies nicht möglich ist, versuchen sie, die erforderlichen Softwareupdates über einen internetbasierten Verteilungspunkt herunterzuladen.

> [!TIP]
> Der Configuration Manager-Client bestimmt automatisch, ob er sich im Intranet oder im Internet befindet. Wenn der Client einen Domänencontroller oder einen lokalen Verwaltungspunkt kontaktieren kann, wird sein Verbindungstyp auf „Derzeit *Intranet*“ festgelegt. Andernfalls wechselt er zu „Derzeit *Internet*“ und kommuniziert mit den Standortsystemen, die seinem Standort zugewiesen sind.
