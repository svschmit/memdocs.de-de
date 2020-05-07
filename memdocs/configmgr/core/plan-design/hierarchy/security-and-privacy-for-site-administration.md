---
title: Sicherheit und Datenschutz für die Standortverwaltung
titleSuffix: Configuration Manager
description: Optimieren von Sicherheit und Datenschutz für die Standortverwaltung in Configuration Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182258"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Sicherheit und Datenschutz für die Standortverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält Sicherheits- und Datenschutzinformationen für Configuration Manager-Standorte und die Hierarchie.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a> Sicherheitsempfehlungen für die Standortverwaltung

Befolgen Sie die unten stehenden Empfehlungen, um Configuration Manager-Standorte und die Hierarchie zu sichern.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Ausführen von Setup aus einer vertrauenswürdigen Quelle und sichere Kommunikation

Führen Sie das Configuration Manager-Setup nur aus einer vertrauenswürdigen Quelle aus, um Manipulationen der Quelldateien zu vermeiden. Wenn Sie die Dateien im Netzwerk speichern, Sichern Sie den Speicherort im Netzwerk.  

Wenn Sie Setup von einem Speicherort im Netzwerk aus ausführen, verwenden Sie IPsec oder SMB-Signaturen zwischen dem Quellspeicherort der Setupdateien und dem Standortserver, um Manipulationen an den Dateien während der Übertragung über das Netzwerk zu verhindern.  

Wenn Sie das Setup-Downloadprogramm zum Herunterladen der für Setup erforderlichen Dateien verwenden, sichern Sie auch den Ort, an dem diese Dateien gespeichert werden. Sichern Sie auch den Kommunikationskanal mit diesem Speicherort, wenn Sie Setup ausführen.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Erweitern des Active Directory-Schemas und Veröffentlichen von Standorten in der Domäne  

Zum Ausführen von Configuration Manager sind keine Schemaerweiterungen erforderlich, sie bewirken jedoch eine sicherere Umgebung. Clients und Standortserver können Informationen aus einer vertrauenswürdigen Quelle abrufen.  

Stellen Sie bei Clients in einer nicht vertrauenswürdigen Domäne die folgenden Standortsystemrollen in den Domänen der Clients bereit:  

- Verwaltungspunkt  

- Verteilungspunkt  

> [!NOTE]  
> Eine vertrauenswürdige Domäne für den Configuration Manager erfordert Kerberos-Authentifizierung. Clients in einer anderen Gesamtstruktur ohne bidirektionale Vertrauensstellung mit der Gesamtstruktur des Standortservers werden als Clients in einer nicht vertrauenswürdigen Domäne betrachtet. Eine externe Vertrauensstellung ist für diesen Zweck nicht ausreichend.  

### <a name="use-ipsec-to-secure-communications"></a>Sichern der Kommunikation mithilfe von IPsec

Die Kommunikation zwischen Standortserver und dem Computer, auf dem SQL Server ausgeführt wird, wird von Configuration Manager gesichert. Die Kommunikation zwischen Standortsystemrollen und SQL Server wird von Configuration Manager jedoch nicht gesichert. Sie können nur einige Standortsysteme mit HTTPS für die standortinterne Kommunikation konfigurieren.  

Wenn Sie keine zusätzlichen Kontrollmaßnahmen zum Sichern dieser Kanäle zwischen Servern verwenden, können Angreifer verschiedene Spoofing- und Man-in-the-middle-Angriffe gegen Standortsysteme richten. Verwenden Sie SMB-Signaturen, wenn Sie IPsec nicht verwenden können.  

> [!Important]  
> Sichern Sie den Kommunikationskanal zwischen Standortserver und Paketquellserver. Diese Kommunikation erfolgt über SMB. Wenn Sie IPsec nicht verwenden können, um die Kommunikation zu sichern, verwenden Sie SMB-Signaturen, um zu gewährleisten, dass die Dateien nicht manipuliert sind, wenn sie von den Clients heruntergeladen und ausgeführt werden.  

### <a name="dont-change-the-default-security-groups"></a>Keine Änderungen der Standardsicherheitsgruppen

Nehmen Sie keine Änderungen an den folgenden Sicherheitsgruppen vor, die von Configuration Manager erstellt und für die Kommunikation im Standortsystem verwaltet werden:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;Standortcode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Standortcode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;Standortcode\>**  

Diese Sicherheitsgruppen werden von Configuration Manager automatisch erstellt und verwaltet. Dieses Verhalten schließt das Entfernen von Computerkonten ein, wenn eine Standortsystemrolle entfernt wird.  

Bearbeiten Sie diese Gruppen nicht manuell, um die Dienstkontinuität und das Prinzip der geringsten Berechtigungen nicht zu gefährden.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Verwalten des Bereitstellungsvorgangs für vertrauenswürdige Stammschlüssel

Wenn eine Abfrage von Configuration Manager-Informationen vom globalen Katalog durch die Clients nicht möglich ist, ist der vertrauenswürdige Stammschlüssel zur Authentifizierung gültiger Verwaltungspunkte erforderlich. Der vertrauenswürdige Stammschlüssel wird in der Clientregistrierung gespeichert. Er kann mithilfe der Gruppenrichtlinie festgelegt oder manuell konfiguriert werden.  

