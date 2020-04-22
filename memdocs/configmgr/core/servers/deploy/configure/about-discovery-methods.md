---
title: Ermittlungsmethoden
titleSuffix: Configuration Manager
description: Dieser Abschnitt enthält Informationen zu den verfügbaren Ermittlungsmethoden für die Suche nach Geräten in Ihrem Netzwerk über Active Directory oder Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 68e622d45de6575ec0f652f33934654cd1481dc2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704998"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>Ermittlungsmethoden für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mit Configuration Manager-Ermittlungsmethoden können Sie andere Geräte in Ihrem Netzwerk, Geräte und Benutzer aus Active Directory oder Geräte aus Azure AD (Azure Active Directory) suchen. Um effizient eine Ermittlungsmethode zu verwenden, sollten Sie die verfügbaren Konfigurationen und Einschränkungen kennen.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a> Active Directory-Gesamtstrukturermittlung  
 **Konfigurierbar:** Ja  

 **Standardmäßig aktiviert:** Nein  

 **Konten** zum Ausführen dieser Methode:  

-   **Active Directory-Gesamtstruktur-Ermittlungskonto** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

Im Unterschied zu anderen Active Directory-Ermittlungsmethoden werden von der Active Directory-Gesamtstrukturermittlung keine Ressourcen, die Sie verwalten können, erkannt. Stattdessen werden von dieser Methode in Active Directory konfigurierte Netzwerkadressen ermittelt. Sie kann diese Adressen für die Verwendung in der gesamten Hierarchie in Grenzen konvertieren.  

Wenn diese Methode ausgeführt wird, sucht sie in der lokalen Active Directory-Gesamtstruktur, in allen vertrauenswürdigen Gesamtstrukturen und in allen weiteren Gesamtstrukturen, die Sie im Knoten **Active Directory-Gesamtstrukturen** der Configuration Manager-Konsole konfigurieren.  

Verwenden Sie die Active Directory-Gesamtstrukturermittlung zu folgenden Zwecken:  

-   Ermitteln von Active Directory-Standorten und -Subnetzen und anschließendes Erstellen von Configuration Manager-Grenzen basierend auf diesen Netzwerkorten  

-   Identifizieren von Supernets, die einem Active Directory-Standort zugewiesen sind. Konvertieren der einzelnen Supernets in eine Bereichsbegrenzung für IP-Adressen.  

-   Veröffentlichen in AD DS (Active Directory Domain Services) in einer Gesamtstruktur bei aktivierter Veröffentlichung in dieser Gesamtstruktur. Das angegebene Konto für die Active Directory-Gesamtstruktur muss über Berechtigungen für diese Gesamtstruktur verfügen.  

Sie können die Active Directory-Gesamtstrukturermittlung in der Configuration Manager-Konsole verwalten. Navigieren Sie zum Arbeitsbereich **Verwaltung**, und erweitern Sie den Bereich **Hierarchiekonfiguration**.   

-   **Ermittlungsmethoden:** Hier können Sie die Ausführung der Active Directory-Gesamtstrukturermittlung am Standort der obersten Ebene Ihrer Hierarchie aktivieren. Sie können auch einen einfachen Zeitplan für die Ermittlung angeben. Konfiguriert die automatische Erstellung von Grenzen aus den ermittelten IP-Subnetzen und Active Directory-Standorten. Die Active Directory-Gesamtstrukturermittlung kann weder an untergeordneten primären Standorten noch an sekundären Standorten ausgeführt werden.  

-   **Active Directory-Gesamtstrukturen:** Hier können Sie die zusätzlich zu ermittelnden Gesamtstrukturen festlegen, die einzelnen Konten für die Active Directory-Gesamtstruktur angeben und die Veröffentlichung in den einzelnen Gesamtstrukturen konfigurieren. Überwacht den Ermittlungsprozess. Fügt IP-Subnetze und Active Directory-Standorte als Configuration Manager-Grenzen und Mitglieder von Begrenzungsgruppen hinzu.  

Zum Konfigurieren aller Standorte in einer Hierarchie für die Veröffentlichung in Active Directory-Gesamtstrukturen verbinden Sie die Configuration Manager-Konsole mit dem Standort auf der obersten Ebene der Hierarchie. Im Dialogfeld **Eigenschaften** eines Active Directory-Standorts werden auf der Registerkarte **Veröffentlichen** nur der aktuelle Standort und dessen untergeordnete Standorte angezeigt. Wenn die Veröffentlichung für eine Gesamtstruktur aktiviert ist und das Gesamtstrukturschema für Configuration Manager erweitert wurde, werden für jeden Standort, bei dem die Veröffentlichung in dieser Active Directory-Gesamtstruktur aktiviert ist, die folgenden Informationen veröffentlicht:  

-    **SMS-Standort-&lt;Standortcode>**

-   **SMS-MP-&lt;Standortcode>-&lt;System-Standortservername>**  

-   **SMS-SLP-&lt;Standortcode>-&lt;System-Standortservername>**  

-   **SMS-&lt;Standortcode>-&lt;Active Directory-Standortname oder Subnetz>**  

> [!NOTE]  
>  Die Veröffentlichung in Active Directory durch sekundäre Standorte erfolgt immer über das Computerkonto des sekundären Standortservers. Wenn Sie die Veröffentlichung durch sekundäre Standorte in Active Directory wünschen, stellen Sie sicher, dass das Computerkonto des sekundären Standortservers zur Veröffentlichung in Active Directory berechtigt ist. In einer nicht vertrauenswürdigen Gesamtstruktur können von einem sekundären Standort keine Daten veröffentlicht werden.  

> [!CAUTION]  
>  Wenn Sie die Option zum Veröffentlichen eines Standorts in einer Active Directory-Gesamtstruktur deaktivieren, werden alle bereits veröffentlichten Informationen dieses Standorts, einschließlich der verfügbaren Standortsystemrollen, aus Active Directory entfernt.  

Aktionen im Rahmen der Active Directory-Gesamtstrukturermittlung werden in den folgenden Protokollen aufgezeichnet:  

