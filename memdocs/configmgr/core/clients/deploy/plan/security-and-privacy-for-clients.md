---
title: Sicherheit und Datenschutz für Clients
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Sicherheit und Datenschutz für Konfigurations-Manager-Clients.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4922502b49ab2da9ce393fab809e4dc583fd962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694838"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Sicherheit und Datenschutz für Konfigurations-Manager-Clients

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält Informationen zu Sicherheit und Datenschutz für Konfigurations-Manager-Clients. Außerdem enthält er Informationen zu mobilen Geräten, die vom [Exchange Server-Connector](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) verwaltet werden.  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a> Bewährte Sicherheitsmethoden für Clients  

Der Configuration Manager-Standort akzeptiert Daten von Geräten, die den Konfigurations-Manager-Client ausführen. Dieses Verhalten macht den Standort anfällig für Angriffe durch Clients. Beispielsweise könnten falsch formatierte Inventurdaten gesendet werden, und auch eine Überlastung der Standortsysteme wäre möglich. Stellen Sie den Configuration Manager-Client nur auf vertrauenswürdigen Geräten bereit. Schützen Sie den Standort außerdem anhand der folgenden bewährten Sicherheitsmethoden vor nicht autorisierten oder gefährdeten Geräten:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Verwenden von PKI-Zertifikaten (Public Key-Infrastruktur) für die Clientkommunikation mit Standortsystemen, auf denen Internetinformationsdienste (IIS) ausgeführt werden  

- Legen Sie unter **Einstellungen des Standortsystems** die Option **Nur HTTPS**als Standorteigenschaft fest.  

- Installieren Sie Clients mit der CCMSetup-Eigenschaft `UsePKICert`.  

- Verwenden Sie eine Zertifikatsperrliste (Certificate Revocation List, CRL), und sorgen Sie dafür, dass sie stets für Clients und kommunizierende Servern zugänglich ist.  

Clients für mobile Geräte und manche internetbasierte Clients erfordern diese Zertifikate. Microsoft empfiehlt diese Zertifikate für alle Clientverbindungen im Intranet.  

Weitere Informationen zu den PKI-Zertifikatanforderungen und deren Verwendung zum Schutz von Configuration Manager finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Genehmigen Sie Clientcomputer aus vertrauenswürdigen Domänen automatisch, und überprüfen und genehmigen Sie andere Computer manuell.  

Falls Sie die PKI-Authentifizierung nicht verwenden können, geben Sie durch die Genehmigung an, dass ein von Ihnen als vertrauenswürdig eingestufter Computer von Configuration Manager verwaltet werden soll. Die Hierarchie bietet die folgenden Optionen zur Konfiguration der Clientgenehmigung:  

- Manuell
- Automatisch für Computer in vertrauenswürdigen Domänen
- Automatisch für alle Computer  

Die sicherste Genehmigungsmethode ist die automatische Genehmigung von Clients, die Mitglieder einer vertrauenswürdigen Domäne sind. Überprüfen und genehmigen Sie anschließend manuell alle anderen Computer. Die automatische Genehmigung aller Clients ist nur dann empfehlenswert, wenn Sie über andere Zugriffssteuerungsmethoden verfügen, mit denen Sie verhindern können, dass nicht vertrauenswürdige Computer auf das Netzwerk zugreifen.  

