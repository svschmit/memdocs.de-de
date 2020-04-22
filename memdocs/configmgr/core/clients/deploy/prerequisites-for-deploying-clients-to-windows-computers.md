---
title: Voraussetzungen für die Bereitstellung des Windows-Clients
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen über die Voraussetzungen für die Bereitstellung von Configuration Manager-Clients auf Windows-Computern.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694788"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Voraussetzungen zum Bereitstellen von Clients für Windows-Computer in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei der Bereitstellung von Configuration Manager-Clients in einer Umgebung sind die folgenden externen und produktinternen Abhängigkeiten zu beachten. Darüber hinaus weist jede Clientbereitstellungsmethode eigene Abhängigkeiten auf, die erfüllt sein müssen, um eine erfolgreiche Clientinstallation auszuführen.  

Weitere Informationen zu den Mindestanforderungen an Hardware und Betriebssystem für den Konfigurations-Manager-Client finden Sie unter [Unterstützte Konfigurationen](../../plan-design/configs/supported-configurations.md).  

> [!NOTE]  
> Bei den in diesem Artikel aufgeführten Softwareversionsnummern handelt es sich um die erforderlichen Mindestversionsnummern.  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a> Voraussetzungen für Windows-Clients  

Mithilfe der folgenden Informationen können Sie die Voraussetzungen für die Installation des Konfigurations-Manager-Clients auf Windows-Computern bestimmen.  

### <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