Wenn der Client beim ersten Kontakt mit einem Verwaltungspunkt keine Kopie des vertrauenswürdigen Stammschlüssels aufweist, wird dem ersten Verwaltungspunkt vertraut, mit dem kommuniziert wird. Sie können für den Client im Voraus einen vertrauenswürdigen Stammschlüssel bereitstellen, um das Risiko zu reduzieren, dass Clients von einem Angreifer an einen nicht autorisierten Verwaltungspunkt umgeleitet werden. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Verwenden Sie nicht die Standardportnummern

Die Verwendung anderer als die standardmäßigen Portnummern kann zusätzliche Sicherheit bieten. Sie erschweren es Angreifern, die Umgebung in Vorbereitung auf einen Angriff zu erkunden. Wenn Sie sich für die Verwendung von Portnummern entscheiden, die nicht der Standardeinstellung entsprechen, planen Sie diese Nummern, bevor Sie Configuration Manager installieren. Verwenden Sie diese Nummern konsistent in allen Standorten der Hierarchie. Portnummern, die nicht der Standardeinstellung entsprechen, können Sie beispielsweise als Clientanforderungsports und für Wake-On-LAN verwenden.  

### <a name="use-role-separation-on-site-systems"></a>Verwenden Sie die Rollentrennung für Standortsysteme

Sie können zwar sämtliche Standortsystemrollen auf einem einzigen Computer installieren, doch wird dieses Vorgehen in Produktionsnetzwerken selten verwendet. Damit wird ein Single Point of Failure erstellt.  

### <a name="reduce-the-attack-profile"></a>Verringern Sie die Angriffsfläche

Wenn Sie jede Standortserverrolle auf einem anderen Server installieren, reduzieren Sie damit das Risiko, dass ein Angriff gegen Schwachstellen in einem Standortsystem auch gegen ein anderes Standortsystem verwendet werden kann. Für viele Rollen ist die Installation von Internetinformationsdiensten (IIS) im Standortsystem erforderlich. Dadurch vergrößert sich die Angriffsfläche. Wenn Sie Rollen kombinieren müssen, um die Hardwareausgaben zu reduzieren, sollten Sie IIS-Rollen nur mit Rollen kombinieren, für die ebenfalls IIS erforderlich ist.  

> [!IMPORTANT]  
> Für die Fallbackstatuspunkt-Rolle gilt eine Ausnahme. Von dieser Standortsystemrolle werden nicht authentifizierte Daten von Clients akzeptiert, daher sollte die Fallbackstatuspunkt-Rolle niemals einer anderen Configuration Manager-Standortsystemrolle zugewiesen werden.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Konfigurieren Sie statische IP-Adressen für Standortsysteme

Statische IP-Adressen können leichter vor Namensauflösungsangriffen geschützt werden.  

Statische IP-Adressen erleichtern auch die Konfiguration von IPsec. Die Verwendung von IPsec ist eine bewährte Sicherheitsmethode zur Kommunikationssicherung zwischen Standortsystemen in Configuration Manager.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Installieren Sie keine anderen Anwendungen auf Standortsystemservern

Wenn Sie andere Anwendungen auf Standortsystemservern installieren, vergrößern Sie die Angriffsfläche von Configuration Manager. Damit riskieren Sie auch Kompatibilitätsprobleme.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Fordern Sie Signaturen an, und aktivieren Sie Verschlüsselung als Standortoption

Aktivieren Sie die Signierungs- und Verschlüsselungsoptionen für den Standort. Vergewissern Sie sich, dass der SHA-256-Hashalgorithmus von allen Clients unterstützt wird, und aktivieren Sie dann die Option **SHA-256 erforderlich**.  

### <a name="restrict-and-monitor-administrative-users"></a>Einschränken und Überwachen von Administratoren

Gewähren Sie nur vertrauenswürdigen Benutzern Administratorzugriff auf Configuration Manager. Befolgen Sie das Prinzip der minimal erforderlichen Berechtigungen, indem Sie die integrierten Sicherheitsrollen verwenden oder Sicherheitsrollen anpassen. Administratoren, die Software und Konfigurationen erstellen, ändern und bereitstellen, können in der Configuration Manager-Hierarchie möglicherweise Geräte steuern.  

Überwachen Sie kontinuierlich die Administratorzuweisungen und die Autorisierungsebenen, um erforderliche Änderungen zu überprüfen.  

Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Sichern von Configuration Manager-Sicherungen

Beim Wiederherstellen von Configuration Manager sind Informationen erforderlich, in denen auch Zertifikate und andere sensible Daten enthalten sind. Diese Daten könnten von Angreifern zur Identitätsvortäuschung verwendet werden.  

Verwenden Sie SMB-Signaturen oder IPsec, wenn Sie solche Daten im Netzwerk übertragen, und sichern Sie auch das Sicherungsverzeichnis.  

