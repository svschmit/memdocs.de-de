---
title: Suchen von Standortressourcen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie und wann Configuration Manager-Clients die Dienstidentifizierung zum Suchen von Standortressourcen verwenden.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 262234edbd6fac6973653ca6cac62853fde23b2d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700111"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>Informationen dazu, wie Clients Standortressourcen und -dienste für Configuration Manager suchen

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager-Clients verwenden einen als *Dienstidentifizierung* bezeichneten Prozess zum Auffinden von Standortsystemservern, mit denen Sie kommunizieren können und die Dienste bereitstellen, die Clients verwenden sollen. Wenn Sie verstehen, wie und wann Clients die Dienstidentifizierung zum Auffinden von Standortressourcen nutzen, können Sie Ihre Standorte besser für die erfolgreiche Unterstützung von Clientvorgängen konfigurieren. Diese Konfigurationen können erfordern, dass der Standort mit Domänen- und Netzwerkkonfigurationen wie Active Directory-Domänendienste (AD DS) und DNS interagiert. Oder Sie müssen möglicherweise komplexere Alternativen konfigurieren.  

Beispiele für Standortsystemrollen, die Dienste bereitstellen:

- Der zentrale Standortsystemserver für Clients.
- Der Verwaltungspunkt.
- Zusätzliche Standortsystemserver, mit denen der Client kommunizieren kann, z. B. Verteilungspunkte und Softwareupdatepunkte.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Fundamentals of service location  
 Ein Client bewertet seine aktuelle Netzwerkadresse, Kommunikationsprotokolleinstellung und seinen zugewiesenen Standort, wenn die Dienstidentifizierung zum Auffinden eines Verwaltungspunkts genutzt wird, mit dem kommuniziert werden kann.  

**Ein Client kommuniziert zu folgenden Zwecken mit einem Verwaltungspunkt:**  
- Herunterladen von Informationen zu anderen Verwaltungspunkten für den Standort, damit für künftige Dienstidentifizierungszyklen eine Verwaltungspunktliste (auch als *MP-Liste* bezeichnet) erstellt werden kann.  
- Hochladen von Konfigurationsdetails wie Inventur und Status.  
- Herunterladen von Richtlinien zum Festlegen von Konfigurationen auf dem Client, zum Informieren des Clients zu Software, die installiert werden muss oder kann, und zu weiteren dazugehörigen Aufgaben.  
- Anfordern von Informationen zu zusätzlichen Standortsystemrollen, die Dienste bereitstellen, für deren Verwendung der Client konfiguriert wurde. Beispiele umfassen Verteilungspunkte für Software, die vom Client installiert werden können, oder ein Softwareupdatepunkt, von dem Softwareupdates abgerufen werden können.  

**Ein Configuration Manager-Client sendet eine Dienstidentifizierungsanforderung:**  
- Alle 25 Stunden bei kontinuierlichem Betrieb.  
- Wenn der Client eine Änderung seiner Netzwerkkonfiguration oder seiner Adresse erkennt.  
- Wenn der **ccmexec.exe**-Dienst auf dem Computer (der Kern-Clientdienst) gestartet wird.  
- Wenn der Client eine Standortsystemrolle finden muss, die einen erforderlichen Dienst bereitstellt.  

**Beim Versuch, Server zu suchen, die Standortsystemrollen hosten**, verwendet der Client die Dienstidentifizierung, um nach einer Standortsystemrolle zu suchen, die das Protokoll des Clients (HTTP oder HTTPS) unterstützt. Die Wahl fällt standardmäßig auf die sicherste der verfügbaren Methoden. Beachten Sie Folgendes:  

- Zur Verwendung von HTTPS müssen Sie über eine Public Key-Infrastruktur (PKI) verfügen und PKI-Zertifikate auf Clients und Servern installieren. Informationen zum Verwenden von Zertifikaten finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

