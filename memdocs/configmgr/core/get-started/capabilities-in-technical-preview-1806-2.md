---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über neue Features, die mit der Technical Preview-Version 1806.2 für System Center Configuration Manager zur Verfügung stehen.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 93d37ae321ec35fe8de83626f1c5963cb663882d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695998"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Funktionen in der Technical Preview 1806.2 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1806.2 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um Funktionen für Ihren Technical Preview-Standort zu aktualisieren oder neue Funktionen hinzuzufügen. 

Lesen Sie den [Technical Preview](technical-preview.md)-Artikel vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>Bekannte Probleme in dieser Technical Preview

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a> Clients werden nicht automatisch aktualisiert.
<!--518760-->
Bei der Aktualisierung auf Version 1806.2 aktualisiert der Standort außerdem SQL Native Client, was zu einem ausstehenden Neustart auf dem Standortserver führen kann. Diese Verzögerung bewirkt, dass bestimmte Dateien nicht aktualisiert werden, was sich auf das automatische Clientupgrade auswirkt.

#### <a name="workarounds"></a>Problemumgehung
Umgehen Sie dieses Problem mit einem manuellen Upgrade des SQL Native Client *vor dem Aktualisieren* von Configuration Manager auf Version 1806.2. Weitere Informationen finden Sie unter [Neuestes QFE-Update für Microsoft® SQL Server® 2012 Native Client verfügbar](https://www.microsoft.com/download/details.aspx?id=50402).

Wenn Sie Ihre Website bereits aktualisiert haben, funktionieren automatisches Clientupgrade und Clientpushinstallation nicht. Sie müssen die Clients zum vollständigen Testen der meisten neuen Features aktualisieren. Aktualisieren Sie die Technical Preview-Clients mithilfe des folgenden Prozesses manuell:  

1. Suchen Sie die Clientquelldateien im **CMUClient**-Ordner auf dem Standortserver des Configuration Manager-Installationsverzeichnisses. Beispiel: `C:\Program Files\Configuration Manager\CMUClient`  

2. Kopieren Sie den gesamten CMUClient-Ordner auf das Clientgerät. Beispiel: `C:\Temp\CMUClient`  

    Dieser Speicherort kann eine Netzwerkfreigabe sein, die von den Clients aus zugänglich ist.  

3. Führen Sie die folgende Befehlszeile von einer Eingabeaufforderung mit erhöhten Rechten aus: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Wenn Sie einen neuen Client an Ihrem Technical Preview-Version 1806.2-Standort installieren, wenden Sie den gleichen Vorgang an. 

> [!Important]  
> Verwenden Sie in diesem Szenario nicht den `/MP`-Befehlszeilenparameter. Dieser Parameter hat Vorrang vor `/source` und bewirkt, dass ccmsetup Clientinhalte vom Verwaltungs- oder Verteilungspunkt herunterlädt.
> 
> Befehlszeileneigenschaften wie SMSSITECODE oder CCMLOGLEVEL können verwendet werden, sollten jedoch beim Aktualisieren eines vorhandenen Clients nicht erforderlich sein. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a> Version 1806.2 zeigt Version 1806 in Info zu Configuration Manager an
<!--518148-->
Wenn Sie nach dem Upgrade auf Technical Preview-Version 1806.2 in der linken oberen Ecke der Konsole das Fenster **Info zu Configuration Manager** öffnen, wird weiterhin **Version 1806** angezeigt. 

#### <a name="workaround"></a>Problemumgehung
Bestimmen Sie mit der Eigenschaft **Standortversion** den Unterschied zwischen 1806 und 1806.2:

| Standortversion  | Version
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a> Verbesserungen an Bereitstellungen in Phasen

Dieses Release umfasst die folgenden Verbesserungen an [Bereitstellungen in Phasen](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md):
- [Status der Bereitstellung in Phasen](#bkmk_pod-monitor)
- [Bereitstellung von Anwendungen in Phasen](#bkmk_pod-app)
- [Schrittweiser Rollout während Bereitstellungen in Phasen](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a> Status der Bereitstellung in Phasen
<!--1358577-->
Bereitstellungen in Phasen verfügen jetzt über eine native Überwachungsoberfläche. Wählen Sie im Knoten **Bereitstellungen** im Arbeitsbereich **Überwachung** eine Bereitstellung in Phasen aus, und klicken Sie dann im Menüband auf **Status der Bereitstellung in Phasen**.

![Dashboard zum Status der Bereitstellung in Phasen mit Status von zwei Phasen](media/1358577-phased-deployment-status.png)

Dieses Dashboard zeigt für jede Phase in der Bereitstellung die folgenden Informationen an:  

- **Geräte gesamt:** auf wie viele Geräte sich diese Phase auswirkt.  

- **Status:** der aktuelle Status dieser Phase. Jede Phase kann einen der folgenden Zustände aufweisen:  

    - **Bereitstellung erstellt:** Bei der Bereitstellung in Phasen wurde eine Bereitstellung der Software für die Sammlung für diese Phase erstellt. An Clients wird diese Software gesendet.  

    - **Warten:** Da die vorherige Phase noch nicht die Erfolgskriterien für die Bereitstellung erfüllt hat, kann noch nicht mit dieser Phase fortgefahren werden.  

    - **Angehalten:** Ein Administrator hat die Bereitstellung angehalten.  

- **Fortschritt:** die farbcodierten Bereitstellungszustände von Clients. Beispiel: „Erfolg“, „In Bearbeitung“, „Fehler“, „Anforderungen nicht erfüllt“ und „Unbekannt“. 


#### <a name="known-issue"></a>Bekanntes Problem
Das Dashboard zum Status der Bereitstellung in Phasen zeigt möglicherweise mehrere Zeilen für die gleiche Phase an.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a> Bereitstellung von Anwendungen in Phasen
<!--1358147-->
Erstellen Sie in Phasen unterteilte Bereitstellungen von Anwendungen. Mithilfe von Bereitstellungen in Phasen können Sie einen koordinierten, sequenzierten Softwarerollout basierend auf anpassbaren Kriterien und Gruppen orchestrieren.

Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie **Anwendungen** aus. Wählen Sie eine Anwendung aus, und klicken Sie dann im Menüband auf **Stufenweise Bereitstellung erstellen**. 

Das Verhalten der stufenweisen Bereitstellung einer Anwendung entspricht der bei Tasksequenzen. Weitere Informationen finden Sie unter [Erstellen einer Bereitstellung in Phasen für eine Tasksequenz](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Voraussetzung
Verteilen Sie den Inhalt für die Anwendung an einem Verteilungspunkt, bevor Sie die in Phasen unterteilte Bereitstellung erstellen.<!--518293-->

#### <a name="known-issue"></a>Bekanntes Problem
Sie können Phasen für eine Anwendung nicht manuell erstellen. Der Assistent erstellt automatisch zwei Phasen für Bereitstellungen von Anwendungen.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a> Schrittweiser Rollout während Bereitstellungen in Phasen
<!--1358578-->
Während einer Bereitstellung in Phasen kann der Rollout in jeder Phase jetzt schrittweise erfolgen. Dieses Verhalten mindert das Risiko von Bereitstellungsproblemen und verringert die Belastung des Netzwerks durch die Verteilung von Inhalten an Clients. Der Standort kann die Software abhängig von der Konfiguration nach und nach für die einzelnen Phasen verfügbar machen. Für jeden Client in einer Phase gilt eine zu dem Zeitpunkt, zu dem die Software zur Verfügung gestellt wird, relative Frist. Das Zeitfenster zwischen dem Zeitpunkt der Verfügbarkeit und der Frist ist für alle Clients in einer Phase identisch. 

Wenn Sie eine stufenweise Bereitstellung erstellen und eine Phase manuell konfigurieren, legen Sie auf der Seite **Phaseneinstellungen** des Assistenten zum Hinzufügen einer Phase oder der Seite **Einstellungen** des Assistenten für das Erstellen einer stufenweisen Bereitstellung folgende Option fest: **Diese Software in diesem Zeitraum (in Tagen) schrittweise zur Verfügung stellen**. Der Standardwert für diese Einstellung ist **0** (null), sodass die Bereitstellung standardmäßig nicht gedrosselt ist.

> [!Note]  
> Diese Option ist derzeit nur für Bereitstellungen von Tasksequenzen in Phasen verfügbar.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a> Unterstützung für neue Windows-App-Paketformate
<!--1357427-->
Configuration Manager unterstützt jetzt die Bereitstellung der neuen Formate für Windows 10-App-Pakete (.msix) und App-Bundles (.msixbundle). Die neuesten Builds von [Windows Insider Preview](https://insider.windows.com/) unterstützen derzeit diese neuen Formate.

Eine Übersicht über MSIX finden Sie unter [A closer look at MSIX (MSIX von Nahem betrachtet)](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Informationen zum Erstellen einer neuen MSIX-App finden Sie unter [MSIX support introduced in Insider Build 17682 (Einführung der MSIX-Unterstützung in Insider Build 17682)](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Voraussetzungen
- Ein Windows 10-Client, auf dem mindestens Windows Insider Preview-Build 17682 ausgeführt wird
- Ein Windows-App-Paket im MSIX-Format

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. [Erstellen Sie eine Anwendung](../../apps/deploy-use/create-applications.md) in der Configuration Manager-Konsole. 
2. Wählen Sie als **Typ** der Installationsdatei für die Anwendung **Windows-App-Paket (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** aus.
3. [Stellen Sie die Anwendung bereit](../../apps/deploy-use/deploy-applications.md) für den Client, der den aktuellen Windows Insider Preview-Build ausführt.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a> Verbesserung der Clientpushsicherheit
<!--1358204-->
Bei Verwendung der [Clientpushmethode](../clients/deploy/plan/client-installation-methods.md#client-push-installation) zum Installieren des Configuration Manager-Clients stellt der Standortserver eine Remoteverbindung mit dem Client her, um die Installation zu starten. Ab diesem Release kann der Standort gegenseitige Kerberos-Authentifizierung erfordern, indem vor dem Herstellen der Verbindung kein Fallback auf NTLM zugelassen wird. Diese Verbesserung sichert die Kommunikation zwischen dem Server und dem Client. 

Je nach Ihren Sicherheitsrichtlinien kann Ihre Umgebung möglicherweise bereits Kerberos gegenüber älteren NTLM-Authentifizierungen bevorzugen oder erfordern. Weitere Informationen zu den Sicherheitsüberlegungen dieser Authentifizierungsprotokolle finden Sie unter den [Sicherheitserwägungen](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Voraussetzung

Um dieses Feature verwenden zu können, müssen Clients sich in einer vertrauenswürdigen Active Directory-Gesamtstruktur befinden. Kerberos hängt in Windows zur gegenseitigen Authentifizierung von Active Directory ab. 


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

Wenn Sie den Standort aktualisieren, bleibt das vorhandene Verhalten erhalten. Sobald Sie die Eigenschaften der Clientpushinstallation *geöffnet* haben, aktiviert der Standort automatisch die Kerberos-Überprüfung. Bei Bedarf können Sie ein Fallback der Verbindung zulassen, um eine weniger sichere NTLM-Verbindung zu verwenden – dies wird jedoch nicht empfohlen. 

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Wählen Sie den Zielstandort aus. Klicken Sie im Menüband auf **Clientinstallationseinstellungen**, und wählen Sie **Clientpushinstallation** aus.  

2. Der Standort hat nun die Kerberos-Überprüfung für die Clientpushinstallation aktiviert. Klicken Sie auf **OK**, um das Fenster zu schließen.  

3. Falls es für Ihre Umgebung erforderlich ist, steht ihnen im Fenster „Clientpushinstallations-Eigenschaften“ auf der Registerkarte **Allgemein** die Option **Verbindungsfallback auf NTLM zulassen** zur Verfügung. Diese Option ist standardmäßig deaktiviert. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a> Einblicke für die Verwaltung für proaktive Wartung
<!--1352184,et al-->
Zusätzliche Einblicke für die Verwaltung sind in diesem Release verfügbar, um potenzielle Konfigurationsprobleme hervorzuheben. Beachten Sie die folgenden Regeln in der neuen Gruppe **Proaktive Wartung**:  

- **Nicht verwendete Konfigurationselemente**: Konfigurationselemente, die nicht Teil einer Konfigurationsbaseline und älter als 30 Tage sind.  

- **Nicht verwendete Startimages**: Startimages, auf die nicht für die Verwendung für PXE-Start oder Tasksequenz verwiesen wird.  

- **Begrenzungsgruppen ohne zugewiesene Standortsysteme**: Ohne zugewiesene Standortsysteme können Begrenzungsgruppen nur zur Standortzuweisung verwendet werden.  

- **Begrenzungsgruppen ohne Mitglieder**: Begrenzungsgruppen sind nicht für Standortzuweisung oder Inhaltssuche anwendbar, wenn sie keine Mitglieder enthalten.  

- **Verteilungspunkte, die keinen Inhalt für Clients bereitstellen**: Verteilungspunkte, die in den letzten 30 Tagen keine Inhalte für Clients zur Verfügung gestellt haben. Diese Daten basieren auf Berichten von Clients zu ihrem Downloadverlauf.  

- **Abgelaufene Updates gefunden:** Abgelaufene Updates sind nicht für die Bereitstellung anwendbar.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a> Übergang von Mobile Apps-Workload für gemeinsam verwaltete Geräte
<!--1357892-->
Verwalten Sie mobile Apps mit Microsoft Intune, während Sie weiterhin Configuration Manager verwenden, um Windows-Desktopanwendungen bereitzustellen. Wechseln Sie für den Übergang der Moderne Apps-Workload zur Eigenschaftenseite für die gemeinsame Verwaltung. Bewegen Sie den Schieberegler von Configuration Manager zu „Pilot“ oder „alle“. 

Nachdem Sie diese Workload umgestellt haben, sind alle über Intune bereitgestellten verfügbaren Apps im Unternehmensportal verfügbar. Apps, die Sie im Configuration Manager bereitstellen, sind im Softwarecenter verfügbar. 

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Co-Verwaltung für Windows 10-Geräte](../../comanage/overview.md)  

- [Was ist Microsoft Intune-App-Verwaltung?](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> Begrenzungsgruppenoptionen für Peerdownloads
<!--1356193-->
Begrenzungsgruppen beinhalten nun zusätzliche Einstellungen, die Ihnen mehr Kontrolle über die Verteilung von Inhalten in Ihrer Umgebung einräumen. Dieses Release bietet die folgenden Optionen:  

- **Peerdownloads in dieser Begrenzungsgruppe zulassen:** Diese Einstellung ist standardmäßig aktiviert. Der Verwaltungspunkt bietet Clients eine Liste der Speicherorte für Inhalt, die Peerquellen enthält. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    In zwei häufigen Szenarios sollten Sie erwägen, diese Option zu deaktivieren:  

    - Wenn Sie eine Begrenzungsgruppe besitzen, die Grenzen von geografisch verstreuten Speicherorten wie einem VPN enthält. Zwei Clients können sich in der gleichen Begrenzungsgruppe befinden, da sie über VPN verbunden sind, aber an höchst unterschiedlichen Speicherorten, die zur Peerfreigabe von Inhalten nicht geeignet sind.  

    - Bei Verwendung einer einzigen, großen Begrenzungsgruppe für die Standortzuweisung, die nicht auf Verteilungspunkte verweist.  

- **Bei Peerdownloads nur Peers in demselben Subnetz verwenden:** Diese Einstellung ist abhängig von der davor. Wenn Sie diese Option aktivieren, enthält der Verwaltungspunkt nur in der Inhaltsspeicherort-Liste Peerquellen, die sich im gleichen Subnetz wie der Client befinden.

    Allgemeine Szenarien für die Aktivierung dieser Option:

    - Ihr Begrenzungsgruppenentwurf für die Inhaltsverteilung enthält eine große Begrenzungsgruppe, die andere kleinere Begrenzungsgruppen überlappt. Mit dieser neuen Einstellung enthält die Liste der Inhaltsquellen, die der Verwaltungspunkt für Clients bereitstellt, nur Peerquellen aus demselben Subnetz.

    - Sie haben eine einzelne große Begrenzungsgruppe für alle Remotebüro-Standorte. Wenn Sie diese Option aktivieren, teilen Clients nur Inhalte innerhalb des Subnetzes am Remotebüro-Standort, anstatt zu riskieren, Inhalte mit anderen Standorten zu teilen.


### <a name="known-issue"></a>Bekanntes Problem
Verfügt der Peerquellenclient über mehrere IP-Adressen (IPv4, IPv6 oder beide), funktioniert das Peercaching nicht. Die neue Option **Während Peerdownloads nur Peers im gleichen Subnetz verwenden** hat keine Auswirkungen, wenn die Peerquelle über mehrere IP-Adressen verfügt.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a> Unterstützung für benutzerdefinierte Kataloge für Drittanbieter-Softwareupdates
<!--1358714-->
Aufgrund Ihres [UserVoice-Feedbacks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) unterstützt dieses Release weiterhin Updates für Drittanbietersoftware. [Technical Preview-Version 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) bietet Unterstützung für *Partnerkataloge*. Dabei handelt es sich um registrierte Kataloge von Softwareherstellern. Von Ihnen erstellte Kataloge, die nicht bei Microsoft registriert sind, werden als *benutzerdefinierte Kataloge* bezeichnet. Fügen Sie benutzerdefinierte Kataloge in der Configuration Manager-Konsole hinzu.  


### <a name="prerequisites"></a>Voraussetzungen 

- [Updates für Drittanbietersoftware](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) einrichten. Phase 1 abschließen: Aktivieren und Einrichten des Features.   

- Ein digital signierter benutzerdefinierter Katalog, der digital signierte Softwareupdates enthält.  

- Der Administrator setzt folgende Berechtigungen voraus:  

    - Standort: Erstellen, Ändern  


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Softwareupdates**, und wählen Sie den Knoten **Katalog mit Updates für Drittanbietersoftware** aus. Klicken Sie im Menüband auf **Benutzerdefinierten Katalog hinzufügen**.  

2. Geben Sie auf der Seite **Allgemein** die folgenden Details an:  

    - **Download URL:** eine gültige HTTPS-Adresse des benutzerdefinierten Katalogs.  

    - **Herausgeber:** der Name der Organisation, die den Katalog veröffentlicht.  

    - **Name:** der Name des Katalogs, der in der Configuration Manager-Konsole angezeigt werden soll.  

    - **Beschreibung:** eine Beschreibung der Warnung.  

    - **Support-URL** (optional): eine gültige HTTPS-Adresse einer Website, auf der Hilfe zum Katalog angeboten wird.  

    - **Supportkontakt** (optional): Kontaktinformationen, über die man Hilfe zum Katalog erhält.  

3. Schließen Sie den Assistenten ab. Der Assistent fügt den neuen Katalog als nicht abonniert hinzu.  

4. Abonnieren Sie den benutzerdefinierten Katalog mithilfe der vorhandenen Aktion **Katalog abonnieren**. Weitere Informationen finden Sie in [Phase 2: Abonnieren von Drittanbieterkatalogen und Synchronisierungsupdates](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Sie können weder Kataloge mit derselben Download-URL hinzufügen noch Katalogeigenschaften bearbeiten. Wenn Sie falsche Eigenschaften für einen benutzerdefinierten Katalog angeben, löschen Sie den Katalog, bevor Sie ihn erneut hinzufügen.  


#### <a name="unsubscribe-from-a-catalog"></a>Kündigen eines Katalogabonnements
Zum Kündigen eines Katalogabonnements wählen Sie den gewünschten Katalog in der Liste aus und klicken im Menüband auf **Katalogabonnement kündigen**. Wenn Sie ein Katalogabonnement kündigen, treten die folgenden Aktionen und Verhalten auf: 
- Der Standort beendet die Synchronisierung neuer Updates. 
- Der Standort blockiert die zugeordneten Zertifikate zum Signieren und Aktualisieren des Inhalts. 
- Vorhandene Updates werden nicht entfernt, aber möglicherweise können Sie sie nicht veröffentlichen oder bereitstellen.

#### <a name="delete-a-custom-catalog"></a>Löschen eines benutzerdefinierten Katalogs
Löschen Sie benutzerdefinierte Kataloge vom selben Knoten der Konsole aus. Wählen Sie einen *nicht abonnierten* benutzerdefinierten Katalog aus, und klicken Sie auf **Benutzerdefinierten Katalog löschen**. Wenn Sie den Katalog bereits abonniert haben, kündigen Sie das Abonnement, bevor Sie ihn löschen. Sie können keine Partnerkataloge löschen. Beim Löschen wird ein benutzerdefinierter Katalog aus der Liste der Kataloge entfernt. Diese Aktion wirkt sich nicht auf Softwareupdates aus, die Sie auf Ihrem Softwareupdatepunkt veröffentlicht haben.


### <a name="known-issue"></a>Bekanntes Problem
Die Löschaktion für benutzerdefinierte Kataloge ist abgeblendet, sodass Sie keine benutzerdefinierten Kataloge von der Konsole aus löschen können. Zur Umgehung dieses Problems verwenden Sie das **wbemtest**-Tool auf dem Standortserver. Fragen Sie die Instanz, die Sie löschen möchten, mit dem Namen oder der Download-URL ab, z.B.: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. Wählen Sie im Abfrageergebnisfenster das Objekt aus, und klicken Sie auf **Löschen**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a> Verbesserungen der Cloudverwaltungsfeatures

Dieses Release umfasst die folgenden Verbesserungen:  

- Die folgenden Features unterstützen jetzt die Verwendung der Azure U.S. Government Cloud:<!--511980-->  

    - Onboarding des Standorts für **Cloudverwaltung** über [Azure-Dienste](../servers/deploy/configure/azure-services-wizard.md)  

    - Bereitstellen eines [Cloudverwaltungsgateways mit Azure Resource Manager](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - Bereitstellen eines [Cloudverteilungspunkts mit Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- Kunden verwenden Windows AutoPilot für die Bereitstellung von Windows 10 auf mit dem lokalen Netzwerk verbundenen Geräten, die in Azure Active Directory eingebunden sind. Zum Installieren oder Aktualisieren des Configuration Manager-Clients auf diesen Geräten benötigen Sie jetzt keinen Cloudverteilungspunkt oder lokalen Verteilungspunkt mehr, der so konfiguriert ist, dass **Clients anonym eine Verbindung herstellen können**. Aktivieren Sie stattdessen die Standortoption zum **Verwenden durch den Configuration Manager generierter Zertifikate für HTTP-Standortsysteme**, die einem in eine Clouddomäne eingebundenen Client die Kommunikation mit einem lokalen HTTP-fähigen Verteilungspunkt ermöglicht. Weitere Informationen zu dieser Einstellung finden Sie unter [Verbesserte sichere Clientkommunikation](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a> Neuer Bericht zur Konformität von Softwareupdates
<!--1357775-->
Das Anzeigen von Berichten zur Konformität von Softwareupdates umfasst normalerweise Daten von Clients, die seit einiger Zeit keinen Kontakt mehr mit dem Standort hatten. In einem neuen Bericht können Sie Konformitätsergebnisse für eine bestimmte Softwareupdategruppe nach „fehlerfreien“Clients filtern. Dieser Bericht zeigt den realistischeren Konformitätsstatus der aktiven Clients in Ihrer Umgebung. 
 
Um den Bericht anzuzeigen, wechseln Sie zum Arbeitsbereich **Überwachung**, erweitern **Berichterstellung**, erweitern **Berichte**, erweitern **Softwareupdates – A-Konformität** und wählen **Konformität 9: Gesamtintegrität und -konformität** aus. Geben Sie **Updategruppe**, **Sammlungsname** und **Clientintegritäts**-Zustand an.

Der Bericht enthält die folgenden Teile:
- **„Fehlerlose Clients“ im Vergleich zu „Gesamtzahl Clients“:** In diesem Balkendiagramm werden die „fehlerlosen“ Clients, die im angegebenen Zeitraum mit dem Standort kommuniziert haben, mit der Gesamtanzahl der Clients in der angegebenen Sammlung verglichen.
- **Konformitätsübersicht:** Dieses Tortendiagramm zeigt den gesamten Konformitätszustand für die jeweilige Softwareupdategruppe auf aktiven Clients in der angegebenen Sammlung an.
- **Wichtigste 5 nicht konforme nach Artikel-ID:** Dieses Balkendiagramm zeigt die fünf wichtigsten Softwareupdates in der angegebenen Gruppe an, die auf aktiven Clients in der angegebenen Sammlung nicht konform sind.
- Der untere Rand des Berichts ist eine Tabelle mit zusätzlichen Informationen, in der die Softwareupdates in der angegebenen Gruppe aufgeführt sind.



## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