### <a name="secure-locations-for-exported-objects"></a>Sichere Speicherorte für exportierte Objekte

Sichern Sie beim Exportieren und Importieren von Objekten zwischen Configuration Manager-Konsole und einem Netzwerkspeicherort den Speicherort sowie den Netzwerkkanal.

Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.  

Verwenden Sie SMB-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der exportierten Daten zu hindern. Sichern Sie außerdem die Kommunikation zwischen dem Standortserver und dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird. Verwenden Sie IPsec zum Verschlüsseln der Daten im Netzwerk, um die Offenlegung von Informationen zu verhindern.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Manuelles Entfernen von Zertifikaten von ausgefallenen Servern

Wenn ein Standortsystem nicht richtig deinstalliert wird oder bei Funktionsausfall nicht wiederhergestellt werden kann, entfernen Sie die Configuration Manager-Zertifikate für diesen Server manuell von anderen Configuration Manager-Servern.

Zum Entfernen von Peervertrauen, das ursprünglich mit dem Standortsystem und den Standortsystemrollen erstellt wurde, entfernen Sie die Configuration Manager-Zertifikate für den ausgefallenen Server im Zertifikatspeicher **Vertrauenswürdige Personen** auf anderen Standortsystemservern manuell. Diese Aktion ist wichtig, wenn Sie den Server ohne Neuformatieren wiederverwenden.  