|Komponente|Beschreibung|  
|---|---|  
|Windows Installer Version 3.1.4000.2435|Erforderlich, um die Verwendung der Microsoft Windows Installer-Updatedateien (.msp) für Pakete und Softwareupdates zu unterstützen.|  
|Microsoft Background Intelligent Transfer Service (BITS) Version 2.5|Erforderlich, um Datenübertragungen eingeschränkter Bandbreite zwischen dem Clientcomputer und den Configuration Manager-Standortsystemen zu ermöglichen. BITS wird während der Clientinstallation nicht automatisch heruntergeladen. Wenn BITS auf Computern installiert wird, ist in der Regel ein Neustart zum Abschließen der Installation erforderlich.<br /><br /> Die meisten Betriebssysteme enthalten BITS. Wenn das nicht der Fall ist, installieren Sie BITS, bevor Sie den Konfigurations-Manager-Client installieren.|  
|Microsoft-Aufgabenplanung|Aktivieren Sie diesen Dienst auf dem Client, um die Clientinstallation abzuschließen.|  
|Unterstützung für SHA-2-Codesignieren|Ab Version 1906 müssen Clients den SHA-2-Codesignaturalgorithmus unterstützen. Weitere Informationen finden Sie unter [Unterstützung für SHA-2-Codesignieren](#bkmk_sha2).|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a> Unterstützung für SHA-2-Codesignieren

<!--SCCMDocs-pr#3404-->
Aufgrund von Schwächen des SHA-1-Algorithmus und um Branchenstandards zu erfüllen, signiert Microsoft nun Configuration Manager-Binärdateien mit dem SHA-2-Algorithmus, der größere Sicherheit bietet. Ältere Windows-Betriebssystemversionen erfordern ein Update, damit die SHA-2-Codesignierung unterstützt wird. Weitere Informationen finden Sie unter [Unterstützung der SHA-2-Codesignierung für Windows und WSUS (2019)](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Wenn Sie kein Update dieser Betriebssystemversionen ausführen, können Sie die Configuration Manager-Clientversion 1906 nicht installieren. Dieses Verhalten gilt für das Installieren eines neuen Clients sowie für ein Update von einer früheren Version.

Wenn Sie einen Client in einer Windows-Version verwalten müssen, für die kein Update durchgeführt wird, bzw. die älter als die oben aufgeführten Versionen ist, verwenden Sie den Configuration Manager-Client für erweiterte Interoperabilität (EIC), Version 1902. Weitere Informationen finden unter [Client für erweiterte Interoperabilität](../../understand/interoperability-client.md).

> [!Tip]  
> Wenn Sie kein [automatisches Clientupdate](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) verwenden und Clients über einen anderen Mechanismus aktualisieren, müssen Sie die Version von ccmsetup aktualisieren. Eine ältere Version von ccmsetup überprüft möglicherweise das neue SHA-2-Codesignierzertifikat in den Binärdateien von Client-Version 1906. Sie kopieren z. B. „ccmsetup.exe“ in eine Dateifreigabe oder verwenden ccmsetup.msi mit Gruppenrichtlinien.<!-- 4963362 -->
>
> Die folgenden Client-Updatemechanismen sollten nicht betroffen sein:
>
> - Clientpushinstallation: Das Clientpaket vom Standort wird verwendet
> - Auf Softwareupdate basierende Installation: Das Standortupdate wird in WSUS erneut veröffentlicht
> - Mit Intune MDM verwaltete Windows-Geräte: Die unterstützte Version für diesen Mechanismus unterstützt bereits das SHA-2-Codesignieren, trotzdem muss immer noch die neueste Datei „ccmsetup. msi“ verwendet werden

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a> Externe abhängige Komponenten für Configuration Manager, die bei der Installation automatisch heruntergeladen werden  

Der Konfigurations-Manager-Client verfügt über externe Abhängigkeiten. Diese Abhängigkeiten hängen von der Version des Betriebssystems und der installierten Software auf dem Clientcomputer ab.  

Wenn der Client diese Abhängigkeiten benötigt, um die Installation abzuschließen, werden sie automatisch installiert.  

|Komponente|Beschreibung|  
|---|---|  
|Windows Update Agent Version 7.0.6000.363|Wird von Windows zur Unterstützung der Updateerkennung und -bereitstellung benötigt.|  
|Microsoft Core XML Services (MSXML) Version 6.20.5002 oder höher|Wird unter Windows zur Unterstützung der Verarbeitung von XML-Dokumenten benötigt.|  
|Microsoft Remote Differential Compression (RDC)|Ist erforderlich, um die Datenübertragung über das Netzwerk zu optimieren.|  
|Microsoft Visual C++ 2013 Redistributable Version 12.0.21005.1|Ist zur Unterstützung von Clientoperationen erforderlich. Wenn Sie dieses Update auf Clientcomputern installieren, kann ein Neustart zum Abschließen der Installation erforderlich sein.|  
|Microsoft Visual C++ 2005 Redistributable Version 8.0.50727.42|Für die Version 1606 und ältere Versionen ist erforderlich, das Microsoft SQL Server Compact-Operationen unterstützt werden.|  
|Windows Imaging APIs 6.0.6001.18000|Ist erforderlich für die Verwaltung von Windows-Imagedateien (.wim) mit Configuration Manager.|  
|Microsoft-Richtlinienplattform 1.2.3514.0|Ist erforderlich, damit Konformitätseinstellungen von Clients ausgewertet werden können.|  
|Microsoft .NET Framework 4.5.2|Ist zur Unterstützung von Clientoperationen erforderlich. Wird automatisch auf dem Clientcomputer installiert, wenn Microsoft .NET Framework 4.5 oder höher nicht installiert ist. Weitere Informationen finden Sie im nächsten Abschnitt unter [Weitere Informationen über Microsoft .NET Framework, Version 4.5.2](#dotNet).|  
|Microsoft SQL Server Compact 4.0 SP1-Komponenten|Ist erforderlich zum Speichern von Informationen zu Clientoperationen.|  

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Wenn Sie weiterhin die Benutzeroberfläche der Website mit dem Anwendungskatalog nutzen, erfordert der Client Microsoft Silverlight 5.1.41212.0. Silverlight wird vom Client nicht automatisch installiert. Die primäre Funktion des Anwendungskatalogs ist jetzt im Softwarecenter verfügbar.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a> Weitere Informationen über Microsoft .NET Framework, Version 4.5.2  

> [!NOTE]  
> .NET 4.0, 4.5 und 4.5.1 werden nicht mehr unterstützt. Weitere Informationen finden Sie unter [Microsoft .NET Framework Support Lifecycle-Richtlinien – häufig gestellte Fragen](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Möglicherweise muss .NET Framework 4.5.2 neu gestartet werden, um die Installation abzuschließen. Der Benutzer sieht auf der Taskleiste die Benachrichtigung **Neustart erforderlich**. Für die folgenden allgemeinen Szenarios ist ein Neustart der Clientcomputer erforderlich:  

- .NET-Anwendungen oder -Dienste, die auf dem Computer ausgeführt werden.  

- Es fehlen ein oder mehrere Softwareupdates, die für die .NET-Installation erforderlich sind.  

- Der Computer wartet auf einen Neustart aufgrund einer vorherigen Installation von Softwareupdates für .NET Framework.  

Nach der Installation von .NET Framework 4.5.2 können weitere Updates erforderlich sein. Für diese späteren Updates muss der Computer möglicherweise mehrmals neu gestartet werden.  

### <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

Weitere Informationen finden Sie unter [Ermitteln der Standortsystemrollen für System Center Configuration Manager-Clients](plan/determine-the-site-system-roles-for-clients.md).  

|Komponente|Beschreibung|  
|---|---|  
|Verwaltungspunkt|Zum Bereitstellen des Konfigurations-Manager-Clients ist kein Verwaltungspunkt erforderlich. Ein Verwaltungspunkt ist für den Client zum Austauschen von Informationen mit dem Standort erforderlich. Ohne Verwaltungspunkt können Sie Clientcomputer nicht verwalten.|  
|Verteilungspunkt|Der Verteilungspunkt ist eine optionale Standortsystemrolle, deren Verwendung für die Clientbereitstellung und -verwaltung jedoch empfohlen wird. Alle Verteilungspunkte hosten die Clientquelldateien. Clients ermitteln den nächsten Verteilungspunkt, von dem sie die Quelldateien während der Clientbereitstellung oder des Updates herunterladen. Falls der Standort nicht über einen Verteilungspunkt verfügt, werden die Clientquelldateien von Computern vom jeweiligen Verwaltungspunkt heruntergeladen.|  
|Fallbackstatuspunkt|Der Fallbackstatuspunkt ist eine optionale Standortsystemrolle, deren Verwendung für die Clientbereitstellung jedoch empfohlen wird. Mithilfe des Fallbackstatuspunkts wird die Clientbereitstellung nachverfolgt, und es wird Computern am Configuration Manager-Standort ermöglicht, Zustandsmeldungen zu senden, wenn sie nicht mit einem Verwaltungspunkt kommunizieren können.|  
|Reporting Services-Punkt|Der Reporting Services-Punkt ist eine optionale aber empfohlene Standortsystemrolle. Sie zeigt Berichte im Zusammenhang mit der Clientbereitstellung und -verwaltung an. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../servers/manage/introduction-to-reporting.md).|  

### <a name="installation-method-dependencies"></a>Installationsmethodenabhängigkeiten  

Die folgenden Voraussetzungen gelten für die verschiedenen Clientinstallationsmethoden.  

#### <a name="client-push-installation"></a>Clientpushinstallation  

- Der Standort verwendet Clientpushinstallationskonten, um eine Verbindung mit Computern herzustellen und den Client zu installieren. Legen Sie diese Konten auf der Registerkarte **Konten** der Eigenschaften der Clientpushinstallation fest. Das Konto muss ein Mitglied der lokalen Gruppe „Administratoren“ auf dem Zielcomputer sein.  

    Wenn Sie kein Clientpushinstallationskonto angeben, wird das Konto des Standortservercomputers verwendet.  

- Der Standort muss den Computer ermitteln, auf dem Sie den Client installieren. Mindestens eine Configuration Manager-Ermittlungsmethode ist erforderlich.  

- Auf dem Computer ist eine ADMIN$-Freigabe vorhanden.  

- Aktivieren Sie in den Einstellungen der Clientpushinstallation die Option **Clientpushinstallation auf zugewiesenen Ressourcen aktivieren**, um den Konfigurations-Manager-Client automatisch per Push an ermittelte Ressourcen zu übertragen.  

- Der Clientcomputer muss mit einem Verteilungspunkt oder einem Verwaltungspunkt kommunizieren, um die Quelldateien herunterzuladen.  

- Clients müssen sich in einer vertrauenswürdigen Active Directory-Gesamtstruktur befinden, wenn Sie die gegenseitige Kerberos-Authentifizierung verwenden möchten. Kerberos hängt in Windows zur gegenseitigen Authentifizierung von Active Directory ab.<!--1358204-->  

Folgende Sicherheitsberechtigungen sind erforderlich, um den Clientpush verwenden zu können:  

- Konfigurieren des Clientpushinstallations-Kontos: Berechtigungen **Ändern** und **Lesen** für das Objekt **Standort**.  

- So verwenden Sie Clientpush, um den Client für Sammlungen, Geräte und Abfragen zu installieren: Berechtigungen **Ressource ändern** und **Lesen** für das Objekt **Sammlung**.  

Die Standardsicherheitsrolle **Infrastrukturadministrator** umfasst die für die Verwaltung von Clientpushinstallationen erforderlichen Berechtigungen.  

#### <a name="software-update-point-based-installation"></a>Auf einem Softwareupdatepunkt basierende Installation  

- Wenn Sie das Active Directory-Schema nicht erweitert haben oder Sie Clients aus einer anderen Gesamtstruktur installieren, verwenden Sie die Gruppenrichtlinie zum Bereitstellen von Installationsparametern für „CCMSetup.exe“. Weitere Informationen finden Sie unter [Bereitstellen von Clientinstallationseigenschaften](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Veröffentlichen Sie den Konfigurations-Manager-Client auf dem Softwareupdatepunkt.  

- Der Clientcomputer muss mit einem Verteilungspunkt oder einem Verwaltungspunkt kommunizieren, um die Quelldateien herunterzuladen.  

Die erforderlichen Sicherheitsberechtigungen zum Verwalten von Configuration Manager-Softwareupdates finden Sie unter [Voraussetzungen für Softwareupdates](../../../sum/plan-design/prerequisites-for-software-updates.md).  

#### <a name="group-policy-based-installation"></a>Auf einer Gruppenrichtlinie basierende Installation  

- Wenn Sie das Active Directory-Schema nicht erweitert haben oder Sie Clients aus einer anderen Gesamtstruktur installieren, verwenden Sie die Gruppenrichtlinie zum Bereitstellen von Installationsparametern für „CCMSetup.exe“. Weitere Informationen finden Sie unter [Bereitstellen von Clientinstallationseigenschaften](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Der Clientcomputer muss mit einem Verteilungspunkt oder einem Verwaltungspunkt kommunizieren, um die Quelldateien herunterzuladen.  

#### <a name="logon-script-based-installation"></a>Auf einem Anmeldeskript basierende Installation  

Der Clientcomputer muss mit einem Verteilungspunkt oder einem Verwaltungspunkt kommunizieren, um die Quelldateien herunterzuladen. Dies gilt nicht, wenn Sie „CCMSetup.exe“ über die folgende Befehlszeileneigenschaft angegeben haben: `ccmsetup /source`  

#### <a name="manual-installation"></a>Manuelle Installation  

Der Clientcomputer muss mit einem Verteilungspunkt oder einem Verwaltungspunkt kommunizieren, um die Quelldateien herunterzuladen. Dies gilt nicht, wenn Sie „CCMSetup.exe“ über die folgende Befehlszeileneigenschaft angegeben haben: `ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Installation von Microsoft Intune-MDM

- Erfordert ein Microsoft Intune-Abonnement und die entsprechenden Lizenzen  

- Für das Gerät ist Internetzugriff erforderlich, auch wenn es nicht internetbasiert ist.  

- Je nach Anwendungsfall kann eine oder beide der folgenden Technologien erforderlich sein:  

    - Azure Active Directory  

    - Cloudverwaltungsgateway  

#### <a name="workgroup-computer-installation"></a>Installation von Arbeitsgruppencomputern  

Konfigurieren Sie ein Netzwerkzugriffskonto für den Standort, um auf Ressourcen in der Domäne des Configuration Manager-Standortservers zugreifen zu können.  

Weitere Informationen zum Konfigurieren des Netzwerkzugriffskontos finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Auf einer Softwareverteilung basierende Installation (nur für Upgrades)  

- Wenn Sie das Active Directory-Schema nicht erweitert haben oder Sie Clients aus einer anderen Gesamtstruktur installieren, verwenden Sie die Gruppenrichtlinie zum Bereitstellen von Installationsparametern für „CCMSetup.exe“. Weitere Informationen finden Sie unter [Bereitstellen von Clientinstallationseigenschaften](deploy-clients-to-windows-computers.md#BKMK_Provision).

- Der Clientcomputer muss mit einem Verteilungspunkt oder einem Verwaltungspunkt kommunizieren, um die Quelldateien herunterzuladen.  

Die Sicherheitsberechtigungen, die für ein Upgrade des Configuration Manager-Clients über die Anwendungsverwaltung erforderlich sind, finden Sie unter [Sicherheit und Datenschutz für die Anwendungsverwaltung](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

#### <a name="automatic-client-upgrades"></a>Automatische Clientupgrades  

Sie müssen ein Mitglied der Sicherheitsrolle **Hauptadministrator** sein, um automatische Clientupgrades konfigurieren zu können.  

### <a name="firewall-requirements"></a>Firewallanforderungen  

Wenn sich zwischen den Standortsystemservern und den Computern, auf denen der Konfigurations-Manager-Client installiert werden soll, eine Firewall befindet, lesen Sie die Hinweise unter [Windows-Firewall- und -Porteinstellungen für Clients](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a> Voraussetzungen für Clients für mobile Geräte  

Mithilfe der folgenden Informationen können Sie die Voraussetzungen für die Installation des Configuration Manager-Clients auf mobilen Geräten bestimmen und diese registrieren.  

### <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager

- Eine Microsoft-Unternehmenszertifizierungsstelle (CA) mit Zertifikatvorlagen, um die Zertifikate bereitzustellen und zu verwalten, die für mobile Geräte erforderlich sind  

    Von der ausstellenden Zertifizierungsstelle müssen im Rahmen der Anmeldung automatisch Zertifikatanforderungen genehmigt werden, die von Benutzern mobiler Geräte übermittelt wurden.  

    Weitere Informationen zu Zertifikatanforderungen finden Sie unter [Sicherheit und Datenschutz für Zertifikatprofile](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

- Eine Sicherheitsgruppe mit Benutzern, die ihre mobilen Geräte anmelden können  

    Mit dieser Sicherheitsgruppe wird die im Rahmen der Anmeldung der mobilen Geräte verwendete Zertifikatvorlage konfiguriert.  

- Optional, jedoch empfohlen: ein DNS-Alias (CNAME-Eintrag) namens **ConfigMgrEnroll**. Konfigurieren Sie den Alias für den Servernamen des Anmeldungsproxypunkts.  

    Dieser DNS-Alias ist erforderlich, um die automatische Ermittlung für den Registrierungsdienst zu unterstützen. Wenn dieser DNS-Eintrag nicht konfiguriert wird, müssen Benutzer im Rahmen des Anmeldungsprozesses den Namen des Anmeldungsproxypunkts manuell angeben.  

- Abhängigkeiten der Standortsystemrollen für die Computer, auf denen die Standortsystemrollen „Anmeldungspunkt“ und „Anmeldungsproxypunkt“ ausgeführt werden  

    Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Standortsystemserver](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager

Weitere Informationen finden Sie unter [Ermitteln der Standortsystemrollen für System Center Configuration Manager-Clients](plan/determine-the-site-system-roles-for-clients.md).  

- Verwaltungspunkt, der für HTTPS-Clientverbindungen konfiguriert und für mobile Geräte aktiviert ist  

    Ein Verwaltungspunkt ist immer erforderlich, um den Configuration Manager-Client auf mobilen Geräten installieren zu können. Zusätzlich zu diesen Konfigurationsanforderungen (HTTPS-Unterstützung und für mobile Geräte aktiviert) muss der Verwaltungspunkt mit einem Internet-FQDN konfiguriert sein und Clientverbindungen über das Internet unterstützen.  

- Anmeldungspunkt und Anmeldungsproxypunkt  

    Mithilfe eines Anmeldungsproxypunkts werden Anmeldungsanforderungen von mobilen Geräten verwaltet. Der Anmeldungspunkt schließt den Anmeldungsprozess ab. Der Anmeldungspunkt muss sich in der gleichen Active Directory-Gesamtstruktur befinden wie der Standortserver. Der Anmeldungsproxypunkt kann sich dagegen in einer anderen Gesamtstruktur befinden.  

- Clienteinstellungen für die Anmeldung mobiler Geräte  

    Konfigurieren Sie Clienteinstellungen, damit Benutzer mobile Geräte anmelden können, und konfigurieren Sie mindestens ein Anmeldungsprofil.  

- Reporting Services-Punkt  

    Der Reporting Services-Punkt ist eine optionale, aber empfohlene Standortsystemrolle, über die Berichte zur Anmeldung mobiler Geräte und zur Clientverwaltung angezeigt werden können.  

    Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../servers/manage/introduction-to-reporting.md).  

- Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um die Anmeldung mobiler Geräte konfigurieren zu können:  

    - So können Sie die Standortsystemrollen für die Anmeldung hinzufügen, ändern und löschen: Berechtigung **Ändern** für das Objekt **Standort**.  

    - So können Sie Clienteinstellungen für die Anmeldung konfigurieren: Für die Standardclienteinstellungen ist die Berechtigung **Ändern** für das Objekt **Standort** und für benutzerdefinierte Clienteinstellungen die Berechtigung **Client-Agent** erforderlich.  

    Die Standardsicherheitsrolle **Hauptadministrator** umfasst die für die Konfiguration der Anmeldungsstandortsystemrollen erforderlichen Berechtigungen.  

- Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um angemeldete mobile Geräte verwalten zu können:  

    - So setzen Sie ein mobiles Gerät zurück oder außer Kraft: **Ressource löschen** für das Objekt **Sammlung**.  

    - So können Sie einen Befehl zum Zurücksetzen oder Außerkraftsetzen abbrechen: **Ressource löschen** für das Objekt **Sammlung**.  

    - So können Sie mobile Geräte zulassen oder blockieren: **Ressource ändern** für das Objekt **Sammlung**.  

    - So können Sie den Passcode auf einem mobilen Gerät remote sperren oder zurücksetzen: **Ressource ändern** für das Objekt **Sammlung**.  

    Die Standardsicherheitsrolle **Betriebsadministrator** umfasst die für die Verwaltung mobiler Geräte erforderlichen Berechtigungen.  

    Weitere Informationen zum Konfigurieren von Sicherheitsberechtigungen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../understand/fundamentals-of-role-based-administration.md) und [Konfigurieren der rollenbasierten Verwaltung](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Firewallanforderungen

Von beteiligten Netzwerkgeräten wie Routern und Firewalls (einschließlich der Windows-Firewall) muss der Datenverkehr der Anmeldung mobiler Geräte zugelassen werden.  

- Zwischen mobilen Geräten und dem Anmeldungsproxypunkt: HTTPS (standardmäßig TCP 443)  

- Zwischen dem Anmeldungsproxypunkt und dem Anmeldungspunkt: HTTPS (standardmäßig TCP 443)  

Wenn Sie einen Proxywebserver verwenden, muss dieser für SSL-Tunneling konfiguriert sein. Das SSL-Bridging wird auf mobilen Geräten nicht unterstützt.  