- Wenn Sie eine Standortsystemrolle bereitstellen, die Internetinformationsdienst (IIS) verwendet und die Kommunikation von Clients unterstützt, müssen Sie angeben, ob Clients eine Verbindung mit dem Standortsystem über HTTP oder HTTPS herstellen. Falls Sie sich für HTTP entscheiden, müssen Sie auch Signierungs- und Verschlüsselungsoptionen erwägen. Weitere Informationen finden Sie unter [Planen von Signierung und Verschlüsselung](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in [Planen der Sicherheit](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Dienstidentifizierung und wie Clients den ihnen zugewiesenen Verwaltungspunkt ermitteln  
Wenn ein Client erstmals einem primären Standort zugewiesen wird, wählt er einen Standardverwaltungspunkt für diesen Standort aus. Primäre Standorte unterstützen mehrere Verwaltungspunkte, und jeder Client identifiziert unabhängig einen Verwaltungspunkt als Standardverwaltungspunkt. Der Standardverwaltungspunkt wird dann der diesem Client zugewiesene Verwaltungspunkt. (Sie können auch bei der Installation eines Clients Befehle zum Festlegen des zugewiesenen Verwaltungspunkts für einen Client festlegen.)  

Ein Client wählt einen Verwaltungspunkt für die Kommunikation basierend auf seiner aktuellen Konfiguration der Netzwerkadresse und Begrenzungsgruppe aus. Auch wenn ein Client einen zugewiesenen Verwaltungspunkt hat, ist dies ggf. nicht der Verwaltungspunkt, den der Client verwendet.  

> [!NOTE]  
> Ein Client verwendet immer den zugewiesenen Verwaltungspunkt für Registrierungs- und bestimmte Richtlinienmeldungen, selbst wenn andere Mitteilungen an einen Proxy oder lokalen Verwaltungspunkt gesendet werden.

Sie können bevorzugte Verwaltungspunkte verwenden. Bevorzugte Verwaltungspunkte sind Verwaltungspunkte vom zugewiesenen Standort eines Clients, die einer Begrenzungsgruppe zugeordnet sind, die vom Client verwendet wird, um Standortsystemserver zu finden. Die Zuordnung eines bevorzugten Verwaltungspunkts zu einer Begrenzungsgruppe als Standortsystemserver ist ähnlich der Zuordnung von Verteilungspunkten oder Zustandsmigrationspunkten zu einer Begrenzungsgruppe. Wenn Sie bevorzugte Verwaltungspunkte für die Hierarchie aktivieren, versucht ein Client einen bevorzugten Verwaltungspunkt zu verwenden, wenn er einen Verwaltungspunkt von seinem zugewiesenen Standort verwendet, bevor andere Verwaltungspunkte des zugewiesenen Standorts verwendet werden.  

Sie können auch die Informationen im Blog zur [Affinität mit einem Verwaltungspunkt](/archive/blogs/jchalfant/management-point-affinity-added-in-configmgr-2012-r2-cu3) befolgen, um die Affinität mit einem Verwaltungspunkt zu konfigurieren. Die Verwaltungspunktsaffinität überschreibt das Standardverhalten für zugewiesene Verwaltungspunkte und ermöglicht dem Client, einen oder mehrere bestimmte Verwaltungspunkte zu verwenden.  

Jedes Mal, wenn ein Client einen Verwaltungspunkt kontaktieren muss, überprüft er die Verwaltungspunktliste, die lokal in WMI (Windows Management Instrumentation) gespeichert ist. Der Client erstellt bei der Installation eine erste Verwaltungspunktliste. Der Client aktualisiert dann die Liste regelmäßig mit Details zu jedem Verwaltungspunkt in der Hierarchie.  

Wenn der Client keinen gültigen Verwaltungspunkt in seiner Verwaltungspunktliste findet, durchsucht er die folgenden Dienstidentifizierungsquellen in der angegebenen Reihenfolge, bis er einen Verwaltungspunkt findet, den er verwenden kann:  

1.  Verwaltungspunkt  
2.  AD DS  
3.  DNS  
4.  WINS  

Nachdem ein Client Verwaltungspunkt erfolgreich gesucht und kontaktiert hat, lädt er die aktuelle Liste von Verwaltungspunkten herunter, die in der Hierarchie verfügbar sind, und aktualisiert die lokale Verwaltungspunktliste. Dies gilt für alle Clients, unabhängig davon, ob sie einer Domäne angehören oder nicht.  

Wenn beispielsweise ein Configuration Manager-Client, der sich im Internet befindet, eine Verbindung mit einem internetbasierten Verwaltungspunkt herstellt, sendet der Verwaltungspunkt diesem Client eine Liste der verfügbaren internetbasierten Verwaltungspunkte am Standort. Auf ähnliche Weise erhalten auch Clients, die sich in einer Domäne oder in Arbeitsgruppen befinden, die Liste der Verwaltungspunkte, die sie verwenden können.  

Einem Client, der nicht für das Internet konfiguriert ist, werden keine Verwaltungspunkte bereitgestellt, die nur auf das Internet ausgerichtet sind. Arbeitsgruppenclients, die für das Internet konfiguriert sind, kommunizieren nur mit Verwaltungspunkten, die auf das Internet ausgerichtet sind.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a> MP-Liste  
Die Verwaltungspunktliste eines Clients ist die bevorzugte Quelle für die Dienstidentifizierung, da sie eine priorisierte Liste von Verwaltungspunkten ist, die der Client zuvor identifiziert hat. Diese Liste wird nach einzelnen Clients basierend auf dem Netzwerkstandort sortiert, wenn der Client die Liste aktualisiert, und dann lokal auf dem Client in WMI gespeichert.  

### <a name="building-the-initial-mp-list"></a>Erstellen der anfänglichen MP-Liste  
Während der Installation des Clients werden die folgenden Regeln zum Erstellen der anfänglichen MP-Liste des Clients verwendet:  

- Die anfängliche Liste enthält Verwaltungspunkte, die während der Clientinstallation angegeben wurden (bei Verwendung von **SMSMP**= oder **/MP**).  
- Der Client fragt AD DS nach veröffentlichten Verwaltungspunkten ab. Für eine Identifizierung von AD DS muss der Verwaltungspunkt vom zugewiesenen Standort des Clients stammen und der Produktversion des Clients entsprechen.  
- Wenn kein Verwaltungspunkt während der Clientinstallation angegeben wurde und das Active Directory-Schema nicht erweitert ist, überprüft der Client DNS und WINS auf veröffentlichte Verwaltungspunkte.  
- Wenn der Client die anfängliche Liste erstellt, sind möglicherweise keine Informationen zu einigen Verwaltungspunkten in der Hierarchie bekannt.  

### <a name="organizing-the-mp-list"></a>Organisieren der MP-Liste  
Clients organisieren ihre Liste mit Verwaltungspunkten mithilfe der folgenden Klassifizierungen:  

- **Proxy:** ein Verwaltungspunkt an einem sekundären Standort.  
- **Lokal:** jeder Verwaltungspunkt, der dem aktuellen Netzwerkstandort des Clients entsprechend der definierten Standortgrenzen zugeordnet ist. Beachten Sie die folgenden Informationen zu Grenzen:
  - Wenn ein Client zu mehreren Grenzgruppen gehört, wird die Liste der lokalen Verwaltungspunkte aus der Vereinigung aller Grenzen bestimmt, die den aktuellen Netzwerkstandort des Clients enthalten.  
  - In der Regel sind lokale Verwaltungspunkte eine Teilmenge der zugewiesenen Verwaltungspunkte eines Clients, es sei denn, der Client befindet sich an einem Netzwerkstandort, der mit einem anderen Standort mit Verwaltungspunkten verbunden ist, die Grenzgruppen bereitstellen.   


- **Zugewiesen:** alle Verwaltungspunkte, die ein Standortsystem für den zugewiesenen Standort des Clients sind.  

Sie können bevorzugte Verwaltungspunkte verwenden. Verwaltungspunkte an einem Standort, die keiner Begrenzungsgruppe zugeordnet sind oder sich nicht in einer Begrenzungsgruppe befinden, die dem aktuellen Netzwerkspeicherort des Clients zugeordnet ist, gelten nicht als bevorzugt. Sie werden verwendet, wenn der Client keinen verfügbaren bevorzugten Verwaltungspunkt identifizieren kann.  

### <a name="selecting-a-management-point-to-use"></a>Auswählen eines zu verwendenden Verwaltungspunkts  
Für eine typische Kommunikation versucht ein Client, einen Verwaltungspunkt aus den Klassifizierungen in der folgenden Reihenfolge zu verwenden, basierend auf dem Netzwerkstandort des Clients:  

1.  Proxy  
2.  Lokal  
3.  zugewiesenen  

Allerdings verwendet der Client immer den zugewiesenen Verwaltungspunkt für Registrierungsmeldungen und bestimmte Richtlinienmeldungen, selbst andere Mitteilungen an einen Proxy oder lokalen Verwaltungspunkt gesendet werden.  

In jeder Klassifizierung (Proxy, lokal oder zugewiesen) versuchen Clients, einen Verwaltungspunkt auf der Basis von Einstellungen in der folgenden Reihenfolge zu verwenden:  

1.  HTTPS-fähig in einer vertrauenswürdigen oder lokalen Gesamtstruktur (wenn der Client für die HTTPS-Kommunikation konfiguriert ist)  
2.  HTTPS-fähig in einer nicht vertrauenswürdigen oder lokalen Gesamtstruktur (wenn der Client für die HTTPS-Kommunikation konfiguriert ist)  
3.  HTTP-fähig in einer vertrauenswürdigen oder lokalen Gesamtstruktur  
4.  HTTP-fähig, nicht in einer vertrauenswürdigen oder lokalen Gesamtstruktur  

Clients versuchen, aus dem Satz der nach Einstellungen sortierten Verwaltungspunkten den ersten Verwaltungspunkt in der Liste zu verwenden. Diese sortierte Liste von Verwaltungspunkten ist zufällig und kann nicht sortiert werden. Die Reihenfolge der Liste kann sich jedes Mal ändern, wenn der Client seine Verwaltungspunktliste aktualisiert.  

Wenn ein Client keinen Kontakt mit dem ersten Verwaltungspunkt herstellen kann, versucht er es mit jedem nachfolgenden Verwaltungspunkt in der Liste. Er versucht es mit jedem bevorzugten Verwaltungspunkt in der Klassifizierung, bevor es mit nicht bevorzugten Verwaltungspunkten versucht wird. Wenn ein Client keine erfolgreiche Kommunikation mit einem der Verwaltungspunkte in der Klassifizierung herstellen kann, versucht er, einen Kontakt zu einem bevorzugten Verwaltungspunkt aus der nächsten Klassifizierung herzustellen, und setzt diese Vorgehensweise fort, bis er einen Verwaltungspunkt zum Verwenden gefunden hat.  

Nach dem Einrichten der Kommunikation mit einem Verwaltungspunkt verwendet der Client weiterhin denselben Verwaltungspunkt bis zum folgenden Punkt:  

- Es sind 25 Stunden vergangen.  
- Der Client kann bei fünf Versuchen über einen Zeitraum von 10 Minuten keine Kommunikation mit dem Verwaltungspunkt einrichten.

Der Client wählt nach dem Zufallsprinzip einen neuen Verwaltungspunkt aus.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a> Active Directory  
Clients, die der Domäne beigetreten sind, können AD DS für die Dienstidentifizierung verwenden. Dafür müssen Standorte [Daten in Active Directory veröffentlichen](../../servers/deploy/configure/publish-site-data.md).  

Ein Client kann AD DS für die Dienstidentifizierung verwenden, wenn alle folgenden Bedingungen erfüllt sind:  

- Das Active Directory-[Schema wurde erweitert](../network/extend-the-active-directory-schema.md) oder für System Center 2012 Configuration Manager erweitert.  
- Die [Active Directory-Gesamtstruktur ist für die Veröffentlichung konfiguriert](../../servers/deploy/configure/publish-site-data.md)und Configuration Manager-Standorte sind für das Veröffentlichen konfiguriert.  
- Der Clientcomputer ist ein Mitglied einer Active Directory-Domäne, und der Zugriff auf den globalen Katalogserver ist möglich.  

Wenn ein Client keinen Verwaltungspunkt für die Dienstidentifizierung von AD DS finden kann, versucht er, DNS zu verwenden.  

##  <a name="dns"></a><a name="bkmk_dns"></a> DNS  
Clients im Intranet können DNS für die Dienstidentifizierung verwenden. Dafür ist mindestens einen Standort in einer Hierarchie erforderlich, um Informationen zu Verwaltungspunkten in DNS zu veröffentlichen.  

Ziehen Sie die Verwendung von DNS für die Dienstidentifizierung in Betracht, wenn eine der folgenden Bedingungen erfüllt ist:
- Das AD DS-Schema wurde nicht für die Unterstützung von Configuration Manager erweitert.
- Intranetclients befinden sich in einer Gesamtstruktur, die nicht für die Configuration Manager-Veröffentlichung aktiviert ist.  
- Sie haben Clients auf Arbeitsgruppencomputern, und diese Clients sind nicht für eine rein internetbasierte Clientverwaltung konfiguriert. (Ein für das Internet konfigurierter Arbeitsgruppenclient kommuniziert nur mit Verwaltungspunkten, die auf das Internet ausgerichtet sind, und verwendet nicht DNS für die Dienstidentifizierung.)  
- Sie können [Clients für die Suche von Verwaltungspunkten von DNS konfigurieren](../../clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Wenn ein Standort Dienstidentifizierungseinträge für Verwaltungspunkte an DNS veröffentlicht:  

- Die Veröffentlichung gilt nur für Verwaltungspunkte, die Clientverbindungen aus dem Intranet akzeptieren.  
- Durch die Veröffentlichung wird ein Ressourceneintrag für die Dienstidentifizierung (SRV RR) in der DNS-Zone des Verwaltungspunktcomputers hinzugefügt. In DNS muss ein entsprechender Hosteintrag für diesen Computer vorhanden sein.  

Standardmäßig durchsuchen in die Domäne eingebundene Clients DNS nach Verwaltungspunkteinträgen aus der lokalen Domäne des Clients. Sie können eine Clienteigenschaft konfigurieren, die ein Domänensuffix für eine Domäne angibt, in der Verwaltungspunktinformationen in DNS veröffentlicht werden.  

Weitere Informationen zum Konfigurieren des DNS-Suffixes in einer Clienteigenschaft finden Sie unter [Konfigurieren von Clientcomputern für die Suche nach Verwaltungspunkten mithilfe der DNS-Veröffentlichung](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Wenn ein Client keinen Verwaltungspunkt für die Dienstidentifizierung von DNS finden kann, versucht er, WINS zu verwenden.  

### <a name="publish-management-points-to-dns"></a>Veröffentlichen von Verwaltungspunkten in DNS  
Die Veröffentlichung von Verwaltungspunkten in DNS ist nur möglich, wenn die beiden folgenden Bedingungen erfüllt sind:  

- Von den DNS-Servern werden Ressourceneinträge für Dienste unterstützt (durch Verwendung von BIND 8.1.2 oder höher).  
- Zu den angegebenen Intranet-FQDNs für die Verwaltungspunkte in Configuration Manager müssen Hosteinträge z.B. (A-Datensätze) in DNS vorhanden sein.  

> [!IMPORTANT]  
> Bei der DNS-Veröffentlichung über Configuration Manager werden keine separaten Namespaces unterstützt. Liegt ein separater Namespace vor, können Sie Verwaltungspunkte manuell in DNS veröffentlichen oder eine der Dienstidentifizierungsmethoden verwenden, die in diesem Abschnitt beschrieben sind.  

**Falls von den DNS-Servern automatische Updates unterstützt werden**, können Sie festlegen, dass Verwaltungspunkte von Configuration Manager im Intranet automatisch in DNS veröffentlicht werden. Alternativ können Sie diese Datensätze manuell in DNS veröffentlichen. Bei der Veröffentlichung von Verwaltungspunkten in DNS werden der zugehörige Intranet-FQDN und die Portnummer im SRV-Eintrag veröffentlicht. Sie konfigurieren die DNS-Veröffentlichung an einem Standort über die Eigenschaften für Verwaltungspunktkomponenten am Standort. Weitere Informationen finden Sie unter [Standortkomponenten für Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**Wenn Ihre DNS-Zone für dynamische Updates auf „Secure only“ (Nur sichern) festgelegt ist**, kann nur der erste Verwaltungspunkt, der unter DNS veröffentlicht werden soll, dies mit Standardberechtigungen ausführen.

Wenn nur ein Verwaltungspunkt erfolgreich seinen DNS-Eintrag veröffentlichen und ändern kann und der Verwaltungspunktserver fehlerfrei arbeitet, können Clients die vollständige MP-Liste von diesem Verwaltungspunkt erhalten und anschließend ihren bevorzugten Verwaltungspunkt finden.


**Wenn von den DNS-Servern SRV-Einträge unterstützt werden, nicht aber automatische Updates**, können Sie Verwaltungspunkte manuell in DNS veröffentlichen. Dafür müssen Sie den Ressourceneintrag für Dienste (SRV RR) manuell in DNS angeben.  

Configuration Manager unterstützt RFC 2782 für Dienstidentifizierungseinträge. Diese Einträge haben das folgende Format: *_Dienst._Proto.Name TTL Klasse SRV Priorität Gewichtung Port Ziel*  

Geben Sie die folgenden Werte an, um einen Verwaltungspunkt in Configuration Manager zu veröffentlichen:  

- **_Service:** Geben Sie **_mssms_mp**_&lt;Standortcode\> ein, wobei &lt;Standortcode\> der Standortcode des Verwaltungspunkts ist.  
- **._Proto:** Geben Sie **._tcp** an.  
- **.Name:** Geben Sie das DNS-Suffix des Verwaltungspunkts an, z.B. **contoso.com**.  
- **TTL:** Geben Sie **14400** an. Dies entspricht vier Stunden.  
- **Klasse:** Geben Sie **IN** an (in Übereinstimmung mit RFC 1035).  
- **Priorität:** Dieses Feld wird nicht von Configuration Manager verwendet.
- **Stärke:** Dieses Feld wird nicht von Configuration Manager verwendet.  
- **Port:** Geben Sie die Portnummer des Verwaltungspunkts ein, beispielsweise **80** für HTTP und **443** für HTTPS.  

  > [!NOTE]  
  >  Der Port für den SRV-Datensatz sollte dem vom Verwaltungspunkt verwendeten Kommunikationsport entsprechen. Standardmäßig ist dies **80** für die HTTP-Kommunikation und **443** für die HTTPS-Kommunikation.  

- **Ziel:** Geben Sie den Intranet-FQDN des Standortsystems an, das mit der Standortrolle „Verwaltungspunkt“ konfiguriert ist.  

Wenn Sie Windows Server DNS verwenden, können Sie diesen DNS-Eintrag anhand des folgenden Verfahrens für Intranet-Verwaltungspunkte eingeben. Wenn Sie für DNS eine andere Implementierung verwenden, prüfen Sie in der DNS-Dokumentation anhand der Informationen zu den Feldwerten in diesem Abschnitt, wie Sie dieses Verfahren anpassen müssen.  

##### <a name="to-configure-automatic-publishing"></a>So konfigurieren Sie die automatische Veröffentlichung:  

1.  Erweitern Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**.  

2.  Wählen Sie Ihren Standort aus, und wählen Sie dann **Standortkomponenten konfigurieren** aus.  

3.  Wählen Sie **Verwaltungspunkt** aus.  

4.  Wählen Sie die Verwaltungspunkte aus, die Sie veröffentlichen möchten. (Diese Option gilt für die Veröffentlichung in AD DS und DNS.)  

5.  Aktivieren Sie das Kontrollkästchen für die DNS-Veröffentlichung. Dieses Feld bietet folgende Möglichkeiten:  

    - Sie können auswählen, welche Verwaltungspunkte in DNS veröffentlicht werden.  

    - Es wird nicht die Veröffentlichung in AD DS konfiguriert.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>So können Sie Verwaltungspunkte unter Windows Server manuell in DNS veröffentlichen  

1.  Geben Sie in der Configuration Manager-Konsole die Intranet-FQDNs der Standortsysteme an.  

2.  Wählen Sie in der DNS-Verwaltungskonsole die DNS-Zone für den Verwaltungspunktcomputer aus.  

3.  Überprüfen Sie, ob es einen Hostdatensatz (A oder AAAA) für den Intranet-FQDN des Standortsystems gibt. Ist dieser Datensatz nicht vorhanden, erstellen Sie ihn.  

4.  Verwenden Sie die Option **Neue andere Einträge**. Wählen Sie im Dialogfeld **Ressourceneintragstyp** die Option **Dienstidentifizierung (SRV)** aus. Wählen Sie **Eintrag erstellen** aus, geben Sie die folgenden Informationen ein, und wählen Sie dann **Fertig** aus:  

    - **Domäne:** Geben Sie gegebenenfalls das DNS-Suffix des Verwaltungspunkts an, z.B. **contoso.com**.  
    - **Dienst:** Geben Sie **_mssms_mp**_&lt;Standortcode\> ein, wobei &lt;Standortcode\> der Standortcode des Verwaltungspunkts ist.  
    - **Protokoll:** Geben Sie **_tcp** ein.  
    - **Priorität:** Dieses Feld wird nicht von Configuration Manager verwendet.  
    - **Stärke:** Dieses Feld wird nicht von Configuration Manager verwendet.  
    - **Port:** Geben Sie die Portnummer des Verwaltungspunkts ein, beispielsweise **80** für HTTP und **443** für HTTPS.  

      > [!NOTE]  
      > Der Port für den SRV-Datensatz sollte dem vom Verwaltungspunkt verwendeten Kommunikationsport entsprechen. Standardmäßig ist dies **80** für die HTTP-Kommunikation und **443** für die HTTPS-Kommunikation.  

    - **Host, der diesen Dienst anbietet:** Geben Sie den Intranet-FQDN des Standortsystems an, das mit der Standortrolle „Verwaltungspunkt“ konfiguriert ist.  

Wiederholen Sie diese Schritte für jeden Verwaltungspunkt im Intranet, der in DNS veröffentlicht werden soll.  

##  <a name="wins"></a><a name="bkmk_wins"></a> WINS  
Falls andere Dienstidentifizierungsmechanismen erfolglos bleiben, kann durch Überprüfen von WINS ein erster Verwaltungspunkt gefunden werden.  

Standardmäßig veröffentlicht ein primärer Standort in WINS den ersten Verwaltungspunkt am Standort, der für HTTP konfiguriert ist, und den ersten Verwaltungspunkt, der für HTTPS konfiguriert ist.  

Wenn Sie nicht wünschen, dass ein HTTP-Verwaltungspunkt in WINS gefunden wird, konfigurieren Sie für Clients die Client.msi-Eigenschaft **SMSDIRECTORYLOOKUP=NOWINS**mit CCMSetup.exe.