Weitere Informationen finden Sie unter [Kryptografische Steuerelemente für die Serverkommunikation](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Konfigurieren Sie internetbasierte Standortsysteme nicht als Brücke zum Umkreisnetzwerk

Konfigurieren Sie Standortsystemserver nicht so, dass sie mehrfach vernetzt und sowohl mit dem Umkreisnetzwerk als auch mit dem Intranet verbunden sind. Durch eine solche Konfiguration können von internetbasierten Standortsystemen zwar Clientverbindungen aus dem Internet und dem Intranet angenommen werden, aber es wird eine Sicherheitsgrenze zwischen dem Umkreisnetzwerk und dem Intranet aufgehoben.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Konfigurieren Sie den Standortserver für die Initiierung von Verbindungen mit Umkreisnetzwerken

Wenn sich ein Standortsystem in einem nicht vertrauenswürdigen Netzwerk (wie einem Umkreisnetzwerk) befindet, konfigurieren Sie den Standortserver für das Initiieren von Verbindungen mit dem Standortsystem.

Standardmäßig initiieren Standortsysteme Verbindungen mit dem Standortserver, um Daten zu übertragen. Diese Konfiguration kann ein Sicherheitsrisiko darstellen, wenn die Verbindungsinitiierung von einem nicht vertrauenswürdigen Netzwerk zum vertrauenswürdigen Netzwerk erfolgt. Wenn Standortsysteme Verbindungen aus dem Internet akzeptieren oder sich in einer nicht vertrauenswürdigen Gesamtstruktur befinden, legen Sie als Standortsystemoption **Verbindungen mit diesem Standortsystem müssen vom Standortserver hergestellt werden** fest. Nach dem Installieren des Standortsystems und der Rollen werden alle Verbindungen vom Standortserver aus dem vertrauenswürdigen Netzwerk initiiert.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Verwenden Sie SSL-Bridging und einen Tunnelabschluss mit Authentifizierung

Wenn Sie für die internetbasierte Clientverwaltung einen Webproxyserver verwenden, verwenden Sie SSL-zu-SSL-Bridging mit Tunnelabschluss und Authentifizierung.

Wenn Sie den SSL-Tunnelabschluss für den Proxywebserver konfigurieren, werden Pakete aus dem Internet überprüft, bevor sie an das interne Netzwerk weitergeleitet werden. Die vom Client eingehende Verbindung wird vom Proxywebserver authentifiziert und beendet, und dann wird eine neue authentifizierte Verbindung mit dem internetbasierten Standortsystem hergestellt.  

Wenn von Configuration Manager-Clientcomputern ein Proxywebserver verwendet wird, um eine Verbindung mit internetbasierten Standortsystemen herzustellen, wird die Clientidentität (GUID) sicher als Bestandteil der Paketnutzdaten transportiert. Der Proxywebserver wird vom Verwaltungspunkt nicht als Client angesehen.

Wenn von Ihrem Proxywebserver die Voraussetzungen für die Unterstützung von SSL-Bridging nicht erfüllt werden, steht Ihnen als weitere Möglichkeit die Verwendung von SSL-Tunneling zur Verfügung. Diese Option ist weniger sicher. Die SSL-Pakete aus dem Internet werden ohne Tunnelabschluss an die Standortsysteme weitergeleitet. Sie können dann nicht auf schädliche Inhalte überprüft werden.  

> [!WARNING]  
> SSL-Bridging kann von mobilen Geräten, die mithilfe von Configuration Manager registriert wurden, nicht verwendet werden. Sie müssen ausschließlich das SSL-Tunneling verwenden.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Empfohlene Konfigurationen, wenn Sie den Standort zum Aktivieren von Computern für die Softwareinstallation konfigurieren

- Wenn Sie herkömmliche Aktivierungspakete verwenden, bevorzugen Sie Unicast gegenüber subnetzgesteuerten Broadcasts.  

- Wenn subnetzgesteuerte Broadcasts verwendet werden müssen, konfigurieren Sie die Router so, dass IP-gesteuerte Broadcasts nur über den Standortserver und nur über eine nicht standardmäßig konfigurierte Portnummer möglich sind.  

Weitere Informationen zu den verschiedenen Wake-On-LAN-Technologien finden Sie unter [Planen der Clientaktivierung](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Wenn Sie E-Mail-Benachrichtigungen verwenden, konfigurieren Sie einen authentifizierten Zugriff auf den SMTP-E-Mail-Server

Verwenden Sie nach Möglichkeit einen Mailserver, der den authentifizierten Zugriff unterstützt. Verwenden Sie für die Authentifizierung das Computerkonto des Standortservers. Falls Sie ein Benutzerkonto für die Authentifizierung angeben müssen, verwenden Sie eines mit den geringsten Berechtigungen. 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>Erzwingen der LDAP-Kanalbindung und der LDAP-Signatur

Die Sicherheit von Active Directory-Domänencontrollern kann verbessert werden, indem der Server so konfiguriert wird, dass er SASL-LDAP-Bindungen (Simple Authentication and Security Layer) ablehnt, die keine Signatur anfordern, oder einfache LDAP-Bindungen ablehnt, die auf einer Klartextverbindung ausgeführt werden. Ab Version 1910 unterstützt Configuration Manager das Erzwingen der LDAP-Kanalbindung und der LDAP-Signatur. Weitere Informationen finden Sie unter [2020 LDAP-Kanalbindung und LDAP-Signaturanforderung für Windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> Sicherheitsempfehlungen für den Standortserver

Befolgen Sie die unten stehenden Empfehlungen, um den Configuration Manager-Standortserver zu sichern.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Installieren Sie Configuration Manager auf einem Mitgliedsserver anstatt auf einem Domänencontroller

Die Configuration Manager-Standortserver und -Standortsysteme müssen nicht auf einem Domänencontroller installiert werden. Domänencontroller verfügen neben der Domänendatenbank über keine andere lokale SAM-Datenbank (Security Accounts Management). Wenn Sie Configuration Manager auf einem Mitgliedsserver installieren, können Sie die Configuration Manager-Konten in der lokalen SAM-Datenbank anstelle der Domänendatenbank warten.  

Außerdem verringern Sie mit dieser Verfahrensweise die Angriffsfläche Ihrer Domänencontroller.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Installieren von sekundären Standorten ohne Kopieren der Dateien über das Netzwerk

Wenn Sie Setup ausführen und einen sekundären Standort erstellen, aktivieren Sie nicht die Option zum Kopieren der Dateien vom übergeordneten in den sekundären Standort. Verwenden Sie zudem keinen Quellspeicherort im Netzwerk. Wenn Sie Dateien über das Netzwerk kopieren, könnte ein geschickter Angreifer auf das Installationspaket des sekundären Standorts zugreifen und die darin enthaltenen Dateien vor der Installation manipulieren. Das Timing eines solchen Angriffs wäre jedoch schwierig. Dieses Risiko können Sie minimieren, indem Sie beim Übertragen der Dateien IPsec oder SMB verwenden.  

Kopieren Sie die Quelldateien auf dem sekundären Standortserver aus dem Medienordner in einen lokalen Ordner, anstatt sie über das Netzwerk zu kopieren. Wenn Sie dann das Setup ausführen, um einen sekundären Standort zu erstellen, wählen Sie auf der Seite **Installationsquelldateien** die Option **Quelldateien in folgendem lokalen Speicherort auf dem sekundären Standortcomputer verwenden (am sichersten)** aus, und geben Sie diesen Ordner an.  

Weitere Informationen finden Sie unter [Installieren eines sekundären Standorts](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>Die Installation der Standortrollen erbt Berechtigungen vom Laufwerksstamm

<!-- SCCMDocs#1380 -->
Sie müssen die Systemlaufwerksberechtigungen ordnungsgemäß konfigurieren, bevor Sie die erste Standortsystemrolle auf einem Server installieren. `C:\SMS_CCM` erbt beispielsweise Berechtigungen von `C:\`. Wenn das Stammverzeichnis des Laufwerks nicht ordnungsgemäß geschützt ist, können Benutzer mit geringen Rechten möglicherweise Inhalte im Configuration Manager-Ordner aufrufen oder ändern.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> Sicherheitsempfehlungen für SQL Server

Configuration Manager verwendet SQL Server als Back-End-Datenbank. Wenn die Datenbank beschädigt ist, können Angreifer Configuration Manager u. U. umgehen. Wenn Sie direkt auf SQL Server zugreifen, können Angriffe über Configuration Manager gestartet werden. Angriffe auf SQL Server müssen als hochriskant angesehen werden, und es müssen entsprechende Vorkehrungen getroffen werden.  

Befolgen Sie die unten stehenden Sicherheitsempfehlungen, um SQL Server für Configuration Manager zu sichern.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Verwenden Sie den Configuration Manager-Standortdatenbankserver nicht, um andere SQL Server-Anwendungen auszuführen

Je mehr Zugriffsmöglichkeiten auf den Configuration Manager-Standortdatenbankserver bestehen, desto größer ist das Risiko für Ihre Configuration Manager-Daten. Zudem sind auch andere Anwendungen auf dem gleichen SQL Server-Computer einem Risiko ausgesetzt, wenn die Configuration Manager-Standortdatenbank gefährdet ist.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Konfigurieren Sie SQL Server für die Verwendung der Windows-Authentifizierung

Der Zugriff von Configuration Manager auf die Standortdatenbank erfolgt zwar über ein Windows-Konto und mithilfe der Windows-Authentifizierung, aber es ist dennoch möglich, SQL Server für die Verwendung des gemischten Modus von SQL Server zu konfigurieren. Der gemischte SQL Server-Modus lässt zusätzliche SQL-Anmeldungen für den Zugriff auf die Datenbank zu. Eine solche Konfiguration ist nicht erforderlich, und sie vergrößert die Angriffsfläche.  

### <a name="update-sql-server-express-at-secondary-sites"></a>Aktualisieren von SQL Server Express an sekundären Standorten

Wenn Sie einen primären Standort installieren, wird SQL Server Express durch Configuration Manager vom Microsoft Download Center heruntergeladen. Die Dateien werden auf den primären Standortserver kopiert. Wenn Sie einen sekundären Standort installieren und die Option zum Installieren von SQL Server Express auswählen, wird die zuvor heruntergeladene Version von Configuration Manager installiert. Eine Prüfung, ob neue Versionen verfügbar sind, findet nicht statt. Führen Sie eines der folgenden Verfahren aus, um sicherzustellen, dass am sekundären Standort die neuesten Versionen verfügbar sind:  

- Führen Sie nach dem Installieren des sekundären Standorts Windows Update auf dem sekundären Standortserver aus.  

- Installieren Sie vor dem Installieren des sekundären Standorts SQL Server Express manuell auf dem sekundären Standortserver. Stellen Sie sicher, dass Sie die neueste Version und alle Softwareupdates installieren. Installieren Sie dann den sekundären Standort, und wählen Sie die Option zum Verwenden einer vorhandenen SQL Server-Instanz aus.  

Führen Sie Windows Update regelmäßig für alle installierten Versionen von SQL Server aus. Mit dieser Vorgehensweise wird sichergestellt, dass die neuesten Softwareupdates vorhanden sind.  

### <a name="follow-general-guidance-for-sql-server"></a>Befolgen Sie allgemeine Empfehlungen für SQL Server

Identifizieren und befolgen Sie die allgemeinen Empfehlungen für Ihre Version von SQL Server. Berücksichtigen Sie jedoch die folgenden Anforderungen für Configuration Manager:  

- Das Computerkonto des Standortservers muss Mitglied der Administratorgruppe auf dem Computer sein, auf dem SQL Server ausgeführt wird. Wenn Sie der SQL Server-Empfehlung nachkommen, die Administratorprinzipale explizit bereitzustellen, muss das Konto, das zur Ausführung von Setup auf dem Standortserver verwendet wird, Mitglied der SQL-Benutzergruppe sein.  

- Wenn Sie SQL Server mithilfe eines Domänenbenutzerkontos installieren, vergewissern Sie sich, dass das Computerkonto des Standortservers für einen Dienstprinzipalnamen (Service Principal Name, SPN), der in Active Directory Domain Services veröffentlicht wird, konfiguriert ist. Ohne den SPN treten bei der Kerberos-Authentifizierung und bei Configuration Manager-Setup Fehler auf.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> Sicherheitsempfehlungen für Standortsysteme, die IIS ausführen

Mehrere Standortsystemrollen in Configuration Manager erfordern IIS. Wenn Sie IIS sichern, ist ein ordnungsgemäßer Betrieb von Configuration Manager möglich, und das Gefahrenpotenzial in Bezug auf Sicherheitsprobleme wird verringert. Minimieren Sie die Anzahl der Server, für die IIS erforderlich sind. Führen Sie beispielsweise nur so viele Verwaltungspunkte aus, wie Sie für Ihre Client-Basis benötigen. Berücksichtigen Sie dabei Faktoren wie Hochverfügbarkeit und Netzwerkisolation für internetbasierte Clientverwaltung.  

Befolgen Sie die unten stehenden Empfehlungen, um Standortsysteme zu sichern, die IIS ausführen.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Deaktivieren Sie IIS-Funktionen, die Sie nicht benötigen

Installieren Sie nur einen minimalen IIS-Funktionsumfang für die Standortsystemrolle, die Sie installieren. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Konfigurieren Sie die Standortsystemrollen zum Erzwingen von HTTPS

Wenn Clients eine Verbindung mit einem Standortsystem über HTTP und nicht über HTTPS herstellen, verwenden sie die Windows-Authentifizierung. Ein solches Verhalten kann bewirken, dass anstelle der Kerberos-Authentifizierung die NTLM-Authentifizierung verwendet wird. In diesem Fall können von den Clients Verbindungen mit einem nicht autorisierten Server hergestellt werden.  

Eine Ausnahme von dieser Empfehlung können Verteilungspunkte darstellen. Paketzugriffspunkte funktionieren nicht, wenn der Verteilungspunkt für HTTPS konfiguriert ist. Bei Paketzugriffskonten erfolgt eine Autorisierung für den Inhalt, sodass Sie den Zugriff auf den Inhalt auf bestimmte Benutzer beschränken können. Weitere Informationen finden Sie unter [Security best practices for content management (Bewährte Sicherheitsmethoden für die Inhaltsverwaltung)](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Konfigurieren Sie für Standortsystemrollen eine Zertifikatvertrauensliste (Certificate Trust List, CTL) in IIS

Standortsystemrollen:  

- Ein Verteilungspunkt, der für HTTPS konfiguriert ist  

- Ein Verwaltungspunkt, der für HTTPS konfiguriert und für die Unterstützung von mobilen Geräten aktiviert ist

Eine Zertifikatvertrauensliste (Certificate Trust List, CTL) ist eine definierte Liste von vertrauenswürdigen Stammzertifizierungsstellen. Wenn Sie eine CTL mit einer Gruppenrichtlinie und einer PKI-Bereitstellung (Public Key-Infrastruktur) verwenden, können Sie mit einer CTL die vorhandenen vertrauenswürdigen Stammzertifizierungsstellen ergänzen, die im Netzwerk konfiguriert sind. Beispiele sind Zertifizierungsstellen, die automatisch mit Microsoft Windows installiert oder über Windows Enterprise-Stammzertifizierungsstellen hinzugefügt werden. Ist eine Zertifikatvertrauensliste in IIS konfiguriert, definiert sie eine Teilmenge dieser vertrauenswürdigen Stammzertifizierungsstellen.  

Mithilfe dieser Teilmenge können Sie die Sicherheit besser kontrollieren. Die CTL beschränkt die akzeptierten Clientzertifikate auf die Zertifikate, die von der Liste der Zertifizierungsstellen in der CTL ausgegeben wurden. Windows wird beispielsweise mit einer Anzahl von bekannten Zertifikaten von Drittanbieter-Zertifizierungsstellen geliefert, z. B. VeriSign und Thawte.

Standardmäßig stufen Computer mit ISS Zertifikate dieser bekannten Zertifizierungsstellen als vertrauenswürdig ein. Wenn Sie IIS nicht mit einer Zertifikatvertrauensliste für die aufgelisteten Standortsystemrollen konfigurieren, akzeptiert der Standort jedes Gerät als gültigen Client, das über ein von diesen Zertifizierungsstellen ausgestelltes Zertifikat verfügt. Wenn Sie IIS mit einer CTL konfigurieren, die diese Zertifizierungsstellen nicht enthält, lehnt der Standort Clientverbindungen ab, wenn eine Zertifikatkette mit diesen Zertifizierungsstellen vorliegt. Damit Configuration Manager-Clients für die aufgelisteten Standortsystemrollen zugelassen werden, müssen Sie IIS mit einer CTL konfigurieren, die die von Configuration Manager-Clients verwendeten Zertifizierungsstellen angibt.  

> [!NOTE]  
> Die Konfiguration einer Zertifikatvertrauensliste in IIS ist nur für die aufgelisteten Standortsystemrollen erforderlich. Für Clientcomputer, die mit HTTPS-Verwaltungspunkten verbunden werden, wird diese Funktionalität über die Liste der Zertifikataussteller bereitgestellt, die von Configuration Manager für Verwaltungspunkte verwendet wird.  

Weitere Informationen zum Konfigurieren einer Liste von vertrauenswürdigen Zertifizierungsstellen in IIS finden Sie in der IIS-Dokumentation.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Installieren Sie den Standortserver nicht auf einem Computer mit IIS

Mit der Rollentrennung verringern Sie die Angriffsfläche und verbessern die Wiederherstellbarkeit. Das Computerkonto des Standortservers verfügt in der Regel über Administratorrechte für alle Standortsystemrollen. Möglicherweise besitzt es auch Berechtigungen für Configuration Manager-C, wenn Sie die Clientpushinstallation verwenden.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Verwenden Sie dedizierte IIS-Server für Configuration Manager

Sie können zwar mehrere webbasierte Anwendungen auf den IIS-Servern hosten, die auch von Configuration Manager verwendet werden, doch durch dieses Vorgehen kann die Angriffsfläche erheblich vergrößert werden. Ein Angreifer könnte aufgrund einer unzureichend konfigurierten Anwendung die Kontrolle über ein Configuration Manager-Standortsystem gewinnen. In der Folge könnte der Angreifer auch die Kontrolle über die Hierarchie erlangen.  

Wenn Sie andere webbasierte Anwendungen auf Configuration Manager-Standortsystemen ausführen müssen, erstellen Sie eine benutzerdefinierte Website für Configuration Manager-Standortsysteme.  

### <a name="use-a-custom-website"></a>Verwenden Sie eine benutzerdefinierte Website

Sie können Configuration Manager für Standortsysteme, von denen IIS ausgeführt werden, so konfigurieren, dass anstelle der Standardwebsite eine benutzerdefinierte Website verwendet wird. Wenn das Ausführen anderer Webanwendungen auf dem Standortsystem erforderlich ist, müssen Sie eine benutzerdefinierte Website verwenden. Diese Einstellung ist nicht auf ein bestimmtes Standortsystem beschränkt, sondern gilt für den gesamten Standort.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Wenn Sie benutzerdefinierte Websites verwenden, entfernen Sie die virtuellen Standardverzeichnisse

Wenn Sie von der Standardwebsite zu einer benutzerdefinierten Website wechseln, werden die alten virtuellen Verzeichnisse nicht von Configuration Manager entfernt. Entfernen Sie die virtuellen Verzeichnisse, die ursprünglich von Configuration Manager unter der Standardwebsite erstellt wurden.  

Bei einem Verteilungspunkt müssen Sie beispielsweise die folgenden virtuellen Verzeichnisse entfernen:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Befolgen Sie die IIS-Server-Sicherheitsempfehlungen

Identifizieren und befolgen Sie die allgemeinen Empfehlungen für Ihre Version von IIS-Server. Berücksichtigen Sie alle Anforderungen, die unter Configuration Manager für bestimmte Standortsystemrollen gelten. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> Sicherheitsempfehlungen für den Verwaltungspunkt

Verwaltungspunkte sind die primäre Schnittstelle zwischen Geräten und Configuration Manager. Angriffe auf den Verwaltungspunkt und auf den Server, auf dem der Verwaltungspunkt ausgeführt wird, sind hochriskant. Es müssen daher entsprechende Vorkehrungen getroffen werden. Befolgen Sie alle entsprechenden Sicherheitsempfehlungen, und führen Sie eine Überwachung auf ungewöhnliche Aktivitäten hin aus.  

Befolgen Sie die unten stehenden Empfehlungen, um Verwaltungspunkte in Configuration Manager zu sichern.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>Weisen Sie den Client an einem Verwaltungspunkt demselben Standort zu

Achten Sie darauf, den Configuration Manager-Client eines Verwaltungspunkts ausschließlich dem Standort des Verwaltungspunkts zuzuweisen.  

Wenn Sie von einer früheren Version auf die Current Branch-Version von Configuration Manager migrieren, migrieren Sie den Client am Verwaltungspunkt baldmöglichst an den neuen Standort.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> Sicherheitsempfehlungen für den Fallbackstatuspunkt

Befolgen Sie die unten stehenden Sicherheitsempfehlungen, wenn Sie einen Fallbackstatuspunkt in Configuration Manager installieren:

Weitere Informationen zu den Sicherheitserwägungen beim Installieren eines Fallbackstatuspunkts finden Sie unter [Determine whether you require a fallback status point](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Führen Sie keine anderen Rollen im selben Standortsystem aus

Der Fallbackstatuspunkt ist darauf ausgelegt, nicht authentifizierte Kommunikation von beliebigen Computern zu akzeptieren. Wenn Sie diese Standortsystemrolle mit anderen Rollen oder einem Domänencontroller ausführen, steigt das Risiko für den Server erheblich.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Installieren Sie den Fallbackstatuspunkt, bevor Sie Clients mit PKI-Zertifikaten installieren

Wenn von den Configuration Manager-Standortsystemen keine HTTP-Clientkommunikation akzeptiert wird, bemerken Sie möglicherweise nicht, dass Clients ggf. aufgrund von Problemen mit PKI-Zertifikaten nicht verwaltet werden. Wenn Sie Clients einem Fallbackstatuspunkt zuweisen, melden sie diese Zertifikatprobleme über den Fallbackstatuspunkt.  

Aus Sicherheitsgründen können Sie Clients nach deren Installation keinen Fallbackstatuspunkt mehr zuweisen. Diese Rolle können Sie nur während der Installation der Clients zuweisen.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Verwenden Sie den Fallbackstatuspunkt nicht im Umkreisnetzwerk

Es ist beabsichtigt, dass Daten von beliebigen Clients vom Fallbackstatuspunkt akzeptiert werden. Durch das Platzieren des Fallbackstatuspunkts im Umkreisnetzwerk kann die Problembehandlung bei internetbasierten Clients erleichtert werden. Diesen Vorteil müssen Sie jedoch gegen die Risiken abwägen, die entstehen, wenn vom Standortsystem nicht authentifizierte Daten in einem öffentlich zugänglichen Netzwerk akzeptiert werden.  

Wenn Sie den Fallbackstatuspunkt im Umkreisnetzwerk oder in einem nicht vertrauenswürdigen Netzwerk installieren, konfigurieren Sie den Standortserver so, dass er Datenübertragungen initiiert. Übernehmen Sie nicht die Standardeinstellung, mit welcher dem Fallbackstatuspunkt ermöglicht wird, eine Verbindung mit dem Standortserver zu initiieren.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> Sicherheitsprobleme bei der Standortverwaltung

Überprüfen Sie die folgenden Sicherheitsprobleme für Configuration Manager:  

- In Configuration Manager ist kein Schutz gegen autorisierte Administratoren verfügbar, die Configuration Manager zum Angriff auf das Netzwerk verwenden. Nicht autorisierte Administratoren stellen ein erhebliches Sicherheitsrisiko dar. Sie könnten viele Angriffe starten, u. a. durch folgende Strategien:  

    - Verwenden der Softwarebereitstellung zum automatischen Installieren und Ausführen von Schadsoftware auf jedem Configuration Manager-Clientcomputer in der Organisation  

    - Verwenden der Remotesteuerung zum Steuern eines Configuration Manager-Clients ohne dessen Erlaubnis  

    - Konfigurieren schneller Abrufintervalle und extrem großer Inventarmengen Durch eine solche Aktion werden Denial-of-Service-Angriffe gegen Clients und Server bewirkt.  

    - Verwenden eines Standorts der Hierarchie, um in die Active Directory-Daten eines anderen Standorts zu schreiben  

    Die Standorthierarchie ist die Sicherheitsgrenze. Betrachten Sie Standorte nur als Verwaltungsgrenzen.  

    Überwachen Sie alle Administratoraktivitäten, und überprüfen Sie die Überwachungsprotokolle regelmäßig. Unterziehen Sie alle Configuration Manager-Administratoren vor der Einstellung einer zwingenden Hintergrundüberprüfung. Machen Sie regelmäßige erneute Überprüfungen zur Bedingung für die Beschäftigung.  

- Wenn der Anmeldungspunkt gefährdet ist, können Angreifer Zertifikate für die Authentifizierung abrufen. Sie können zudem Anmeldeinformationen von Benutzern stehlen, die ihre mobilen Geräte registrieren.  

    Der Anmeldungspunkt kommuniziert mit einer Zertifizierungsstelle. Active Directory Objekte können erstellt, geändert und gelöscht werden. Installieren Sie einen Anmeldungspunkt niemals im Umkreisnetzwerk. Überwachen Sie ihn laufend auf ungewöhnliche Aktivitäten.  

- Wenn Sie Benutzerrichtlinien für die internetbasierte Clientverwaltung zulassen, vergrößern Sie die potenzielle Angriffsfläche.  

    Bei diesen Konfigurationen werden Verbindungen zwischen Clients und Server über PKI-Zertifikate hergestellt, und es ist zudem eine Windows-Authentifizierung erforderlich. Möglicherweise wird anstelle der Kerberos-Authentifizierung die NTLM-Authentifizierung verwendet. Die NTLM-Authentifizierung ist anfällig für Identitätswechsel und Wiederholungsangriffe. Sie müssen Verbindungen zwischen dem internetbasierten Standortsystem und einem Domänencontroller zulassen, um Benutzer im Internet erfolgreich zu authentifizieren.  

- Auf Standortsystemservern ist die Freigabe **Admin$** erforderlich.  

    Der Configuration Manager-Standortserver verwendet die Admin$-Freigabe, um eine Verbindung mit Standortsystemen herzustellen und Dienstvorgänge auf diesen auszuführen. Sie dürfen diese Freigabe nicht deaktivieren oder entfernen.  

- Configuration Manager stellt Verbindungen mit anderen Computern mithilfe von Namensauflösungsdiensten her. Diese Dienste sind gegen die folgenden Sicherheitsangriffe schwer zu sichern:
    - Spoofing
    - Manipulation
    - Verfälschung
    - Offenlegung von Informationen
    - Denial of Service
    - Rechteerweiterungen

    Identifizieren und befolgen Sie Sicherheitsempfehlungen für die DNS-Version, die Sie zur Namensauflösung verwenden.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> Datenschutzinformationen zur Ermittlung

Bei der Ermittlung werden Datensätze für Netzwerkressourcen erstellt und in der Configuration Manager-Datenbank gespeichert. Discovery Data Records (DDRs) enthalten Computerinformationen wie IP-Adressen, Betriebssystemversionen und Computernamen. Sie können auch Active Directory-Ermittlungsmethoden so konfigurieren, dass sämtliche von Ihrer Organisation in Active Directory Domain Services gespeicherten Informationen zurückgegeben werden.  

Die einzige Ermittlungsmethode, die von Configuration Manager standardmäßig aktiviert wird, ist die Frequenzermittlung. Von dieser Methode wird eine Ermittlung nur für Computer durchgeführt, auf denen die Configuration Manager-Clientsoftware bereits installiert ist.  

Die Ermittlungsdaten werden nicht direkt an Microsoft gesendet. Sie werden in der Configuration Manager-Datenbank gespeichert. Configuration Manager behält Informationen in der Datenbank bei, bis die Daten gelöscht werden. Dieser Vorgang wird alle 90 Tage durch die Standortwartungsaufgabe **Veraltete Ermittlungsdaten löschen**.  