-   Alle Aktionen, mit Ausnahme von Aktionen im Zusammenhang mit der Veröffentlichung, werden auf dem Standortserver in der Datei **ADForestDisc.Log** im Ordner **&lt;InstallationPath>\Logs** aufgezeichnet.  

-   Veröffentlichungsaktionen im Zusammenhang mit der Active Directory-Gesamtstrukturermittlung werden auf dem Standortserver in den Dateien **hman.log** und **sitecomp.log** im Ordner **&lt;InstallationPath>\Logs** aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren von Ermittlungsmethoden](configure-discovery-methods.md#BKMK_ConfigADForestDisc).  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a> Active Directory-Gruppenermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Active Directory-Gesamtstruktur-Ermittlungskonto** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

> [!TIP]  
>  Neben den Informationen in diesem Abschnitt finden Sie weitere unter [Allgemeine Features von Active Directory-Gruppe, System und Ermittlung](#bkmk_shared).  

Verwenden Sie diese Methode zum Durchsuchen von Active Directory Domain Services, um Folgendes zu identifizieren:  

-   Lokale, globale und universelle Sicherheitsgruppen  

-   Mitgliedschaft in Gruppen  

-   Eingeschränkte Informationen über die Mitgliedscomputer und Benutzer einer Gruppe, auch wenn diese Computer und Benutzer zuvor nicht von einer anderen Ermittlungsmethode ermittelt wurden  

Mithilfe dieser Ermittlungsmethode lassen sich Gruppen sowie Gruppenbeziehungen der Mitglieder von Gruppen identifizieren. Standardmäßig werden nur Sicherheitsgruppen ermittelt. Sie können auch die Mitgliedschaften in Verteilergruppen ermitteln, indem Sie im Dialogfeld **Eigenschaften von Active Directory-Gruppenermittlung** auf der Registerkarte **Option** das Kontrollkästchen für die Option **Mitgliedschaft von Verteilergruppen ermitteln** aktivieren.  

Die Active Directory-Gruppenermittlung unterstützt nicht die erweiterten Active Directory-Attribute, die mithilfe der Active Directory-Systemermittlung oder der Active Directory-Benutzerermittlung identifiziert werden können. Da diese Ermittlungsmethode nicht für die Ermittlung von Computer- und Benutzerressourcen optimiert ist, sollten Sie sie ausführen, nachdem Sie die Active Directory-Systemermittlung und die Active Directory-Benutzerermittlung ausgeführt haben. Grund dafür ist, dass von dieser Methode ein vollständiger DDR (Discovery Data Record) für Gruppen erstellt wird, während für Computer und Benutzer, die Mitglieder von Gruppen sind, nur ein eingeschränkter DDR erstellt wird.  

Sie können die folgenden Ermittlungsbereiche konfigurieren; von diesen wird gesteuert, auf welche Art von dieser Methode nach Informationen gesucht wird:  

-   **Speicherort:** Verwenden Sie einen Speicherort, wenn Sie einen oder mehrere Active Directory-Container durchsuchen möchten. Diese Bereichsoption unterstützt eine rekursive Suche in den angegebenen Active Directory-Containern. Dieser Prozess durchsucht die einzelnen, von Ihnen angegebenen untergeordneten Container des Containers. Er wird fortgesetzt, bis keine untergeordneten Container mehr gefunden werden.  

-   **Gruppen:** Verwenden Sie Gruppen, wenn Sie eine oder mehrere bestimmte Active Directory-Gruppen durchsuchen möchten. Sie können die **Active Directory-Domäne** zum Verwenden von Standarddomäne und Standardgesamtstruktur konfigurieren, oder Sie können die Suche auf einen einzelnen Domänencontroller beschränken. Zusätzlich können Sie eine oder mehrere zu durchsuchende Gruppen angeben. Wenn Sie nicht mindestens eine Gruppe angeben, werden alle Gruppen, die am angegebenen **Active Directory-Domänenspeicherort** gefunden werden, durchsucht.  

> [!CAUTION]  
>  Wenn Sie einen Ermittlungsbereich konfigurieren, wählen Sie nur die Gruppen aus, die ermittelt werden müssen. Grund für diese Empfehlung ist, dass bei der Active Directory-Gruppenermittlung versucht wird, jedes Mitglied in allen Gruppen innerhalb des Ermittlungsbereichs zu ermitteln. Bei der Ermittlung großer Gruppen kann es zu einer übermäßigen Beanspruchung von Bandbreite und Active Directory-Ressourcen kommen.  

> [!NOTE]  
>  Je nachdem, was Sie ermitteln möchten, müssen Sie entweder die Active Directory-Systemerkennung oder die Active Directory-Benutzererkennung ausführen, um Sammlungen auf Basis von erweiterten Active Directory-Attributen zu erstellen und um zu gewährleisten, dass die Ermittlungsergebnisse für Computer und Benutzer korrekt sind.  

Die Aktionen der Active Directory-Gruppenermittlung werden in der Datei **adsgdis.log** im Ordner **&lt;InstallationPath\>\LOGS** auf dem Standortserver aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren von Ermittlungsmethoden](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a> Active Directory-Systemermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Konto für Active Directory-Systemermittlung** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

> [!TIP]  
>  Neben den Informationen in diesem Abschnitt finden Sie weitere unter [Allgemeine Features von Active Directory-Gruppe, System und Ermittlung](#bkmk_shared).  

Verwenden Sie diese Ermittlungsmethode, um nach den angegebenen Active Directory Domain Services-Speicherorten für Computerressourcen zu suchen, die zum Erstellen von Sammlungen und Abfragen verwendet werden können. Sie können auch Configuration Manager-Client für ein ermitteltes Gerät mithilfe der Clientpushinstallation installieren.  

Von dieser Methode werden standardmäßig grundlegende Informationen über den Computer einschließlich der folgenden Attribute ermittelt:  

-   Computername  

-   Betriebssystem und Version  

-   Active Directory-Containername  

-   IP-Adresse  

-   Active Directory-Standort  

-   Zeitstempel der letzten Anmeldung  

Damit erfolgreich ein DDR für einen Computer erstellt werden kann, muss das Computerkonto von der Active Directory-Systemermittlung identifiziert werden, und der Computername muss erfolgreich in eine IP-Adresse aufgelöst werden.  

Im Dialogfeld **Eigenschaften für Active Directory-Systemermittlung** können Sie auf der Registerkarte **Active Directory-Attribute** die vollständige Liste der ermittelten Standardobjektattribute anzeigen. Sie können die Methode auch zum Ermitteln zusätzlicher (erweiterter) Attribute konfigurieren.  

Die Aktionen der Active Directory-Systemermittlung werden in der Datei **adsysdis.log** im Ordner **&lt;InstallationPath\>\LOGS** auf dem Standortserver aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren von Ermittlungsmethoden](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a> Active Directory-Benutzerermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Konto für Active Directory-Benutzerermittlung** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

> [!TIP]  
>  Neben den Informationen in diesem Abschnitt finden Sie weitere unter [Allgemeine Features von Active Directory-Gruppe, System und Ermittlung](#bkmk_shared).  

Verwenden Sie diese Ermittlungsmethode zum Durchsuchen von Active Directory Domain Services, um Benutzerkonten und zugeordnete Attribute zu identifizieren. Standardmäßig ermittelt diese Methode grundlegende Informationen zum Benutzerkonto, einschließlich der folgenden Attribute:  

-   Benutzername  

-   Eindeutiger Benutzername (einschließlich Domänenname)  

-   Domain  

-   Active Directory-Containernamen  

Im Dialogfeld **Eigenschaften für Active Directory-Benutzerermittlung** können Sie auf der Registerkarte **Active Directory-Attribute** die vollständige Standardliste der ermittelten Objektattribute anzeigen. Sie können die Methode auch zum Ermitteln zusätzlicher (erweiterter) Attribute konfigurieren.

Die Aktionen der Active Directory-Benutzerermittlung werden in der Datei **adusrdis.log** im Ordner **&lt;InstallationPath\>\LOGS** auf dem Standortserver aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren von Ermittlungsmethoden](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a>Azure Active Directory-Benutzerermittlung

Mithilfe der Azure AD-Benutzerermittlung (Azure Active Directory) können Sie Ihr Azure AD-Abonnement nach Benutzern mit moderner Cloudidentität durchsuchen. Bei der Azure AD-Benutzerermittlung können folgende Attribute gesucht werden:

- ObjectId
- displayName
- mail
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName
- AAD tenantID
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistinguishedName

Diese Methode unterstützt sowohl die vollständige Synchronisierung als auch die Deltasynchronisierung von Benutzerdaten aus Azure AD. Die gewonnenen Informationen lassen sich gemeinsam mit Ermittlungsdaten aus anderen Ermittlungsmethoden verwenden.

Aktionen der Azure AD-Benutzerermittlung werden in der Datei **SMS_AZUREAD_DISCOVERY_AGENT.log** auf dem Standortserver der obersten Ebene in der Hierarchie gespeichert.

Informationen zur Konfiguration der Azure AD-Benutzerermittlung bei der Cloudverwaltung finden Sie unter [Konfigurieren von Azure-Diensten](azure-services-wizard.md). Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren der Azure AD-Benutzerermittlung](configure-discovery-methods.md#azureaadisc).

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Azure Active Directory-Benutzergruppenermittlung
<!--3611956-->
*(Eingeführt als [Vorabfeature](../../manage/pre-release-features.md) in Version 1906)*

Sie können Benutzergruppen und Mitglieder dieser Gruppen aus Azure Active Directory (Azure AD) ermitteln. Bei der Azure AD-Benutzergruppenermittlung können folgende Attribute gesucht werden:

- ObjectId
- displayName
- mailNickname
- onPremisesSecurityIdentifier
- AAD tenantID

Aktionen der Azure AD-Benutzergruppenermittlung werden in der Datei **SMS_AZUREAD_DISCOVERY_AGENT.log** auf dem Standortserver der obersten Ebene in der Hierarchie gespeichert. Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren der Azure AD-Benutzergruppenermittlung](configure-discovery-methods.md#bkmk_azuregroupdisco).

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a> Frequenzermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Ja  

**Konten** zum Ausführen dieser Methode:  

-   **Computerkonto** des Standortservers  

Die Frequenzermittlung unterscheidet sich von anderen Configuration Manager-Ermittlungsmethoden. Sie ist standardmäßig aktiviert und wird auf jedem Computerclient (statt auf einem Standortserver) ausgeführt, um einen DDR zu erstellen. Für mobile Geräteclients wird dieser DDR von dem Verwaltungspunkt erstellt, der vom mobilen Geräteclient verwendet wird. Es wird empfohlen, die Frequenzermittlung nicht zu deaktivieren, um den Datenbankdatensatz von Configuration Manager-Clients aufrechtzuerhalten. Zusätzlich zum Erhalt des Datenbankdatensatzes kann diese Methode die Ermittlung eines Computers als neuer Ressourcendatensatz erzwingen. Zudem kann sie den Datenbankdatensatz eines aus der Datenbank gelöschten Computers neu auffüllen.  

Die Frequenzermittlung wird in einem Zeitplan ausgeführt, der für alle Clients in der Hierarchie konfiguriert ist. Der Zeitplan für die Frequenzermittlung wird standardmäßig alle 7 Tage ausgeführt. Stellen Sie bei einer Änderung des Frequenzermittlungsintervalls sicher, dass die Frequenzermittlung häufiger als die Standortwartungstask **Veraltete Ermittlungsdaten löschen**ausgeführt wird. Diese Task löscht inaktive Clientdatensätze aus der Standortdatenbank. Sie können den Task **Veraltete Ermittlungsdaten löschen** nur für primäre Standorte konfigurieren. 

Sie können die Frequenzermittlung auch manuell auf einem bestimmten Client aufrufen. Führen Sie den **Ermittlungsdaten-Sammlungszyklus** auf der Registerkarte **Aktion** der Configuration Manager-Systemsteuerung eines Clients aus.  

Bei der Frequenzermittlung wird ein DDR erstellt, der die aktuellen Informationen des Clients enthält. Der Client kopiert anschließend diese kleine Datei (ca. 1 KB) an einen Verwaltungspunkt, damit sie von einem primären Standort verarbeitet werden kann. Die Datei enthält die folgenden Informationen:  

-   Netzwerkadresse  

-   NetBIOS-Name  

-   Version des Client-Agents  

-   Betriebsstatusdetails  

Die Frequenzermittlung ist die einzige Ermittlungsmethode, von der Details zum Clientinstallationsstatus bereitgestellt werden. Dabei wird das Clientattribut der Systemressource auf den Wert **Ja** aktualisiert.  

> [!NOTE]  
>  Selbst wenn die Frequenzermittlung deaktiviert ist, werden dennoch DDRs für aktive mobile Geräteclients erstellt und übermittelt. Durch dieses Verhalten wird sichergestellt, dass aktive mobile Geräte nicht durch die Task **Veraltete Ermittlungsdaten löschen** beeinträchtigt werden. Wenn ein Datenbankdatensatz für ein mobiles Gerät durch die Task **Veraltete Ermittlungsdaten löschen** gelöscht wird, wird auch das Gerätezertifikat aufgehoben. Durch diese Aktion wird das mobile Gerät blockiert, sodass es keine Verbindung mit Verwaltungspunkten herstellen kann.  

Frequenzermittlungsaktionen werden an den folgenden Speicherorten protokolliert:  

-   Für Computerclients werden Frequenzermittlungsaktionen auf dem Client in der Datei **InventoryAgent.log** im Ordner *%Windir%\CCM\Logs* aufgezeichnet.  

-   Für mobile Clients werden Frequenzermittlungsaktionen in der Datei **DMPRP.log** im Ordner *%Program Files%\CCM\Logs* des vom mobilen Geräteclient verwendeten Verwaltungspunkts aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren von Ermittlungsmethoden](configure-discovery-methods.md#BKMK_ConfigHBDisc).  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a> Netzwerkermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Computerkonto** des Standortservers  

Verwenden Sie diese Methode zum Ermitteln der Topologie Ihres Netzwerks und von Geräten in Ihrem Netzwerk, die über eine IP-Adresse verfügen. Bei der Netzwerkermittlung wird Ihr Netzwerk nach IP-fähigen Ressourcen durchsucht, indem folgende Entitäten abgefragt werden: 
- Server, auf denen eine Microsoft-Implementierung von DHCP ausgeführt wird
- ARP-Caches (Address Resolution Protocol) in Netzwerkroutern
- SNMP-fähige Geräte
- Active Directory-Domänen  

Falls Sie die Netzwerkermittlung verwenden möchten, müssen Sie die auszuführende *Ermittlungsebene* festlegen. Sie müssen außerdem mindestens einen Ermittlungsmechanismus konfigurieren, mit dessen Hilfe von der Netzwerkermittlung eine Abfrage nach Netzwerksegmenten oder -geräten ausgeführt werden kann. Außerdem können Sie Einstellungen festlegen, die die Steuerung von Ermittlungsaktionen im Netzwerk erleichtern. Abschließend definieren Sie mindestens einen Zeitplan für die Ausführung der Netzwerkermittlung.  

Die erfolgreiche Ermittlung einer Ressource mit dieser Methode setzt voraus, dass die IP-Adresse und die Subnetzmaske der Ressource von der Netzwerkermittlung identifiziert werden. Die folgenden Methoden werden verwendet, um die Subnetzmaske eines Objekts zu identifizieren:  

-   **Router-ARP-Cache:** Bei der Netzwerkermittlung wird der ARP-Cache eines Routers abgefragt, um Subnetzinformationen zu identifizieren. Daten in einem Router-ARP-Cache sind in der Regel nicht lange gültig. Wenn der ARP-Cache im Rahmen der Netzwerkermittlung abgefragt wird, sind Informationen zum angeforderten Objekt möglicherweise nicht mehr im ARP-Cache vorhanden.  

-   **DHCP:** Bei der Netzwerkermittlung wird jeder angegebene DHCP-Server abgefragt, um die Geräte zu ermitteln, für die eine Lease des DHCP-Servers verfügbar ist. Bei der Netzwerkermittlung werden nur DHCP-Server unterstützt, auf denen die Microsoft-Implementierung von DHCP ausgeführt wird.  

-   **SNMP-Gerät:** Bei der Netzwerkermittlung kann ein SNMP-Gerät direkt abgefragt werden. Damit ein Gerät bei der Netzwerkermittlung abgefragt werden kann, muss auf dem Gerät ein lokaler SNMP-Agent installiert sein. Zudem müssen Sie die Netzwerkermittlung für die Verwendung des Communitynamens konfigurieren, der vom SNMP-Agent verwendet wird.  

Wenn bei der Ermittlung ein IP-fähiges Objekt identifiziert wird und die Subnetzmaske des Objekts bestimmt werden kann, wird für dieses Objekt ein DDR erstellt. Da unterschiedliche Gerätetypen eine Verbindung mit dem Netzwerk herstellen, werden bei der Netzwerkermittlung Ressourcen ermittelt, die den Configuration Manager-Client nicht unterstützen. Zu den Geräten, die ermittelt, aber nicht verwaltet werden können, gehören beispielsweise Drucker und Router.  

Von der Netzwerkermittlung können mehrere Attribute als Teil des von ihr erstellten Ermittlungsdatensatzes zurückgegeben werden. Zu diesen Attributen gehören folgende:  

-   NetBIOS-Name  

-   IP-Adressen  

-   Domäne der Ressource  

-   Systemrollen  

-   SNMP-Communityname  

-   MAC-Adressen  

Die Netzwerkermittlungsaktivität wird in der Datei **Netdisc.log** im Ordner *&lt;InstallationPath\>\Logs* auf dem Standortserver aufgezeichnet, auf dem die Ermittlung ausgeführt wird.  

 Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren von Ermittlungsmethoden](configure-discovery-methods.md#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Durch komplexe Netzwerke und Verbindungen mit geringer Bandbreite kann die Ausführung der Netzwerkermittlung beeinträchtigt werden und ein starker Netzwerkdatenverkehr entstehen. Es wird empfohlen, die Netzwerkermittlung nur auszuführen, wenn die zu ermittelnden Ressourcen von den anderen Ermittlungsmethoden nicht gefunden werden. Die Netzwerkermittlung bietet sich beispielsweise an, wenn Sie Arbeitsgruppencomputer ermitteln müssen. Arbeitsgruppencomputer werden von anderen Ermittlungsmethoden nicht erkannt.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a> Ebenen der Netzwerkermittlung  
Beim Konfigurieren der Netzwerkermittlung stehen drei Ermittlungsebenen zur Auswahl:  

|Ermittlungsebene|Details|  
|------------------------|-------------|  
|Topologie|Auf dieser Ebene werden Router und Subnetze ermittelt. Es werden keine Subnetzmasken für Objekte identifiziert.|  
|Topologie und Client|Auf dieser Ebene werden zusätzlich zur Topologie auch potenzielle Clients wie Computer sowie Ressourcen wie Drucker und Router ermittelt. Es wird versucht, die Subnetzmaske der gefundenen Objekte zu identifizieren.|  
|Topologie, Client und Clientbetriebssystem|Auf dieser Ebene wird versucht, zusätzlich zur Topologie und zu potenziellen Clients den Namen und die Version des Computerbetriebssystems zu ermitteln. Dabei werden Windows-Browser- und Windows-Netzwerkaufrufe verwendet.|  

 Je höher die Stufe, desto stärker die Aktivität der Netzwerkermittlung und die Auslastung der Netzwerkbandbreite. Es empfiehlt sich, die Folgen für den Netzwerkdatenverkehr sorgfältig zu erwägen, bevor Sie alle Optionen der Netzwerkermittlung aktivieren.  

 Beispielsweise wäre es sinnvoll, sich beim ersten Einsatz der Netzwerkermittlung mit der Topologieebene zu begnügen und nur die Netzwerkinfrastruktur zu ermitteln. Konfigurieren Sie anschließend die Netzwerkermittlung neu, damit auch Objekte und deren Gerätebetriebssysteme ermittelt werden. Sie können auch Einstellungen konfigurieren, durch die die Netzwerkermittlung auf einen bestimmten Bereich von Netzwerksegmenten beschränkt wird. Auf diese Weise ermitteln Sie erforderliche Objekte in Netzwerkadressen und vermeiden unnötigen Netzwerkdatenverkehr. Dieser Prozess ermöglicht zudem die Ermittlung von Objekten von Edgeroutern oder außerhalb Ihres Netzwerks.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a> Optionen für die Netzwerkermittlung  
Damit bei der Netzwerkermittlung IP-fähige Geräte gesucht werden können, müssen Sie mindestens eine der folgenden Option konfigurieren.  

> [!NOTE]  
>  Die Netzwerkermittlung wird im Kontext des Computerkontos auf dem Standortserver, auf dem die Ermittlung ausgeführt wird, ausgeführt. Falls das Computerkonto keine Berechtigungen für eine nicht vertrauenswürdige Domäne hat, kann es vorkommen, dass von den Konfigurationen der Domäne und des DHCP-Servers keine Ressourcen ermittelt werden können.  

#### <a name="dhcp"></a>DHCP  

Geben Sie alle DHCP-Server an, die bei der Netzwerkermittlung abgefragt werden sollen. (Bei der Netzwerkermittlung werden nur DHCP-Server unterstützt, auf denen die Microsoft-Implementierung von DHCP ausgeführt wird.)  

-   Bei der Netzwerkermittlung werden Informationen mithilfe von Remoteprozeduraufrufen an die Datenbank auf dem DHCP-Server abgerufen.  

-   Bei der Netzwerkermittlung können sowohl 32-Bit- als auch 64-Bit-DHCP-Server nach einer Liste der Geräte abgefragt werden, die bei den einzelnen Servern registriert sind.  

-   Ein DHCP-Server kann bei der Netzwerkermittlung nur erfolgreich abgefragt werden, wenn das Computerkonto des Servers, auf dem die Ermittlung ausgeführt wird, ein Mitglied der DHCP-Benutzergruppe auf dem DHCP-Server ist. Beispielsweise ist diese Zugriffsebene gegeben, wenn eine der folgenden Aussagen zutrifft:  

    -   Der angegebene DHCP-Server ist der DHCP-Server des Servers, auf dem die Ermittlung ausgeführt wird.  

    -   Der Computer, auf dem die Ermittlung ausgeführt wird, und der DHCP-Server befinden sich in der gleichen Domäne.  

    -   Zwischen dem Computer, auf dem die Ermittlung ausgeführt wird, und dem DHCP-Server ist eine bidirektionale Vertrauensstellung vorhanden.  

    -   Der Standortserver ist ein Mitglied der DHCP-Benutzergruppe.  

-   Wenn bei der Netzwerkermittlung ein DHCP-Server aufgezählt wird, können statische IP-Adressen nicht immer ermittelt werden. Bei der Netzwerkermittlung werden keine IP-Adressen gefunden, die einem ausgeschlossenen IP-Adressbereich auf dem DHCP-Server angehören. IP-Adressen, die für die manuelle Zuweisung reserviert sind, werden ebenfalls nicht ermittelt.  

#### <a name="domains"></a>Domänen  

Geben Sie alle Domänen an, die bei der Netzwerkermittlung abgefragt werden sollen.  

-   Das Computerkonto des Standortservers, auf dem die Ermittlung ausgeführt wird, muss für die Domänencontroller in allen angegebenen Domänen über eine Leseberechtigung verfügen.  

-   Für die Ermittlung von Computern in der lokalen Domäne müssen Sie auf mindestens einem Computer den Computersuchdienst aktivieren. Der Computer muss sich dabei im gleichen Subnetz wie der Standortserver befinden, auf dem die Netzwerkermittlung ausgeführt wird.  

-   Bei der Netzwerkermittlung kann jeder Computer ermittelt werden, den Sie beim Durchsuchen des Netzwerks auf dem Standortserver anzeigen können.  

-   Bei der Netzwerkermittlung wird die IP-Adresse abgerufen. Anschließend wird mit einer ICMP-Echoanforderung (Internet Control Message-Protokoll) jedes gefundene Gerät gepingt. Mit dem Befehl **ping** können Sie feststellen, welche Computer zurzeit aktiv sind.  

#### <a name="snmp-devices"></a>SNMP-Geräte  

Geben Sie alle SNMP-Geräte an, die bei der Netzwerkermittlung abgefragt werden sollen.  

-   Bei der Netzwerkermittlung wird von jedem SNMP-Gerät, von dem keine Antwort auf die Abfrage eingeht, der Wert „ipNetToMediaTable“ abgerufen. Von diesem Wert werden Arrays von IP-Adressen zurückgegeben, bei denen es sich um Clientcomputer oder andere Ressourcen wie Drucker, Router oder sonstige IP-fähige Geräte handelt.  

-   Zum Abfragen eines Geräts müssen Sie die IP-Adresse oder den NetBIOS-Namen dieses Geräts angeben.  

-   Konfigurieren Sie die Netzwerkermittlung für die Verwendung des Communitynamens des Geräts. Andernfalls wird die SNMP-basierte Abfrage vom Gerät abgelehnt.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a> Beschränken der Netzwerkermittlung  
Beim Abfragen eines SNMP-Geräts am Rand des Netzwerks können bei der Netzwerkermittlung Informationen über Subnetze und SNMP-Geräte identifiziert werden, die sich außerhalb Ihres unmittelbaren Netzwerks befinden. Sie können mithilfe der folgenden Informationen die Netzwerkermittlung beschränken. Dazu konfigurieren Sie die SNMP-Geräte, bei denen die Kommunikation mit der Ermittlung möglich ist, und geben die abzufragenden Netzwerksegmente an.  

#### <a name="subnets"></a>Subnetze  

Konfigurieren Sie die Subnetze, die bei der Netzwerkermittlung abgefragt werden, sofern die Ermittlungsoptionen SNMP-Geräte und DHCP ausgewählt wurden. Bei diesen beiden Optionen werden nur die aktivierten Subnetze durchsucht.  

Beispielsweise können von einer DHCP-Anforderung Geräte von Orten im gesamten Netzwerk zurückgegeben werden. Falls Sie nur Geräte in einem bestimmten Subnetz ermitteln möchten, müssen Sie im Dialogfeld **Eigenschaften von Netzwerkermittlung** auf der Registerkarte **Subnetze** das jeweilige Subnetz angeben und aktivieren. Wenn Sie Subnetze angeben und aktivieren, beschränken Sie künftige DHCP- und SNMP-Ermittlungsaufgaben auf diese Subnetze.  

> [!NOTE]  
>  Die Objekte, die von der Ermittlungsoption **Domänen** ermittelt werden, werden durch die Subnetzkonfigurationen nicht beschränkt.  

#### <a name="snmp-community-names"></a>SNMP-Communitynamen  

Damit ein SNMP-Gerät erfolgreich abgefragt werden kann, müssen Sie beim Konfigurieren der Netzwerkermittlung den Communitynamen des Geräts angeben. Wird die Netzwerkermittlung nicht anhand des Communitynamens des SNMP-Geräts konfiguriert, wird die Abfrage vom Gerät abgelehnt.  

#### <a name="maximum-hops"></a>Maximale Hopanzahl  

Wenn Sie die maximale Anzahl der Routerhops festlegen, schränken Sie die Anzahl der Netzwerksegmente und Router ein, die von der Netzwerkermittlung mithilfe von SNMP abgefragt werden kann.  

Durch die konfigurierte Hopanzahl wird die Anzahl der zusätzlichen Geräte und Netzwerksegmente eingeschränkt, die bei der Netzwerkermittlung abgefragt werden können.  

Beispielsweise wird bei einer auf die Topologie beschränkten Ermittlung mit **0** (null) Routerhops das Subnetz ermittelt, in dem sich der ursprüngliche Server befindet. Alle Router in diesem Subnetz werden mit eingeschlossen.  

Im folgenden Diagramm ist dargestellt, was bei einer auf die Topologie beschränkten Abfrage der Netzwerkermittlung gefunden wird, wenn sie auf Server 1 ausgeführt wird und 0 Routerhops angegeben sind: Subnetz D und Router 1.  

 ![Bild der Ermittlung mit 0 (null) Routerjumps](media/Disc-0.gif)  

 Im folgenden Diagramm ist dargestellt, was bei einer Abfrage der Topologie- und Clientnetzwerkermittlung gefunden wird, wenn sie auf Server 1 ausgeführt wird und 0 Routerhops angegeben sind: Subnetz D, Router 1 und alle potenziellen Clients in Subnetz D.  

 ![Bild der Ermittlung mit 1 (einem) Routerjump](media/Disc-1.gif)  

 Damit Sie besser verstehen, wie Routerhops die Anzahl der ermittelten Netzwerkressourcen erhöhen können, stellen Sie sich folgendes Netzwerk vor:  

 ![Bild der Ermittlung mit 2 (zwei) Routerjumps](media/Disc-2.gif)  

 Beim Ausführen einer nur auf die Topologie bezogenen Netzwerkermittlung auf Server 1 mit einem einzigen Routerhop werden folgende Entitäten ermittelt:  

-   Router 1 und Subnetz 10.1.10.0 (nach 0 Hops gefunden)  

-   Subnetze 10.1.20.0 und 10.1.30.0, Subnetz A und Router 2 (auf dem ersten Hop gefunden)  

> [!WARNING]  
>  Durch jede Erhöhung der Anzahl von Routerhops kann die Anzahl der ermittelten Ressourcen deutlich erhöht und die von der Netzwerkermittlung verwendete Netzwerkbandbreite gesteigert werden.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a> Serverermittlung  
**Konfigurierbar:** Nein  

Zusätzlich zu den benutzerkonfigurierbaren Ermittlungsmethoden wird von Configuration Manager ein als **Serverermittlung** (SMS_WINNT_SERVER_DISCOVERY_AGENT) bezeichneter Prozess verwendet. Bei dieser Ermittlungsmethode werden Ressourceneinträge für Computer erstellt, bei denen es sich um Standortsysteme handelt. Dazu gehören beispielsweise Computer, die als Verwaltungspunkte konfiguriert sind.  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a> Allgemeine Funktionen der Active Directory-Gruppenermittlung, Systemermittlung und Benutzerermittlung  
Dieser Abschnitt enthält Informationen zu den Funktionen, die folgende Ermittlungsmethoden gemeinsam haben:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

> [!NOTE]  
>  Die Informationen in diesem Abschnitt gelten nicht für die Active Directory-Gesamtstrukturermittlung.  

Diese drei Ermittlungsmethoden ähneln sich im Hinblick auf Konfiguration und Betrieb. Sie dienen zum Ermitteln von Computern, Benutzern und Informationen über die Gruppenmitgliedschaften von Ressourcen, die in Active Directory Domain Services gespeichert sind. Der Ermittlungsprozess wird von einem Ermittlungs-Agent verwaltet. Der Agent wird an jedem Standort, für den eine Ausführung der Ermittlung konfiguriert wurde, auf dem Standortserver ausgeführt. Sie können für jede dieser Ermittlungsmethoden festlegen, dass mindestens ein Active Directory-Ort als Ortsinstanz in der lokalen Gesamtstruktur oder in Remotegesamtstrukturen durchsucht werden soll.  

Beim Durchsuchen einer als nicht vertrauenswürdig eingestuften Gesamtstruktur nach Ressourcen muss vom Ermittlungs-Agent Folgendes aufgelöst werden können:  

-   Der FQDN der Ressource muss vom Ermittlungs-Agent aufgelöst werden können, um eine Computerressource mit der Active Directory-Systemermittlung zu ermitteln. Ist dies nicht möglich, wird versucht, die Ressource anhand ihres NetBIOS-Namens aufzulösen.  

-   Der FQDN des von Ihnen für den Active Directory-Standort angegebenen Domänencontrollernamens muss vom Ermittlungs-Agent aufgelöst werden können, um eine Benutzer- oder eine Gruppenressource mit der Active Directory-Benutzerermittlung bzw. der Active Directory-Gruppenermittlung zu ermitteln.  

Sie können für jeden von Ihnen angegebenen Ort individuelle Suchoptionen konfigurieren. Beispielsweise können Sie das rekursive Durchsuchen der untergeordneten Active Directory-Container an diesen Standorten aktivieren. Außerdem können Sie ein eindeutiges Konto konfigurieren, das beim Durchsuchen dieses Orts verwendet werden soll. Dieses Konto bietet somit die flexible Möglichkeit, eine Ermittlungsmethode an einem Standort zu konfigurieren, um mehrere Active Directory-Standorte in mehreren Gesamtstrukturen zu durchsuchen. Es ist nicht erforderlich, ein einzelnes Konto mit Berechtigungen für sämtliche Standorte zu konfigurieren.  

Bei der Ausführung dieser drei Ermittlungsmethoden an einem bestimmten Standort wird vom Configuration Manager-Standortserver an diesem Standort eine Verbindung mit dem nächstgelegenen Domänencontroller in der angegebenen Active Directory-Gesamtstruktur hergestellt, um Active Directory-Ressourcen zu suchen. Die Domäne und die Gesamtstruktur können in einem beliebigen unterstützten Active Directory-Modus befinden. Das Konto, das Sie jeder Standortinstanz zuweisen, muss über die Berechtigung **Lesen** für die angegebenen Active Directory-Standorte verfügen.

Bei der Ermittlung werden zunächst die angegebenen Orte nach Objekten durchsucht. Anschließend wird versucht, Informationen über diese Objekte zu sammeln. Falls genügend Informationen zu einer Ressource identifiziert werden können, wird ein DDR erstellt. Welche Informationen erforderlich sind, hängt jeweils von der verwendeten Ermittlungsmethode ab.  

Sie können die gleiche Ermittlungsmethode für die Ausführung an mehreren Configuration Manager-Standorten konfigurieren, um den Vorteil von Abfragen an die lokalen Active Directory-Server zu nutzen. In diesem Fall können Sie jeden Standort mit einem eindeutigen Satz von Ermittlungsoptionen konfigurieren. Da die Ermittlungsdaten für alle Standorte in der Hierarchie freigegeben werden, sollten Sie ein Überlappen zwischen diesen Konfigurationen vermeiden, um jede Ressource effektiv ein Mal ermitteln zu können.

Führen Sie bei kleineren Umgebungen unter Umständen alle Ermittlungsmethoden an nur einem Standort in Ihrer Hierarchie aus. Diese Konfiguration reduziert den Verwaltungsmehraufwand und die Wahrscheinlichkeit, dass bei mehreren Ermittlungsaktionen die gleichen Ressourcen neu ermittelt werden. Wenn Sie die Anzahl der Standorte, an denen die Ermittlung ausgeführt wird, auf ein Mindestmaß beschränken, verringern Sie die bei der Ermittlung verwendete Netzwerkbandbreite insgesamt. Sie können auch die Anzahl der DDRs reduzieren, die erstellt und von Ihren Standortservern verarbeitet werden müssen.  

Viele Konfigurationen von Ermittlungsmethoden sind selbsterklärend. In den nachfolgenden Abschnitten finden Sie weitere Informationen, die Sie möglicherweise benötigen, bevor Sie sie die entsprechenden Ermittlungsoptionen konfigurieren.  

Die folgenden Optionen stehen für die Verwendung mit mehreren Active Directory-Ermittlungsmethoden zur Verfügung:  

-   [Deltaermittlung](#bkmk_delta)  

-   [Filtern veralteter Computerdatensätze bei der Domänenanmeldung](#bkmk_stalelogon)  

-   [Filtern veralteter Datensätze nach Computerkennwort](#bkmk_stalepassword)  

-   [Suchen nach benutzerdefinierten Attributen von Active Directory](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a> Deltaermittlung  
Verfügbar für:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

Deltaermittlung ist eine unabhängige Ermittlungsmethode, jedoch als Option für die entsprechenden Methoden verfügbar. Die Deltaermittlung sucht bestimmte Active Directory-Attribute für Änderungen, die seit dem letzten vollständigen Ermittlungszyklus der entsprechenden Ermittlungsmethode vorgenommen wurden. Die Attributänderungen werden an die Configuration Manager-Datenbank gesendet, um den Ermittlungsdatensatz der Ressource zu aktualisieren.  

Die Deltaermittlung wird standardmäßig in einem Fünfminutenzyklus ausgeführt. Dieser Zeitplan erfolgt sehr viel häufiger, als der normale Zeitplan für einen vollständigen Ermittlungszyklus vorsieht. Dieser häufige Zyklus ist möglich, da Deltaermittlung weniger Standortserver- und Netzwerkressourcen verwendet als ein vollständiger Ermittlungszyklus. Bei der Verwendung der Deltaermittlung können Sie die Häufigkeit des vollständigen Ermittlungszyklus der betreffenden Ermittlungsmethode reduzieren.  

Die gängigsten Änderungen, die von der Deltaermittlung erkannt werden, sind:  

-   Neue Computer oder Benutzer, die Active Directory hinzugefügt wurden  

-   Änderungen an grundlegenden Computer- und Benutzerinformationen  

-   Neue Computer oder Benutzer, die einer Gruppe hinzugefügt wurden  

-   Computer oder Benutzer, die aus einer Gruppe entfernt wurden  

-   Änderungen an Systemgruppenobjekten  

Bei der Deltaermittlung können zwar neue Ressourcen und Änderungen an der Gruppenmitgliedschaft erkannt werden, jedoch nicht, ob eine Ressource aus Active Directory gelöscht wurde. DDRs, die von der Deltaermittlung erstellt werden, werden wie von einem vollständigen Ermittlungszyklus erstellte DDRs verarbeitet.  

Die Deltaermittlung wird in den Eigenschaften einer Ermittlungsmethode auf der Registerkarte **Abfragezeitplan** konfiguriert.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a> Filtern veralteter Computerdatensätze bei der Domänenanmeldung  
Verfügbar für:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

Sie können die Ermittlung so konfigurieren, dass Computer mit veralteten Computerdatensätzen ausgeschlossen werden. Dieser Ausschluss basiert auf der letzten Domänenanmeldung des Computers. Wenn diese Option aktiviert ist, wird jeder identifizierte Computer von der Active Directory-Systemermittlung ausgewertet. Von der Active Directory-Gruppenermittlung wird jeder Computer ausgewertet, der Mitglied in einer ermittelten Gruppe ist.  

Voraussetzungen für die Verwendung dieser Option:  

-   Computer müssen so konfiguriert werden, dass das Attribut **LastLogonTimeStamp** in Active Directory Domain Services aktualisiert wird.  

-   Die Active Directory-Domänenfunktionsebene muss auf Windows Server 2003 oder höher festgelegt sein.  

Berücksichtigen Sie das Intervall der Replikation zwischen Domänencontrollern, wenn Sie die Zeit nach der letzten Anmeldung konfigurieren, die Sie für diese Einstellung verwenden möchten.  

Sie konfigurieren die Filterung auf der Registerkarte **Option** in den Dialogfeldern **Eigenschaften von Active Directory-Systemermittlung** und **Eigenschaften von Active Directory-Gruppenermittlung**. Wählen Sie die Option **Nur Computer ermitteln, die in einem bestimmten Zeitraum bei einer Domäne angemeldet waren** aus.  

> [!WARNING]  
>  Wenn Sie diesen Filter konfigurieren und **Filtern veralteter Datensätze nach Computerkennwort** verwenden, werden Computer, die die Kriterien mindestens eines Filters erfüllen, von der Ermittlung ausgeschlossen.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a> Filtern veralteter Datensätze nach Computerkennwort  
Verfügbar für:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

Sie können die Ermittlung so konfigurieren, dass Computer mit veralteten Computerdatensätzen ausgeschlossen werden. Dieser Ausschluss basiert auf der letzten Kennwortaktualisierung des Computerkontos vom Computer. Wenn diese Option aktiviert ist, wird jeder identifizierte Computer von der Active Directory-Systemermittlung ausgewertet. Von der Active Directory-Gruppenermittlung wird jeder Computer ausgewertet, der Mitglied in einer ermittelten Gruppe ist.  

Voraussetzungen für die Verwendung dieser Option:  

-   Computer müssen so konfiguriert werden, dass das Attribut **pwdLastSet** in Active Directory Domain Services aktualisiert wird.  

Wenn Sie diese Option konfigurieren, sollten Sie das Intervall für Updates für dieses Attribut berücksichtigen. Berücksichtigen Sie auch das Replikationsintervall zwischen Domänencontrollern.  

Sie konfigurieren die Filterung auf der Registerkarte **Option** in den Dialogfeldern **Eigenschaften von Active Directory-Systemermittlung** und **Eigenschaften von Active Directory-Gruppenermittlung**. Wählen Sie die Option **Nur Computer ermitteln, von denen in einem bestimmten Zeitraum das Kennwort für das Computerkonto aktualisiert wurde**.  

> [!WARNING]  
>  Wenn Sie diesen Filter konfigurieren und **Filtern veralteter Datensätze nach Domänenanmeldung** verwenden, werden Computer, die die Kriterien mindestens eines Filters erfüllen, von der Ermittlung ausgeschlossen.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a> Suchen nach benutzerdefinierten Attributen von Active Directory  
 Verfügbar für:  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

Von jeder Ermittlungsmethode wird eine eindeutige Liste von Active Directory Attributen, die ermittelt werden können, unterstützt.  

Prüfen und konfigurieren Sie die Liste benutzerdefinierter Attribute auf der Registerkarte **Active Directory-Attribute** im Dialogfeld **Eigenschaften der Active Directory-Systemermittlung** und im Dialogfeld **Eigenschaften der Active Directory-Benutzerermittlung**.  