Weitere Informationen zum manuellen Genehmigen von Computern finden Sie unter [Verwalten von Clients mithilfe des Knotens „Geräte“](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Verlassen Sie sich nicht nur auf das Blockieren, um den Zugriff von Clients auf die Configuration Manager-Hierarchie zu verhindern  

Blockierte Clients werden von der Configuration Manager-Infrastruktur abgelehnt. Wenn Clients blockiert sind, können sie nicht mit Standortsystemen kommunizieren, um Richtlinien herunterzuladen, Inventurdaten hochzuladen oder Zustands- bzw. Statusmeldungen zu senden.

Das Blockieren ist auf die folgenden Szenarios ausgerichtet:

- Blockieren verlorener oder gefährdeter Bootmedien beim Bereitstellen eines Betriebssystems für Clients
- Wenn alle Standortsysteme HTTPS-Clientverbindungen akzeptieren

Wenn Standortsysteme HTTP-Clientverbindungen akzeptieren, sollten Sie sich aber nicht darauf verlassen, dass das Blockieren einen ausreichenden Schutz der Configuration Manager-Hierarchie vor nicht vertrauenswürdigen Computern darstellt. In diesem Fall könnte ein blockierter Client mit einem selbstsignierten Zertifikat und einer Hardware-ID dem Standort wieder hinzugefügt werden.

Die Zertifikatsperrung ist die erste Verteidigungslinie gegen möglicherweise gefährdete Zertifikate. Eine Zertifikatsperrliste (Certificate Revocation List, CRL) ist nur über eine Public Key-Infrastruktur (PKI) verfügbar. Das Blockieren von Clients in Configuration Manager bietet eine zweite Stufe der Verteidigung, mit der die Standorthierarchie geschützt wird.  

Weitere Informationen finden Sie unter [Bestimmen, ob Clients blockiert werden sollen](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Verwenden der sichersten Clientinstallationsmethoden, die für Ihre Umgebung geeignet sind  

- Bei Domänencomputern sind die gruppenrichtlinienbasierte Clientinstallation und die softwareupdatebasierte Clientinstallationsmethode sicherer als die Clientpushinstallation.  

- Verwenden Sie die Imageerstellung und manuelle Installationsmethoden, wenn Sie die Zugriffs- und Änderungssteuerung anwenden.  

- Verwenden Sie in Version 1806 oder höher die gegenseitige Kerberos-Authentifizierung mit Clientpushinstallation.  

Von allen Clientinstallationsmethoden bietet die Clientpushinstallation aufgrund ihrer vielen Abhängigkeiten die geringste Sicherheit. Diese Abhängigkeiten schließen lokale Administratorberechtigungen, die admin$-Freigabe und Firewallausnahmen ein. Die Anzahl und der Typ dieser Abhängigkeiten vergrößert die Angriffsfläche.  

Ab Version 1806 kann der Standort bei der Verwendung von Clientpush gegenseitige Kerberos-Authentifizierung erfordern, indem vor dem Herstellen der Verbindung kein Fallback auf NTLM zugelassen wird. Diese Verbesserung sichert die Kommunikation zwischen dem Server und dem Client. Weitere Informationen finden Sie unter [Installieren von Clients mittels Clientpush](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->  

Weitere Informationen zu den verschiedenen Clientinstallationsmethoden finden Sie unter [Clientinstallationsmethoden](client-installation-methods.md).  

Wählen Sie möglichst immer eine Clientinstallationsmethode aus, die am wenigsten Sicherheitsberechtigungen in Configuration Manager erfordert. Schränken Sie Administratoren, denen Sicherheitsrollen zugewiesen werden, durch Berechtigungen ein, die für andere Zwecke als die Clientbereitstellung verwendet werden können. Beispielsweise ist für das Konfigurieren eines automatischen Clientupdates die Sicherheitsrolle **Hauptadministrator** erforderlich, die einem Administrator sämtliche Sicherheitsberechtigungen erteilt.  

Weitere Informationen zu den Abhängigkeiten und Sicherheitsberechtigungen für jede Clientinstallationsmethode finden Sie im Abschnitt „Installationsmethodenabhängigkeiten“ unter [Voraussetzungen für Computerclients](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Falls Sie die Clientpushinstallation verwenden müssen, ergreifen Sie weitere Maßnahmen zum Schutz des Clientpushinstallationskontos.  

Dieses Konto muss ein Mitglied der lokalen Gruppe **Administratoren** auf jedem Computer sein, auf dem der Konfigurations-Manager-Client installiert wird. Fügen Sie das Clientpushinstallationskonto nie der Gruppe **Domänenadministratoren** hinzu. Erstellen Sie stattdessen eine globale Gruppe, und fügen Sie diese globale Gruppe der lokalen Gruppe **Administratoren** auf den Clients hinzu. Erstellen Sie ein Gruppenrichtlinienobjekt, um eine Einstellung für eingeschränkte Gruppen hinzuzufügen, mit der das Clientpushinstallationskonto der lokalen Gruppe **Administratoren** hinzugefügt wird.  

Erstellen Sie für zusätzliche Sicherheit mehrere Clientpushinstallationskonten, die alle Administratorzugriff auf eine begrenzte Anzahl Computer haben. Wenn ein Konto gefährdet ist, sind nur die Clientcomputer gefährdet, auf die dieses Konto Zugriff hat.  

### <a name="remove-certificates-before-imaging-clients"></a>Entfernen von Zertifikaten vor der Erstellung eines Clientimages  

Wenn Sie Clients mithilfe von Betriebssystemimages bereitstellen, sollten Sie vor der Aufzeichnung des Images immer Zertifikate entfernen. Dies können unter anderem PKI-Zertifikate für die Clientauthentifizierung und selbstsignierte Zertifikate sein. Wenn Sie diese Zertifikate nicht entfernen, können Clients gegenseitig die Identität wechseln. Es ist nicht möglich, die Daten für jeden Client zu überprüfen.  

Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Sicherstellen, dass die Configuration Manager-Computerclients eine autorisierte Kopie dieser Zertifikate erhalten  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Das Zertifikat für den vertrauenswürdigen Configuration Manager-Stammschlüssel  

Wenn beide der folgenden Aussagen zutreffen, verwenden Clients den vertrauenswürdigen Stammschlüssel von Configuration Manager zur Authentifizierung gültiger Verwaltungspunkte:  

- Sie haben das Active Directory-Schema für Configuration Manager nicht erweitert
- Clients verwenden keine PKI-Zertifikate bei der Kommunikation mit Verwaltungspunkten  

In diesem Fall kann nur mit dem vertrauenswürdigen Stammschlüssel festgestellt werden, ob ein Verwaltungspunkt in der Hierarchie als vertrauenswürdig eingestuft ist. Ohne den vertrauenswürdigen Stammschlüssel könnten Clients von einem geschickten Angreifer an einen nicht autorisierten Verwaltungspunkt weitergeleitet werden.  

Wenn der vertrauenswürdige Configuration Manager-Stammschlüssel nicht aus dem globalen Katalog oder mithilfe von PKI-Zertifikaten heruntergeladen werden kann, stellen Sie den Clients den vertrauenswürdigen Stammschlüssel vorab bereit. Hierdurch wird sichergestellt, dass sie nicht an nicht autorisierte Verwaltungspunkte weitergeleitet werden. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>Signaturzertifikat des Standortservers  

Clients verwenden dieses Zertifikat, um zu überprüfen, ob die von einem Verwaltungspunkt heruntergeladene Richtlinie vom Standortserver signiert wurde. Dieses Zertifikat ist ein selbstsigniertes Zertifikat des Standortservers und wird in den Active Directory-Domänendiensten veröffentlicht.  

Wenn Clients das Signaturzertifikat des Standortservers nicht aus dem globalen Katalog herunterladen können, wird es standardmäßig vom Verwaltungspunkt heruntergeladen. Wenn der Verwaltungspunkt in einem nicht vertrauenswürdigen Netzwerk wie dem Internet verfügbar gemacht wird, installieren Sie das Signaturzertifikat des Standortservers manuell auf Clients. Dadurch wird sichergestellt, dass sie keine manipulierten Clientrichtlinien von einem gefährdeten Verwaltungspunkt herunterladen können.  

Verwenden Sie in CCMSetup die **client.msi**-Eigenschaft SMSSIGNCERT, um das Signaturzertifikat des Standortservers manuell zu installieren. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../about-client-installation-properties.md).  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Keine Verwendung der automatischen Standortzuweisung, wenn der vertrauenswürdige Stammschlüssel vom ersten Verwaltungspunkt heruntergeladen wird, mit dem der Client eine Verbindung herstellt  

Verwenden Sie die automatische Standortzuweisung nur in folgenden Szenarios, um dem Risiko vorzubeugen, dass der vertrauenswürdige Stammschlüssel durch den Client von einem nicht autorisierten Verwaltungspunkt heruntergeladen wird:  

- Der Client kann auf Configuration Manager-Standortinformationen zugreifen, die in Active Directory Domain Services veröffentlicht sind.  

- Sie stellen den vertrauenswürdigen Stammschlüssel für den Client im Voraus bereit.  

- Sie verwenden PKI-Zertifikate von einer Unternehmenszertifizierungsstelle, um eine Vertrauensstellung zwischen Client und Verwaltungspunkt herzustellen.  

Weitere Informationen zum vertrauenswürdigen Stammschlüssel finden Sie unter [Planen des vertrauenswürdigen Stammschlüssels](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Installieren Sie Clientcomputer mit der Client.msi-Option SMSDIRECTORYLOOKUP=NoWINS für CCMSetup.  

Die sicherste Dienstidentifizierungsmethode zur Suche nach Standorten und Verwaltungspunkten ist die Verwendung der Active Directory-Domänendienste. In manchen Fällen ist diese Methode in manchen Umgebungen nicht möglich. Beispielsweise wenn Sie das Active Directory-Schema für Configuration Manager nicht erweitern können, oder wenn Clients sich in einer nicht vertrauenswürdigen Gesamtstruktur oder Arbeitsgruppe befinden. Wenn diese Methode nicht möglich ist, können Sie die DNS-Veröffentlichung als alternative Dienstidentifizierungsmethode verwenden. Wenn keine dieser Methoden erfolgreich, und der Verwaltungspunkt nicht für HTTPS-Clientverbindungen konfiguriert ist, können Clients auf WINS ausweichen.  

Die Veröffentlichung auf WINS ist nicht so sicher wie die anderen Veröffentlichungsmethoden. Konfigurieren Sie Clientcomputer so, dass diese nicht auf die Verwendung von WINS ausweichen, indem Sie **SMSDIRECTORYLOOKUP=NoWINS** angeben. Wenn Sie WINS als Dienstidentifizierung verwenden möchten, geben Sie **SMSDIRECTORYLOOKUP=WINSSECURE** an. Dies ist die Standardeinstellung. Hier wird der vertrauenswürdige Configuration Manager-Stammschlüssel verwendet, um das selbstsignierte Zertifikat des Verwaltungspunkts zu überprüfen.  

> [!NOTE]  
> Wenn Sie den Client für **SMSDIRECTORYLOOKUP=WINSSECURE** konfigurieren und über WINS ein Verwaltungspunkt gefunden wird, überprüft der Client die Kopie des vertrauenswürdigen Configuration Manager-Stammschlüssels in WMI.  
>
> Wenn die Signatur des Verwaltungspunktzertifikats mit der Clientkopie des vertrauenswürdigen Stammschlüssels übereinstimmt, ist das Zertifikat gültig. Nach Überprüfung des Zertifikats stellt der Client die Kommunikation mit dem mithilfe von WINS gefundenen Verwaltungspunkt her.  
>
> Wenn die Signatur des Verwaltungspunktzertifikats nicht mit der Clientkopie des vertrauenswürdigen Stammschlüssels übereinstimmt, ist das Zertifikat ungültig. In diesem Fall kommuniziert der Client nicht mit dem Verwaltungspunkt, der mithilfe von WINS gefunden wurde.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Achten Sie darauf, dass die Wartungsfenster für die Bereitstellung wichtiger Softwareupdates groß genug sind.  

Wartungsfenster für Gerätesammlungen beschränken die Zeitpunkte, zu denen Software von Configuration Manager auf diesen Geräten installiert werden kann. Wenn Sie das Wartungsfenster zu klein konfigurieren, kann der Client möglicherweise keine wichtigen Softwareupdates installieren. Durch dieses Verhalten ist der Client anfällig für Angriffe, die durch das Softwareupdate verhindert werden könnten.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Zusätzliche Sicherheitsvorkehrungen zur Reduzierung der Angriffsfläche auf Windows Embedded-Geräten mit Schreibfiltern  

Wenn Sie Schreibfilter auf Windows Embedded-Geräten aktivieren, werden die Softwareinstallationen oder -änderungen nur in der Überlagerung vorgenommen. Diese Änderungen werden nicht beibehalten, wenn das Gerät neu startet. Wenn Sie Configuration Manager verwenden, um Schreibfilter zu deaktivieren, ist das Embedded-Gerät während dieser Zeit nicht gegen Änderungen an allen Volumes geschützt. Diese Volumes schließen freigegebene Ordner ein.  

Configuration Manager sperrt den Computer während dieses Zeitraums, sodass sich nur lokale Administratoren anmelden können. Treffen Sie wann immer möglich weitere Sicherheitsvorkehrungen, um den Computer zu schützen. Aktivieren Sie z.B. weitere Einschränkungen in der Firewall.  

Wenn Sie Wartungsfenster verwenden, um Änderungen beizubehalten, sollten Sie diese Fenster sorgfältig planen. Minimieren Sie die Zeit, in der Schreibfilter deaktiviert sind, aber planen Sie genug Zeit für Softwareinstallationen und Neustarts ein.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Verwenden der aktuellen Clientversion mit auf Softwareupdate basierender Clientinstallation

Falls Sie eine auf Softwareupdate basierende Clientinstallation verwenden und eine spätere Version des Clients am Standort installieren, aktualisieren Sie das veröffentlichte Softwareupdate. Dadurch erhalten die Clients die aktuelle Version des Softwareupdatepunkts.  

Wenn Sie den Standort aktualisieren, wird das Softwareupdate für die Clientbereitstellung, das am Softwareupdatepunkt veröffentlicht ist, nicht automatisch aktualisiert. Veröffentlichen Sie den Konfigurations-Manager-Client erneut am Softwareupdatepunkt, und aktualisieren Sie die Versionsnummer.  

Weitere Informationen finden Sie unter [Installieren von Clients mithilfe auf einem Softwareupdate basierenden Installation](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>BitLocker-PIN-Eingabe nur auf vertrauenswürdigen Geräten und Geräten mit beschränktem Zugriff anhalten  

Legen Sie die Clienteinstellung **BitLocker-PIN-Eingabe bei Neustart anhalten** nur bei Computern, die Sie als vertrauenswürdig einstufen und auf die der physische Zugriff beschränkt ist, auf **Immer** fest.

Wenn Sie diese Einstellung auf **Immer** festlegen, kann Configuration Manager die Installation der Software abschließen. Durch dieses Verhalten können wichtige Softwareupdates installiert und der Dienst fortgesetzt werden. Wenn der Neustart von einem Angreifer abgefangen wird, könnte dieser den Computer unter seine Kontrolle bringen. Verwenden Sie diese Einstellung nur, wenn Sie den Computer als vertrauenswürdig einstufen und wenn der physische Zugriff auf den Computer beschränkt ist. Beispielsweise eignet sich diese Einstellung möglicherweise für Server in einem Rechenzentrum.  

Weitere Informationen zu dieser Clienteinstellung finden Sie unter [Informationen zu Clienteinstellungen](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>Keine Umgehung der PowerShell-Ausführungsrichtlinie

Wenn Sie die Einstellung des Konfigurations-Manager-Clients für die **PowerShell-Ausführungsrichtlinie** auf **Umgehung** festlegen, erlaubt Windows die Ausführung unsignierter PowerShell-Skripts. Dieses Verhalten könnte die Ausführung von Malware auf Clientcomputern ermöglichen. Wenn Ihre Organisation diese Option benötigt, verwenden Sie eine benutzerdefinierte Clienteinstellung. Weisen Sie sie nur den Clientcomputern zu, die unsignierte PowerShell-Skripts ausführen müssen.  

Weitere Informationen zu dieser Clienteinstellung finden Sie unter [Informationen zu Clienteinstellungen](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a> Bewährte Sicherheitsmethoden für mobile Geräte  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Installieren des Anmeldungsproxypunkts in einem Umkreisnetzwerk und des Anmeldungspunkts im Intranet  

Installieren Sie für internetbasierte mobile Geräte, die Sie mit Configuration Manager registrieren, den Anmeldungsproxypunkt in einem Umkreisnetzwerk und den Anmeldungspunkt im Intranet. Diese Rollentrennung trägt zum Schutz des Anmeldungspunkts vor Angriffen bei. Wenn Angreifer den Anmeldungspunkt gefährden, können sie Zertifikate für die Authentifizierung abrufen. Sie können ebenfalls Anmeldeinformationen von Benutzern stehlen, die ihre mobilen Geräte registrieren.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Konfigurieren der Kennworteinstellungen zum Schutz mobiler Geräte vor nicht autorisiertem Zugriff  

*Für mobile Geräte, die mithilfe von Configuration Manager registriert werden:* Verwenden Sie ein Konfigurationselement für mobile Geräte, um die Kennwortkomplexität als PIN zu konfigurieren. Die Kennwortlänge muss mindestens der minimalen Standardlänge entsprechen.  

*Für mobile Geräte, auf denen kein Konfigurations-Manager-Client installiert ist, die aber vom Exchange Server-Connector verwaltet werden:* Geben Sie in den **Kennworteinstellungen** für den Exchange Server-Connector an, dass die Kennwortkomplexität der PIN ist. Die Kennwortlänge muss mindestens der minimalen Standardlänge entsprechen.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Ausführung nur der Anwendungen, die von vertrauenswürdigen Unternehmen signiert sind  

Verhindern Sie die Manipulation von Inventur- und Statusinformationen, indem Sie die Ausführung von Anwendungen nur gestatten, wenn diese von vertrauenswürdigen Unternehmen stammen. Lassen Sie nicht zu, dass Geräte unsignierte Dateien installieren.  

*Für mobile Geräte, die mithilfe von Configuration Manager registriert werden:* Wählen Sie mit einem Konfigurationselement für mobile Geräte unter **Nicht signierte Anwendungen** die Sicherheitseinstellung **Nicht zugelassen** aus. Legen Sie die **Installation nicht signierter Dateien** auf eine vertrauenswürdige Quelle fest.  

*Für mobile Geräte, auf denen kein Konfigurations-Manager-Client installiert ist, die aber vom Exchange Server-Connector verwaltet werden:* Stellen Sie in den **Anwendungseinstellungen** für den Exchange Server-Connector die Optionen **Installation nicht signierter Dateien** und **Nicht signierte Anwendungen**auf **Nicht zugelassen** ein.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Sperren mobiler Geräte bei Nichtverwendung  

Verhindern Sie Angriffe durch Rechteerweiterungen, indem Sie das mobile Gerät sperren, wenn es nicht in Gebrauch ist.

*Für mobile Geräte, die mithilfe von Configuration Manager registriert werden:* Verwenden Sie ein Konfigurationselement für mobile Geräte, um die Kennworteinstellung **Idle time in minutes before mobile device is locked** (Leerlaufzeit in Minuten vor dem Sperren des Mobilgeräts) zu konfigurieren.  

*Für mobile Geräte, auf denen kein Konfigurations-Manager-Client installiert ist, die aber vom Exchange Server-Connector verwaltet werden:* Konfigurieren Sie die **Kennworteinstellungen** für den Exchange Server-Connector so, dass diese auf **Idle time in minutes before mobile device is locked** (Leerlaufzeit in Minuten vor dem Sperren des Mobilgeräts) eingestellt sind.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Einschränken der Benutzer, die ihre mobilen Geräte registrieren dürfen  

Verhindern Sie Rechteerweiterungen, indem Sie einschränken, welche Benutzer ihre mobilen Geräte registrieren dürfen. Verwenden Sie eine benutzerdefinierte Clienteinstellung anstelle von Standardclienteinstellungen, um nur autorisierten Benutzern das Anmelden ihrer mobilen Geräte zu gestatten.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Leitfaden zur Affinität zwischen Benutzer und Gerät für mobile Geräte  

Stellen Sie in den folgenden Szenarios keine Anwendungen für Benutzer bereit, die mobile Geräte über Configuration Manager oder Windows Intune registriert haben:  

- Das mobile Gerät wird von mehreren Personen verwendet.  

- Das Gerät wird von einem Administrator im Namen eines Benutzers angemeldet.  

- Das Gerät wird ohne vorherige Abkopplung und erneute Registrierung an eine andere Person übertragen.  

Die Registrierung erstellt eine Affinität zwischen Benutzer und Gerät. Diese Beziehung weist den Benutzer zu, der die Registrierung des mobilen Geräts vornimmt. Wenn ein anderer Benutzer das mobile Gerät verwendet, kann er die Anwendungen ausführen, die an den ursprünglichen Benutzer bereitgestellt wurden, was zu einer Rechteerweiterung führen kann. Wenn ein Administrator das mobile Gerät für einen Benutzer registriert, werden Anwendungen, die für diesen Benutzer bereitgestellt werden, nicht auf dem mobilen Gerät installiert. Stattdessen werden möglicherweise Anwendungen installiert, die für den Administrator bereitgestellt werden.  

Anders als bei der Affinität zwischen Benutzer und Gerät für Windows-Computer können Sie die Informationen zur Affinität zwischen Benutzer und Gerät nicht für mobile Geräte definieren, die von Microsoft Intune registriert werden.  

Wenn Sie den Besitz eines mobilen Geräts übertragen, das von Intune registriert ist, müssen Sie zuerst das mobile Gerät von Intune abkoppeln. Dadurch wird die Affinität zwischen Benutzer und Gerät entfernt. Fordern Sie dann den aktuellen Besitzer auf, das Gerät erneut zu registrieren.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Sicherstellen, dass Benutzer ihre eigenen mobilen Geräte für Microsoft Intune registrieren  

Während der Registrierung wird eine Affinität zwischen Benutzer und Gerät erstellt. Diese Aktion weist den Benutzer zu, der die Registrierung des mobilen Geräts vornimmt. Wenn ein Administrator das mobile Gerät für einen Benutzer registriert, werden Anwendungen, die für diesen Benutzer bereitgestellt werden, nicht auf dem mobilen Gerät installiert. Stattdessen werden möglicherweise Anwendungen installiert, die für den Administrator bereitgestellt werden.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Schützen der Verbindung zwischen dem Configuration Manager-Standortserver und Exchange Server

Verwenden Sie IPsec für einen lokalen Exchange Server-Server. Hosted Exchange schützt die Verbindung automatisch über SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Verwenden des Prinzips der geringsten Berechtigungen für den Connector  

Eine Liste der mindestens erforderlichen Cmdlets für den Exchange Server-Connector finden Sie unter [Verwalten von mobilen Geräten mit Configuration Manager und Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a> Bewährte Sicherheitsmethoden für Macs  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Verwenden eines sicheren Speicherorts zum Speichern und Zugreifen auf die Clientquelldateien  

Vor der Installation oder Registrierung des Clients auf einem Macintosh-Computer werden die Clientquelldateien von Configuration Manager nicht auf eine mögliche Manipulation hin überprüft. Laden Sie diese Dateien von einer vertrauenswürdigen Quelle herunter. Stellen Sie Sicherheit beim Speichern und Zugreifen sicher.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Überwachen und verfolgen der Gültigkeitsdauer des Zertifikats  

Überwachen und verfolgen Sie den Gültigkeitszeitraum der Zertifikate, die Sie für Macintosh-Computer verwenden, um eine Geschäftskontinuität sicherzustellen. Configuration Manager unterstützt die automatische Erneuerung dieses Zertifikats nicht bzw. gibt keine Warnung aus, wenn das Zertifikat in Kürze abläuft. Eine typische Gültigkeitsdauer beträgt ein Jahr.  

Weitere Informationen zur Erneuerung des Zertifikats finden Sie unter [Erneuern des Zertifikats für den Macintosh-Client](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Konfigurieren des vertrauenswürdigen Stammzertifikat nur für SSL  

Ziehen Sie zum Schutz vor einer Rechteerweiterung in Betracht, das Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle zu konfigurieren, das ausschließlich auf das SSL-Protokoll festgelegt ist.

Bei der Registrierung von Macintosh-Computern wird automatisch ein Benutzerzertifikat installiert, um den Konfigurations-Manager-Client zu verwalten. Dieses Benutzerzertifikat enthält die vertrauenswürdigen Stammzertifikate in seiner Vertrauenskette. Wenn Sie die Vertrauenswürdigkeit dieses Stammzertifikats ausschließlich auf das SSL-Protokoll beschränken wollen, können Sie wie folgt vorgehen:  

1. Öffnen Sie auf dem Macintosh-Computer ein Terminal-Fenster.  

2. Geben Sie den folgenden Befehl ein: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. Klicken Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** auf **System**. Klicken Sie anschließend im Abschnitt **Kategorie** auf **Zertifikate**.  

4. Suchen Sie nach dem Zertifikat der Stammzertifizierungsstelle für das Zertifikat des Mac-Clients, und doppelklicken Sie darauf.  

5. Erweitern Sie im Dialogfeld des Stammzertifikats den Abschnitt **Vertrauensstellung** , und nehmen Sie dann die folgenden Änderungen vor:  

    1. **Bei Verwendung dieses Zertifikats:** Ändern Sie die Einstellung **Always Trust** (Immer vertrauen) in **Use System Defaults** (Systemstandardwerte verwenden).  

    2. **Bei Verwendung von Secure Sockets Layer (SSL):** Ändern Sie **no value specified** (kein Wert angegeben) in **Always Trust** (Immer vertrauen).  

6. Schließen Sie das Dialogfeld. Geben Sie bei entsprechender Aufforderung das Administratorkennwort ein, und klicken Sie dann auf **Einstellungen aktualisieren**.  

Nach Abschluss dieser Prozedur ist das Stammzertifikat nur für die Überprüfung des SSL-Protokolls vertrauenswürdig. Andere Protokolle, die für dieses Zertifikat als nicht vertrauenswürdig eingestuft wurden, sind z.B. Secure Mail (S/MIME), Extensible Authentication (EAP) oder Codesignatur.  

> [!NOTE]  
> Verwenden Sie diese Prozedur auch, wenn Sie das Clientzertifikat unabhängig von Configuration Manager installiert haben.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a> Sicherheitsprobleme bei Configuration Manager-Clients  

Für die folgenden Sicherheitsprobleme ist keine Risikominderung vorhanden:  

### <a name="status-messages-arent-authenticated"></a>Statusmeldungen werden nicht authentifiziert

Für Statusmeldungen wird keine Authentifizierung ausgeführt. Wenn von einem Verwaltungspunkt HTTP-Clientverbindungen akzeptiert werden, können Statusmeldungen von beliebigen Geräten an den Verwaltungspunkt gesendet werden. Wenn der Verwaltungspunkt dagegen nur HTTPS-Clientverbindungen akzeptiert, muss für ein Gerät ein gültiges Clientauthentifizierungszertifikat von einer vertrauenswürdigen Zertifizierungsstelle vorliegen. Jedoch können auch beliebige Statusmeldungen gesendet werden. Der Verwaltungspunkt verwirft ungültige Statusmeldungen von Clients.  

Dieses Sicherheitsrisiko kann von manchen Angriffen ausgenutzt werden:

- Angreifer könnten z.B. eine gefälschte Statusmeldung senden, um Mitglied einer Sammlung zu werden, die auf Statusmeldungsabfragen basiert.
- Jeder Client könnte einen Denial-of-Service-Angriff auf den Verwaltungspunkt ausführen, in dem er mit Statusmeldungen überflutet wird.
- Wenn Statusmeldungen Aktionen in der Filterregel für Statusmeldungen auslösen, könnten Angreifer die Filterregel für Statusmeldungen auslösen.
- Angreifer könnten eine Statusmeldung senden, die dazu führt, dass Berichtsinformationen falsch angegeben werden.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>Richtlinien können auf Clients umgeleitet werden, für die sie nicht bestimmt sind.  

Angreifer verfügen über verschiedene Methoden, um eine Richtlinie auf einen anderen als den gewünschten Client anzuwenden. Beispielsweise könnte ein Angreifer falsche Inventur- oder Ermittlungsinformationen von einem vertrauenswürdigen Client senden, damit der Computer einer falschen Sammlung hinzugefügt wird. Dieser Client empfängt somit alle Bereitstellungen für diese Sammlung.

Es bestehen Kontrollen, um zu verhindern, dass Angreifer Richtlinien direkt modifizieren. Angreifer können jedoch eine vorhandene Richtlinie verwenden, die ein Betriebssystem neu formatiert und erneut bereitstellt, und es an einen anderen Computer senden. Diese umgeleitete Richtlinie könnte einen DoS-Angriff verursachen. Diese Angriffsmethoden erfordern einen genauen Zeitplan und umfassende Kenntnisse der Configuration Manager-Infrastruktur.  

### <a name="client-logs-allow-user-access"></a>Benutzer können auf Clientprotokolle zugreifen.  

Alle Clientprotokolldateien lassen die Gruppe **Benutzer** mit *Lesezugriff* und den besonderen **interaktiven** Benutzer mit *Schreibzugriff* zu. Wenn Sie die ausführliche Protokollierung aktivieren, können Angreifer die Protokolldateien anzeigen und so nach Informationen zur Kompatibilität oder Sicherheitsrisiken des Systems suchen. Prozesse, wie z.B. Software, die vom Client im Kontext eines Benutzers installiert wird, müssen mit einem Benutzerkonto mit geringen Rechten in Protokolle schreiben. Dieses Verhalten ermöglicht es auch Angreifern, mit einem Konto mit geringen Rechten in die Protokolle zu schreiben.  

Das größte Risiko ist, dass ein Angreifer Informationen in den Protokolldateien entfernen könnte. Ein Administrator benötigt diese Informationen möglicherweise für die Überwachung und Eindringungserkennung.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Mithilfe eines Computers können Zertifikate abgerufen werden, die für die Registrierung mobiler Geräte bestimmt sind  

Beim Verarbeiten einer Registrierungsanforderung in Configuration Manager kann nicht überprüft werden, ob die Anforderung von einem mobilen Gerät oder von einem Computer übermittelt wurde. Wurde die Anforderung von einem Computer übermittelt, kann auf diesem ein PKI-Zertifikat installiert werden, das die Registrierung mit Configuration Manager ermöglicht.

Verhindern Sie Angriffe durch Rechteerweiterungen in solchen Szenarios, indem Sie nur vertrauenswürdigen Benutzern die Registrierung ihrer mobilen Geräte gestatten. Überwachen Sie Registrierungsaktivitäten an diesem Standort sorgfältig.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Blockierte Clients können weiterhin Meldungen an den Verwaltungspunkt senden

Wenn Sie einen Client blockieren, dem Sie nicht mehr vertrauen, dieser aber eine Netzwerkverbindung für die Clientbenachrichtigung hergestellt hat, wird die Sitzung nicht von Configuration Manager unterbrochen. Vom blockierten Client können weiterhin Pakete an dessen Verwaltungspunkt geschickt werden, bis die Verbindung zum Netzwerk vom Client getrennt wird. Diese Pakete sind lediglich kleine Keep-Alive-Pakete. Dieser Client kann nicht von Configuration Manager verwaltet werden, bis die Blockierung aufgehoben wird.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Das automatische Clientupdate überprüft den Verwaltungspunkt nicht

Wenn Sie das automatische Clientupdate verwenden, kann der Client an einen Verwaltungspunkt weitergeleitet werden, um die Clientquelldateien herunterzuladen. In diesem Fall überprüft der Client nicht, ob der Verwaltungspunkt eine vertrauenswürdige Quelle ist.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Wenn Benutzer ihre Macintosh-Computer zum ersten Mal registrieren, sind diese durch DNS-Spoofing gefährdet  

Wenn der Macintosh-Computer während der Registrierung eine Verbindung zum Anmeldungsproxypunkt herstellt, verfügt der Macintosh-Computer wahrscheinlich noch nicht über ein Zertifikat der vertrauenswürdigen Stammzertifizierungsstelle. Zu diesem Zeitpunkt stuft der Macintosh-Computer den Server als nicht vertrauenswürdig ein, und der Benutzer wird zum Fortfahren aufgefordert. Falls der vollqualifizierte Domänenname (Fully Qualified Domain Name, FQDN) des Anmeldungsproxypunkts durch einen nicht autorisierten DNS-Server aufgelöst wird, könnte der Macintosh-Computer an einen nicht autorisierten Anmeldungsproxypunkt verwiesen werden und Zertifikate von einer nicht vertrauenswürdigen Quelle installieren. Zur Minderung dieses Risikos sollten Sie die bewährten Methoden im Hinblick auf die Verhinderung von DNS-Spoofing in Ihrer Umgebung befolgen.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Die Registrierung von Macintosh-Computern schränkt Zertifikatanforderungen nicht ein  

Benutzer können ihre Macintosh-Computer erneut registrieren und dabei jedes Mal ein neues Clientzertifikat anfordern. Configuration Manager führt keine Überprüfung auf mehrere Anforderungen durch, bzw. beschränkt nicht die Anzahl der Zertifikate, die von einem einzelnen Computer angefordert werden. Ein nicht autorisierter Benutzer könnte ein Skript ausführen, dass die Anmeldeanforderung über die Befehlszeile wiederholt. Dieser Angriff könnte einen Denial-of-Service-Modus für das Netzwerk oder die ausstellende Zertifizierungsstelle auslösen. Zur Minderung dieses Risikos sollten Sie die ausstellende Zertifizierungsstelle sorgfältig überwachen, um derartiges verdächtiges Verhalten zu erkennen. Jeder Computer, der diese Art von Verhalten zeigt, sollte umgehend für die Configuration Manager-Hierarchie blockiert werden.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Eine Zurücksetzbestätigung ist kein Nachweis dafür, dass das Gerät erfolgreich zurückgesetzt wurde  

Wenn Sie die Zurücksetzung eines mobilen Geräts initiieren und Configuration Manager die Zurücksetzung bestätigt, wird durch diese Bestätigung belegt, dass Configuration Manager die Meldung erfolgreich an das mobile Gerät *gesendet* hat. Sie bestätigt nicht, dass das Gerät die Anforderung *ausgeführt* hat.

Bei mobilen Geräten, die durch den Exchange Server-Connector verwaltet werden, wird durch eine Zurücksetzungsbestätigung belegt, dass der Befehl bei Exchange eingegangen ist, aber nicht auf dem Gerät.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Wenn Sie die Optionen für das Ausführen von Änderungen auf Windows Embedded-Geräten verwenden, werden Konten möglicherweise früher als erwartet gesperrt  

Wenn auf dem Windows Embedded-Gerät eine frühere Betriebssystemversion als Windows 7 ausgeführt wird, und ein Benutzer versucht, sich anzumelden, während die Schreibfilter von Configuration Manager deaktiviert sind, lässt Windows nur die Hälfte der festgelegten Zahl ungültiger Anmeldeversuche zu, bevor das Konto gesperrt wird.

Beispiel: Sie haben die Domänenrichtlinie für die **Kontensperrungsschwelle** auf sechs Versuche festgelegt. Ein Benutzer gibt sein Kennwort dreimal falsch ein, und das Konto wird gesperrt. Dieses Verhalten erstellt effizient einen Denial-of-Service-Zustand. Wenn sich Benutzer in diesem Szenario auf Embedded-Geräten anmelden müssen, informieren Sie sie über die Möglichkeit eines reduzierten Schwellenwert für die Sperre.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a> Informationen zum Datenschutz für Configuration Manager-Clients  

Wenn Sie den Konfigurations-Manager-Client bereitstellen, aktivieren Sie Clienteinstellungen, um Configuration Manager-Features verwenden zu können. Die Einstellungen, die Sie für die Konfiguration der Features verwenden, können für alle Clients in der Configuration Manager-Hierarchie gelten. Dieses Verhalten ist identisch, egal ob sie eine direkte Verbindung zum internen Netzwerk herstellen, über eine Remotesitzung verbunden werden oder über das Internet eine Verbindung herstellen.  

Clientinformationen werden in der Configuration Manager-Datenbank in SQL Server gespeichert und nicht an Microsoft gesendet. Die Informationen bleiben bis zum Löschen durch den Standortwartungstask **Veraltete Ermittlungsdaten löschen** in der Datenbank gespeichert. Der Löschvorgang wird alle 90 Tage ausgeführt. Sie können das Löschintervall konfigurieren. 

Einige zusammengefasste oder aggregierte Diagnose- und Nutzungsdaten werden an Microsoft gesendet. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Berücksichtigen Sie beim Konfigurieren des Configuration Manager-Clients Ihre Datenschutzanforderungen.  

Weitere Informationen zur Erfassung und Verwendung von Daten finden Sie in der [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/privacystatement).

### <a name="client-status"></a>Clientstatus  

Configuration Manager überwacht die Aktivität von Clients. In regelmäßigen Abständen wertet der Dienst den Konfigurations-Manager-Client aus und kann Probleme bei diesem Client und seinen Abhängigkeiten korrigieren. Der Clientstatus ist standardmäßig aktiviert. Er verwendet serverseitige Metriken zur Überprüfung der Clientaktivität. Der Clientstatus verwendet clientseitige Aktionen zur Selbstüberprüfung, Wartung und für das Übermitteln von Clientstatusinformationen an den Standort. Vom Client werden die Selbstüberprüfungen nach einem von Ihnen konfigurierten Zeitplan ausgeführt. Die Ergebnisse der Überprüfungen werden an den Configuration Manager-Standort übermittelt. Diese Informationen werden während der Übertragung verschlüsselt.  

Clientstatusinformationen werden in der Configuration Manager-Datenbank in SQL Server gespeichert und nicht an Microsoft gesendet. In der Standortdatenbank werden die Informationen unverschlüsselt gespeichert. Diese Informationen bleiben bis zum Löschen in der Datenbank gespeichert, abhängig von dem für die Clientstatuseinstellung **Clientstatusverlauf für die folgende Anzahl von Tagen beibehalten** konfigurierten Wert. Der Standardwert für diese Einstellung ist 31 Tage.  

Berücksichtigen Sie beim Installieren des Configuration Manager-Clients mit Überprüfung des Clientstatus Ihre Datenschutzanforderungen.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a> Informationen zum Datenschutz für vom Exchange Server-Connector verwaltete mobile Geräte  

Geräte, die über das ActiveSync-Protokoll mit einem lokalen oder gehosteten Exchange Server-Server verbunden sind, werden vom Exchange Server-Connector ermittelt und verwaltet. Die vom Exchange Server-Connector ermittelten Datensätze werden in der Configuration Manager-Datenbank in SQL Server gespeichert. Die Informationen werden von Exchange Server gesammelt. Dabei werden nur die von den mobilen Geräten an Exchange Server übermittelten Daten erfasst.  

Die Informationen zu den mobilen Geräten werden nicht an Microsoft gesendet. Anschließend werden die Informationen zu den mobilen Geräten in der Configuration Manager-Datenbank in SQL Server gespeichert. Die Informationen verbleiben bis zum Löschen durch den Standortwartungstask **Veraltete Ermittlungsdaten löschen** in der Datenbank. Der Löschvorgang wird alle 90 Tage ausgeführt. Sie können das Löschintervall konfigurieren.  

Berücksichtigen Sie beim Installieren und Konfigurieren des Exchange Server-Connectors Ihre Datenschutzanforderungen.  

Weitere Informationen zur Erfassung und Verwendung von Daten finden Sie in der [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/privacystatement).
