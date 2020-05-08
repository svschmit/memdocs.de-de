---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über neue Features, die mit der Technical Preview-Version 1805 für System Center Configuration Manager zur Verfügung stehen.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d8c1cd6610bd09b2714951d8a755770b6347b2f6
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905231"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Funktionen in der Technical Preview 1805 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1805 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um Funktionen für Ihren Technical Preview-Standort zu aktualisieren oder neue Funktionen hinzuzufügen. 

Lesen Sie den [Technical Preview](technical-preview.md)-Artikel vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Erstellen einer stufenweisen Bereitstellung mit manuell konfigurierten Phasen für eine Tasksequenz
<!--1358148-->
Sie können jetzt [eine stufenweise Bereitstellung](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) mit manuell konfigurierten Phasen für eine Tasksequenz erstellen. Sie können bis zu 10 weitere Phasen aus der Registerkarte **Phasen** des Assistenten für das Erstellen der stufenweisen Bereitstellung hinzufügen. 


### <a name="try-it-out"></a>Probieren Sie es aus!
Folgen Sie den Anweisungen zum Erstellen einer stufenweisen Bereitstellung, in der Sie alle Phasen manuell konfigurieren. Senden Sie uns Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist. 

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

2. Klicken Sie mit der rechten Maustaste auf eine bereits vorhandene Tasksequenz, und klicken Sie auf **Create Phased Deployment** (Bereitstellung in Phasen).  

3. Vergeben Sie auf der Registerkarte **Allgemein** einen Namen für die stufenweise Bereitstellung, fügen Sie (optional) eine Beschreibung hinzu, und wählen Sie **Alle Phasen manuell konfigurieren** aus.  

4. Klicken Sie auf der Registerkarte **Phasen** auf **Hinzufügen**.  

5. Geben Sie einen **Namen** für die Phase an, und navigieren Sie zu dem Ziel **Phasensammlung**.  

6. Wählen Sie in der Registerkarte **Phaseneinstellungen** für jede Einstellung des Zeitplans eine Option aus, und klicken Sie anschließend auf **Weiter**.  

    - Kriterien für den Erfolg der vorherigen Phase (Diese Option ist für die erste Phase deaktiviert.)
        - **Bereitstellungserfolg in Prozent**: Geben Sie den Prozentsatz der Geräte an, für die die Bereitstellung der vorherigen Phase erfolgreich abgeschlossen wurde.  

    - Bedingungen für den Start dieser Bereitstellungsphase nach dem erfolgreichen Abschluss der vorherigen Phase  
        - **Diese Phase nach Verzögerung (in Tagen) automatisch starten**: Legen Sie fest, wie viele Tage nach dem erfolgreichen Abschluss der vorherigen Phase die nächste beginnen soll. 
        - **Diese Phase der Bereitstellung manuell starten**: Diese Phase beginnt nicht automatisch nach dem erfolgreichen Abschluss der vorherigen.  

    - Sobald ein Gerät bestimmt ist, Software installieren
        - **So bald wie möglich**: Hiermit wird festgelegt, dass die Software installiert wird, sobald ein Gerät bestimmt wird.
        - **Fristzeitraum (von der Bestimmung des Geräts abhängig)** : Legt die Frist der Installation auf eine bestimmte Anzahl von Tagen nach der Bestimmung des Geräts fest.  
     
7. Schließen Sie den Assistenten für die Phaseneinstellungen ab.

8. Auf der Registerkarte **Phasen** des Assistenten zum Erstellen der stufenweisen Bereitstellung können Sie die Phasen für diese Bereitstellung jetzt hinzufügen, entfernen, neu anordnen oder bearbeiten.  

9. Schließen Sie den Assistenten zum Erstellen der stufenweisen Bereitstellung ab.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Cloudverteilungspunkt-Unterstützung für Azure Resource Manager
<!--1322209-->
Beim Erstellen einer Instanz des [Cloudverteilungspunkts](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) bietet der Assistent jetzt die Option, eine **Azure Resource Manager-Bereitstellung** zu erstellen. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) ist eine moderne Plattform zum Verwalten aller Lösungsressourcen als eine einzige Entität, die als [Ressourcengruppe](/azure/azure-resource-manager/resource-group-overview#resource-groups) bezeichnet wird. Beim Bereitstellen eines Cloudverteilungspunkts mit Azure Resource Manager verwendet der Standort Azure Active Directory (Azure AD), um die erforderlichen Cloudressourcen zu authentifizieren und zu erstellen. Diese modernisierte Bereitstellung benötigt kein klassisches Azure-Verwaltungszertifikat.  

Der Cloudverteilungspunkt-Assistent bietet weiterhin die Option einer **klassischen Dienstbereitstellung** mit einem Azure-Verwaltungszertifikat. Um die Bereitstellung und Verwaltung von Ressourcen zu vereinfachen, empfiehlt sich die Verwendung des Azure Resource Manager-Bereitstellungsmodells für alle neuen Cloudverteilungspunkte. Stellen Sie nach Möglichkeit vorhandene Cloudverteilungspunkte über Resource Manager erneut bereit.

Configuration Manager migriert keine vorhandenen klassischen Cloudverteilungspunkte zum Azure Resource Manager-Bereitstellungsmodell. Erstellen Sie neue Cloudverteilungspunkte mit Azure Resource Manager-Bereitstellungen, und entfernen Sie dann klassische Cloudverteilungspunkte. 

> [!IMPORTANT]  
> Diese Funktion aktiviert nicht die Unterstützung für Azure-Clouddienstanbieter (Cloud Service Providers, CSPs). Die Cloudverteilungspunkt-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der vom CSP nicht unterstützt wird. Weitere Informationen finden Sie unter [verfügbare Azure-Dienste in Azure-CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Voraussetzungen  
- Integration in [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Die Azure AD-Benutzerermittlung ist nicht erforderlich.  

- Die gleichen [Anforderungen für einen Cloudverteilungspunkt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements), mit Ausnahme des Azure-Verwaltungszertifikats.  


### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und wählen Sie dann **Cloudverteilungspunkte** aus. Klicken Sie im Menüband auf **Cloudverteilungspunkt erstellen**.   

2. Wählen Sie auf der Seite **Allgemein** die Option **Azure Resource Manager-Bereitstellung** aus. Klicken Sie auf **Anmelden**, um sich mit dem Administratorkonto eines Azure-Abonnements zu authentifizieren. Der Assistent füllt die verbleibenden Felder automatisch aus den Azure AD-Abonnementinformationen auf, die im Rahmen der Voraussetzungen für die Integration gespeichert wurden. Wenn Sie mehrere Abonnements besitzen, wählen Sie das Abonnement aus, das Sie verwenden möchten. Klicken Sie auf **Weiter**.  

3. Geben Sie auf der Seite **Einstellungen** wie gewohnt die PKI-**Zertifikatdatei** an. Dieses Zertifikat definiert den von Azure verwendeten Cloudverteilungspunkt **Dienst-FQDN**. Wählen Sie die **Region** und danach eine der Ressourcengruppenoptionen **Neu erstellen** oder **Vorhandene verwenden** aus. Geben Sie den Namen für die neue Ressourcengruppe ein, oder wählen Sie aus der Dropdownliste eine vorhandene Ressourcengruppe aus.  

4. Schließen Sie den Assistenten ab.  

> [!NOTE]  
> Azure weist der ausgewählten Azure AD-Server-App die Abonnementberechtigung **Mitwirkender** zu.  

Überwachen Sie den Fortschritt der Dienstbereitstellung mit **cloudmgr.log** auf dem Dienstverbindungspunkt.



## <a name="take-actions-based-on-management-insights"></a>Ausführen von Aktionen basierend auf Verwaltungseinblicken
<!--1357930-->
Einige [Verwaltungseinblicke](../servers/manage/management-insights.md) können jetzt Aktionen auslösen. Abhängig von der Regel weist diese Aktion eine der folgenden Verhaltensweisen auf:  

- Automatisches Navigieren in der Konsole zu dem Knoten, wo Sie weitere Maßnahmen ergreifen können. Wenn der Verwaltungseinblick z.B. die Änderung einer Clienteinstellung empfiehlt, besteht die Aktion im Navigieren zum Knoten für Clienteinstellungen. Sie können weitere Maßnahmen ergreifen, indem Sie das standardmäßige oder ein benutzerdefiniertes Clienteinstellungenobjekt ändern.  

- Navigieren Sie basierend auf einer Abfrage zu einer gefilterten Ansicht. Die Durchführung von Aktionen, die sich auf die Regel für leere Sammlungen bezieht, zeigt z.B. nur diese Sammlungen in der Liste der Sammlungen an. Hier können Sie eine weitere Aktion wie z.B. das Löschen einer Sammlung oder Ändern ihrer Mitgliedschaftsregeln durchführen.  

Die folgenden Verwaltungseinblickregeln sind in diesem Release mit Aktionen verbunden:
- Sicherheit
    - Nicht unterstützte Antimalware-Clientversionen
- Software Center
    - Verwenden Sie die neue Version von Softwarecenter
- Applications
    - Anwendungen ohne Bereitstellungen
- Vereinfachte Verwaltung
    - Nicht-CB-Clientversionen
- Sammlungen
    - Leere Sammlungen 
- Cloud Services
    - Clients auf die aktuelle Version von Windows 10 aktualisieren



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Übertragen der Gerätekonfigurationsworkload auf Intune mithilfe der Co-Verwaltung
<!--1357903-->

Sie können jetzt die Gerätekonfigurationsworkload von Configuration Manager auf Intune übertragen, nachdem Sie die Co-Verwaltung aktiviert haben. Mit dem Übergang dieser Workload können Sie Intune zum Bereitstellen von MDM-Richtlinien verwenden, während Sie weiterhin Configuration Manager zum Bereitstellen von Anwendungen verwenden. 

Wechseln Sie für den Übergang dieser Workload zur Eigenschaftenseite für die Co-Verwaltung, und bewegen Sie den Schieberegler von „Configuration Manager“ zu **Pilot** oder **Alle**. Weitere Informationen finden Sie unter [Co-Verwaltung für Windows 10-Geräte](../../comanage/overview.md).

> [!Note]  
> Beim Verschieben dieser Workload werden auch die Workloads **Ressourcenzugriff** und **Endpoint Protection** verschoben, die eine Teilmenge der Gerätekonfigurationsworkload sind.

Wenn Sie den Übergang dieser Workload durchführen, können Sie immer noch Einstellungen von Configuration Manager für co-verwaltete Geräte bereitstellen, obwohl Intune die Autorität für die Gerätekonfiguration ist. Diese Ausnahme kann genutzt werden, um Einstellungen zu konfigurieren, die Ihre Organisation benötigt, jedoch noch nicht in Intune verfügbar sind. Geben Sie diese Ausnahme in einer Konfigurationsbaseline für den Configuration Manager an. Aktivieren Sie bei der Erstellung der Baselinie oder auf der Registerkarte **Allgemein** der Eigenschaften einer vorhandenen Baseline die Option **Diese Baseline auch immer für gemeinsam verwaltete Clients anwenden**. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Aktivieren der Verwendung der Netzwerküberlastungssteuerung durch die Verteilungspunkte
<!--1358112-->

Windows Low Extra Delay Background Transport (LEDBAT) ist ein Feature von Windows Server zum Verwalten von Netzwerkübertragungen im Hintergrund. Für Verteilungspunkte, die auf unterstützten Versionen von Windows Server ausgeführt werden, können Sie eine Option zum Anpassen des Netzwerkdatenverkehrs aktivieren. Clients verwenden Netzwerkbandbreite nur, wenn sie verfügbar ist. 


### <a name="prerequisites"></a>Voraussetzungen
- Ein Verteilungspunkt unter Windows Server, Version 1709.  

- Es gibt keine Clientvoraussetzungen.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Wählen Sie den Knoten **Verteilungspunkte** aus. Wählen Sie den Zielverteilungspunkt aus, und klicken Sie im Menüband auf **Eigenschaften**.  

2. Aktivieren Sie auf der Registerkarte **Allgemein** die Option **Downloadgeschwindigkeit zur Verwendung der nicht verwendeten Netzwerkbandbreite anpassen (Windows LEDBAT)** .  



## <a name="cloud-management-dashboard"></a>Dashboard für die Cloudverwaltung
<!--1358461-->
Das neue **Dashboard für die Cloudverwaltung** bietet eine zentrale Ansicht für die Nutzung von Cloud Management Gateway (CMG). Wenn im Standort Azure AD integriert ist, werden auch Daten zu Cloudbenutzern und -geräten angezeigt.  

Der folgende Screenshot zeigt einen Teil des Dashboards für die Cloudverwaltung mit zwei der verfügbaren Kacheln:  
![Kacheln des Dashboards für die Cloudverwaltung mit CMG-Datenverkehr und aktuellen Onlineclients](media/1358461-cmg-dashboard.png)

Diese Funktion umfasst auch die **CMG-Verbindungsanalyse** für die Echtzeitüberprüfung zur Unterstützung der Problembehandlung. Das Hilfsprogramm in der Konsole überprüft den aktuellen Status des Diensts und den Kommunikationskanal über den CMG-Verbindungspunkt zu Verwaltungspunkten, die CMG-Datenverkehr zulassen.


### <a name="prerequisites"></a>Voraussetzungen
- Ein von internetbasierten Clients verwendetes aktives [Cloudverwaltungsgateway](../clients/manage/cmg/plan-cloud-management-gateway.md).  

- Die Integration des Standorts in [Azure-Dienste](../servers/deploy/configure/azure-services-wizard.md) für die Cloudverwaltung.  


### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

#### <a name="cloud-management-dashboard"></a>Dashboard für die Cloudverwaltung

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Wählen Sie den Knoten **Cloudverwaltung** aus, und zeigen Sie die Dashboardkacheln an.  

#### <a name="cmg-connection-analyzer"></a>CMG-Verbindungsanalyse

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Clouddienste**, und wählen Sie **Cloud Management Gateway** aus.  

2. Wählen Sie die CMG-Zielinstanz und dann **Verbindungsanalyse** im Menüband aus.  

3. Wählen Sie im CMG-Verbindungsanalysefenster eine der folgenden Optionen aus, um sich bei dem Dienst zu authentifizieren:  

     1. **Azure AD-Benutzer**: Simulieren Sie mit dieser Option die Kommunikation einer cloudbasierten Benutzeridentität, die bei einem in Azure AD eingebundenen Windows 10-Gerät angemeldet ist. Klicken Sie auf **Anmelden**, um sicher die Anmeldeinformationen für das Azure AD-Benutzerkonto einzugeben.  

     2. **Clientzertifikat**: Simulieren Sie mit dieser Option die Kommunikation eines Configuration Manager-Clients mit einem [Clientauthentifizierungszertifikat](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Klicken Sie auf **Starten**, um die Analyse zu starten. Die Ergebnisse werden im Analysefenster angezeigt. Wählen Sie einen Eintrag aus, um weitere Informationen im Feld „Beschreibung“ anzuzeigen.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager hat immer einen großen zentralen Speicher für Gerätedaten bereitgestellt, die Kunden für Berichtszwecke verwenden. Der Nutzen der Daten hängt jedoch davon ab, wieviel Zeit vergangen ist, seit sie auf den Clients gesammelt wurden. 

CMPivot ist ein neues in der Konsole integriertes Hilfsprogramm, das Echtzeitzugriff auf den Status von Geräten in Ihrer Umgebung in Echtzeit ermöglicht. Es führt sofort eine Abfrage aller derzeit verbundenen Geräte in der Zielsammlung durch und gibt die Ergebnisse zurück. Sie können diese Daten dann im Tool filtern und gruppieren. Mit dem Bereitstellen von Echtzeitdaten von Onlineclients können Sie schneller Geschäftsfragen beantworten, Problembehandlungen durchführen sowie auf Sicherheitsvorfälle reagieren.

Beispielsweise ist eine der Anforderungen der [Abhilfe bei vermutlichen Kanalsicherheitsrisiken auf der Ausführungsseite](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974) die Aktualisierung des System-BIOS. Mit CMPivot können Sie schnell Informationen zum System-BIOS abfragen und Clients suchen, die nicht kompatibel sind. 

In diesem Screenshot zeigt CMPivot zwei separate BIOS-Versionen mit jeweiliger Geräteanzahl an. Sie können diese Beispielabfrage verwenden, wenn Sie CMPivot ausprobieren:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![CMPivot-Fenster mit Beispielabfrage für BIOSVersion](media/1358456-cmpivot-biosversion.png)

Sie können auf die Geräteanzahl klicken, um einen Drilldown zur Anzeige der gewünschten Geräte auszuführen. Zum Anzeigen von Geräten in CMPivot können Sie mit der rechten Maustaste auf ein Gerät klicken und die folgenden [Clientbenachrichtigungsaktionen](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) auswählen:
- Skript ausführen
- Remotesteuerung
- Ressourcen-Explorer

Wenn Sie mit der rechten Maustaste auf ein bestimmtes Gerät klicken, können Sie auch die Ansicht dieses Geräts auf eines der folgenden Attribute pivotieren:
- Autostartbefehle
- Installierte Produkte
- Prozesse
- Dienste
- -Benutzer
- Aktive Verbindungen
- Fehlende Updates

### <a name="prerequisites"></a>Voraussetzungen
- Die Zielclients müssen auf die neueste Version aktualisiert werden.  

- Der Configuration Manager-Administrator benötigt Berechtigungen zum Ausführen von Skripts. Weitere Informationen finden Sie unter [Erstellen von Sicherheitsrollen für Skripts](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie **Gerätesammlungen** aus. Wählen Sie eine Zielsammlung aus, und klicken Sie im Menüband auf **CMPivot starten**, um das Tool zu starten.  

2. Die Benutzeroberfläche bietet weitere Informationen zur Verwendung des Tools. 
     - Sie können oben manuell Abfragezeichenfolgen eingeben oder auf die Links in der Inlinedokumentation klicken.
     - Klicken Sie auf eine der **Entitäten**, um sie der Abfragezeichenfolge hinzuzufügen. 
     - Die Links für **Tabellenoperatoren**, **Aggregationsfunktionen** und **Skalarfunktionen** öffnen die Sprachreferenzdokumentation im Webbrowser. CMPivot verwendet die gleiche Abfragesprache wie [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Verbesserte sichere Clientkommunikation
<!--1356889,1358228,1358460-->
Die HTTPS-Kommunikation wird für alle Configuration Manager-Kommunikationspfade empfohlen, kann jedoch wegen der aufwändigen Verwaltung von PKI-Zertifikaten für einige Kunden schwierig sein. Die Einführung der Integration von Azure Active Directory (Azure AD) reduziert einige der Zertifikatanforderungen, aber nicht alle. 

Dieses Release bietet Verbesserungen der Kommunikation von Clients mit Standortsystemen. Diese Verbesserungen verfolgen zwei Hauptziele:  

- Sie können die Clientkommunikation sichern, ohne dass PKI-Serverauthentifizierungszertifikate notwendig sind.  

- Clients können ohne Netzwerkzugriffskonto sicher von Verteilungspunkten auf Inhalt zugreifen.  

> [!Note]  
> PKI-Zertifikate sind immer noch eine gültige Option für Kunden, die sie verwenden möchten.  


### <a name="scenarios"></a><a name="bkmk_token"></a> Szenarios
Die folgenden Szenarios profitieren von diesen Verbesserungen:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a> Szenario 1: Client zu Verwaltungspunkt
<!--1356889-->
[In Azure AD eingebundene Geräte](/azure/active-directory/devices/concept-azure-ad-join) können über ein Cloud Management Gateway (CMG) mit einem Verwaltungspunkt kommunizieren, der für HTTP konfiguriert ist. Der Standortserver generiert ein Zertifikat für den Verwaltungspunkt, sodass er über einen sicheren Kanal kommunizieren kann.   

> [!Note]  
> Dieses Verhalten ist eine Änderung gegenüber der aktuellen Version 1802 von Configuration Manager, die einen HTTPS-fähigen Verwaltungspunkt für dieses Szenario erfordert. Weitere Informationen finden Sie unter [Verwaltungspunkt für HTTPS aktivieren](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a> Szenario 2: Client zu Verteilungspunkt
<!--1358228-->
Eine Arbeitsgruppe oder ein in Azure AD eingebundener Client kann über einen sicheren Kanal von einem für HTTP konfigurierten Verteilungspunkt Inhalt herunterladen.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a> Szenario 3: Azure AD-Geräteidentität 
<!--1358460-->
Ein in Azure AD eingebundenes oder [hybrides Azure AD-Gerät](/azure/active-directory/devices/concept-azure-ad-join-hybrid) kann sicher mit seinem zugewiesenen Standort kommunizieren, ohne dass ein Azure AD-Benutzer angemeldet ist. Die cloudbasierte Geräteidentität reicht jetzt für die Authentifizierung beim CMG und Verwaltungspunkt aus.  


### <a name="prerequisites"></a>Voraussetzungen  

- Ein Verwaltungspunkt, der für HTTP-Clientverbindungen konfiguriert ist. Legen Sie diese Option auf der Registerkarte **Allgemein** der Rolleneigenschaften des Standortsystems fest.  

- Ein für HTTP-Clientverbindungen konfigurierter Verteilungspunkt. Legen Sie diese Option auf der Registerkarte **Allgemein** der Rolleneigenschaften des Standortsystems fest. Aktivieren Sie nicht die Option **Anonyme Verbindung von Clients zulassen**.  

- Ein Cloudverwaltungsgateway.  

- Integrieren Sie den Standort zur Cloudverwaltung in Azure AD.  

    - Wenn diese Voraussetzung für Ihren Standort bereits erfüllt ist, müssen Sie die Azure AD-Anwendung aktualisieren. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Clouddienste**, und wählen Sie **Azure Active Directory-Mandanten** aus. Wählen Sie den Azure AD-Mandanten aus, die Webanwendung im Bereich **Anwendungen**, und klicken Sie dann im Menüband auf **Anwendungseinstellungen aktualisieren**.  

- Ein in Azure AD eingebundener Client, auf dem Windows 10, Version 1803 ausgeführt wird. (Diese Anforderung gilt nur für [Szenario 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Wählen Sie den Standort aus, und klicken Sie im Menüband auf **Eigenschaften**.  

2. Wechseln Sie zur Registerkarte **Clientcomputerkommunikation**. Wählen Sie die Option für **HTTPS oder HTTP** aus, und aktivieren Sie die neue Option zum **Verwenden von vom Configuration Manager generierten Zertifikaten für HTTP-Standortsysteme**.  

Nutzen Sie die obige [Liste von Szenarios](#bkmk_token) zum Überprüfen.

> [!Tip]
> In diesem Release müssen Sie bis zu 30 Minuten warten, bis der Verwaltungspunkt das neue Zertifikat vom Standort empfängt und konfiguriert.

Sie können diese Zertifikate in der Configuration Manager-Konsole anzeigen. Wechseln Sie zum Arbeitsbereich **Verwaltung**, erweitern Sie **Sicherheit**, und wählen Sie den **Zertifikate**-Knoten aus. Suchen Sie nach dem **SMS-Ausgabe**-Stammzertifikat sowie den vom „SMS-Ausgabe“-Stamm ausgegebenen Standortserverrollen-Zertifikaten.


### <a name="known-issues"></a>Bekannte Probleme
- Der Benutzer kann im Softwarecenter keine für ihn verfügbaren Anwendungen anzeigen.  

- Betriebssystembereitstellungs-Szenarios benötigen weiterhin das Netzwerkzugriffskonto.  

- Schnelles und wiederholtes Aktivieren und Deaktivieren der Option zum **Verwenden von vom Configuration Manager generierten Zertifikaten für HTTP-Standortsysteme** kann dazu führen, dass das Zertifikat nicht ordnungsgemäß an die Standortsystemrollen gebunden wird. Kein vom „SMS-Ausgabe“-Zertifikat ausgestelltes Zertifikat ist an eine Website in Windows Server Internet Information Services (IIS) gebunden. Um dieses Problem zu umgehen, löschen Sie alle vom „SMS-Ausgabe“-Zertifikat ausgestellten Zertifikate aus dem **SMS**-Zertifikatspeicher in Windows, und starten Sie dann den smsexec-Dienst neu.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Verbesserungen, um die Unterstützung von Drittanbietersoftware-Updates zu ermöglichen
<!--1357605-->
Aufgrund Ihres UserVoice-Feedbacks zur [Unterstützung von Drittanbietersoftware-Updates](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) war die Integration in System Center Updates Publisher (SCUP) in diesem Release wieder ein Thema. Ab Configuration Manager Technical Preview [Version 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) bestand die Möglichkeit, das Zertifikat von WSUS für Drittanbieterupdates zu lesen und dann das Zertifikat für Clients bereitzustellen. Doch Sie mussten das Zertifikat zum Signieren von Drittanbietersoftware-Updates immer noch mit dem SCUP-Tool erstellen und verwalten.

In diesem Release können Sie dem Configuration Manager-Standort ermöglichen, das Zertifikat automatisch zu konfigurieren. Der Standort kommuniziert zu diesem Zweck mit WSUS, um ein Zertifikat zu generieren. Configuration Manager fährt dann damit fort, das Zertifikat für Clients bereitzustellen. Dank dieser Verbesserung muss das SCUP-Tool nicht mehr zum Erstellen und Verwalten des Zertifikats verwendet werden. 

Weitere Informationen zur allgemeinen Verwendung des SCUP-Tools finden Sie unter [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Voraussetzungen
- Aktivieren und Bereitstellen der Clienteinstellung **Softwareupdates von Drittanbietern aktivieren** in der Gruppe **Softwareupdates**.
- Wenn WSUS sich auf einem anderen Server als der Softwareupdatepunkt befindet, müssen Sie eine der folgenden Optionen auf dem WSUS-Remoteserver ausführen:
    - Aktivieren des Remoteregistrierungsdiensts in Windows  
    oder
    - Erstellen Sie im Registrierungsschlüssel `HKLM\Software\Microsoft\Update Services\Server\Setup` ein neues DWORD mit dem Namen **EnableSelfSignedCertificates** und dem Wert `1`. 

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Wählen Sie den Standort der obersten Ebene aus, klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.  

2. Wechseln Sie zu der Registerkarte **Drittanbieterupdates**. Wählen Sie die Option **Softwareupdates von Drittanbietern aktivieren** und dann die Option für **Configuration Manager verwaltet das Zertifikat automatisch** aus.

3. Fahren mit dem Rest des typischen SCUP-Workflows zum Importieren eines Drittanbietersoftware-Update-Katalogs fort, und stellen Sie dann die Updates für Clients bereit.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Verbesserungen an der Tasksequenz für direktes Windows 10-Upgrade
<!--1358500-->

Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält jetzt eine zusätzliche neue Gruppe mit empfohlenen Aktionen, die zusätzlich durchgeführt werden, falls bei dem Upgradevorgang ein Fehler auftritt. Diese Aktionen erleichtern die Problembehandlung.

### <a name="new-groups-under-run-actions-on-failure"></a>Neue Gruppen unter **Bei Auftreten eines Fehlers auszuführende Aktionen**
- **Protokolle sammeln**: Um Protokolle auf dem Client zu sammeln, fügen Sie in dieser Gruppe Schritte hinzu. 
    - Üblicherweise werden die Protokolldateien in eine Netzwerkfreigabe kopiert. Um diese Verbindung herzustellen, führen Sie den Schritt [Verbindung mit Netzwerkordner herstellen](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) aus. 
    - Um den Kopiervorgang auszuführen, verwenden Sie ein benutzerdefiniertes Skript oder ein Hilfsprogramm zusammen mit dem Schritt [Befehlszeile ausführen](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) oder [PowerShell-Skript ausführen](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).
    - Zu den zu sammelnden Dateien könnten folgende Protokolle zählen:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Weitere Informationen zu „setupact.log“ und anderen Windows Setup-Protokollen finden Sie unter [Protokolldateien](/windows/deployment/upgrade/log-files).
    - Weitere Informationen zu Configuration Manager-Clientprotokollen finden Sie unter [Configuration Manager-Clientprotokolle](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
    - Weitere Informationen zu _SMSTSLogPath und anderen nützlichen Variablen finden Sie unter [Integrierte Tasksequenzvariablen](../../osd/understand/task-sequence-variables.md).

- **Ausführen von Diagnosetools**: Fügen Sie zum Ausführen zusätzlicher Diagnosetools Schritte in dieser Gruppe hinzu. Diese Tools sollten automatisiert werden, um so bald wie möglich nach Auftreten eines Fehlers zusätzliche Informationen aus dem System zu sammeln.
    - Ein solches Tool ist Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Mit diesem eigenständigen Diagnosetool können Sie Details zur Ursache des erfolglosen Versuchs eines Windows 10-Upgrades abrufen.
         - Im Configuration Manager [erstellen Sie ein Paket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) für das Tool.
         - Fügen Sie dieser Gruppe Ihrer Tasksequenz den Schritt [Befehlszeile ausführen](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) hinzu. Verweisen Sie mit der Option **Paket** auf das Tool. Die folgende Zeichenfolge ist das Beispiel einer **Befehlszeile**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace mit Client installiert
<!--1357971-->

Das CMTrace-Protokollanzeigetool wird jetzt automatisch mit dem Configuration Manager-Client installiert. Es wird dem Clientinstallationsverzeichnis (standardmäßig `%WinDir%\ccm\cmtrace.exe`) hinzugefügt.

> [!Note]  
> Windows legt *nicht* automatisch fest, dass CMTrace Dateien mit der Erweiterung LOG öffnet.



## <a name="improvement-to-the-configuration-manager-console"></a>Verbesserungen der Configuration Manager-Konsole
<!--1358202-->
Folgende Verbesserungen wurden an der Configuration Manager-Konsole vorgenommen:

- Die Gerätelisten unter „Bestand und Kompatibilität“ > „Geräte“ zeigen jetzt standardmäßig den derzeit angemeldeten Benutzer an. Dieser Wert ist so aktuell wie die [Clientstatus](../clients/manage/monitor-clients.md#bkmk_indStatus). Der Wert wird gelöscht, wenn der Benutzer sich abmeldet. Wenn kein Benutzer angemeldet ist, ist der Wert leer. 

### <a name="known-issues"></a>Bekannte Probleme
Der Wert für den derzeit angemeldeten Benutzer im Knoten „Geräte“ oder beim Anzeigen einer Geräteliste unter dem Knoten „Gerätesammlungen“ ist leer. Um dieses Problem zu umgehen, laden Sie dieses [SQL-Skript](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c) herunter. Führen Sie „sp_BgbUpdateLiveData.sql“ auf dem Standortdatenbankserver aus, und starten Sie dann die Dienste „smsexec“ und „sms_notification_server“ auf dem Verwaltungspunkt neu.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Verbesserungen des Konsolenfeedbacks
<!--1357542-->
Dieses Release umfasst folgende Verbesserungen des neuen [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback)-Mechanismus der Configuration Manager-Konsole:  

- Das Feedback-Dialogfeld speichert nun Ihre vorherigen Einstellungen, z.B. die ausgewählten Optionen und Ihre E-Mail-Adresse.  

- Es unterstützt jetzt Offlinefeedback. Speichern Sie Ihr Feedback über die Konsole, und laden Sie es dann über ein System mit Internetzugang an Microsoft hoch. Verwenden Sie das neue Tool zum Hochladen des Offlinefeedbacks in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Um die verfügbaren und erforderlichen Befehlszeilenoptionen anzuzeigen, führen Sie das Tool mit der `--help`-Option aus. Das verbundene System benötigt Zugriff auf **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Bekannte Probleme
Bei der Verwendung von **Lächeln senden** oder **Stirnrunzeln senden** über die Konsole auf einem Computer mit Internetverbindung kann die folgende Meldung zurückgegeben werden: „Fehler beim Senden von Feedback“. Wenn Sie auf **Weitere Details** klicken, wird der folgende Text angezeigt: `{"Message":""}`. Dieser Fehler wird durch ein bekanntes Problem mit der Antwort aus dem Back-End-Feedbacksystem verursacht. Sie können die Fehlermeldung ignorieren. Microsoft hat Ihr Feedback trotzdem erhalten. (Wenn in den Details eine andere Meldung angezeigt wird, verwenden Sie die Option für Offlinefeedback, oder senden Sie Ihr Feedback zu einem späteren Zeitpunkt erneut.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Verbesserungen an PXE-fähigen Verteilungspunkten
<!--1357580-->

Dieses Release enthält die folgenden zusätzlichen Verbesserungen bei der Verwendung der Option [**PXE-Responder ohne Windows-Bereitstellungsdienst aktivieren**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) auf einem Verteilungspunkt:  

- Windows-Firewall-Regeln werden automatisch auf dem Verteilungspunkt erstellt, wenn Sie diese Option aktivieren.  
- Verbesserungen bei der Komponentenprotokollierung



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Verbesserung der Hardwareinventur für große ganzzahlige Werte
<!--1357880-->
Für die Hardwareinventur gilt derzeit für ganze Zahlen der Höchstwert 4.294.967.296 (2^32). Attribute wie z.B. die Festplattengröße in Bytes können diesen Grenzwert erreichen. Da der Verwaltungspunkt keine höheren Ganzzahlwerte verarbeitet, werden diese Werte nicht in der Datenbank gespeichert. Ab diesem Release beträgt der Höchstwert 18.446.744.073.709.551.616 (2^64). 

Für eine Eigenschaft mit einem Wert, der sich nicht ändert, wie die gesamte Festplattengröße, wird nach dem Upgrade des Standorts möglicherweise nicht sofort der Wert angezeigt. Die Hardwareinventur ist meistens ein Deltabericht. Der Client sendet nur die Werte, die sich ändern. Um dieses Verhalten zu umgehen, fügen Sie derselben Klasse eine andere Eigenschaft hinzu. Diese Aktion bewirkt, dass der Client alle Eigenschaften in der Klasse aktualisiert, die sich geändert haben. 



## <a name="improvement-to-wsus-maintenance"></a>Verbesserung der WSUS-Wartung
<!--1357898-->

Der WSUS-Bereinigungs-Assistent lehnt jetzt Updates ab, die gemäß den Ablösungsregeln abgelaufen oder abgelöst sind. Diese Regeln sind in den Eigenschaften der Softwareupdatepunkt-Komponente definiert.

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Wählen Sie den Standort der obersten Ebene aus, klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.  

2. Wechseln Sie zu der Registerkarte **Ablösungsregeln**. Aktivieren Sie die Option zum **Ausführen des WSUS-Bereinigungs-Assistenten**. Geben Sie das gewünschte Ablösungsverhalten an.  

3. Überprüfen Sie die Datei „WSyncMgr.log“.



## <a name="improvement-to-support-for-cng-certificates"></a>Verbesserte Unterstützung für CNG-Zertifikate
<!--1357314-->
Ab diesem Release können Sie [CNG-Zertifikate](../plan-design/network/cng-certificates-overview.md) für die folgenden HTTPS-fähigen Serverrollen verwenden:  
- Zertifikatregistrierungspunkt einschließlich des NDES-Servers mit dem Configuration Manager-Richtlinienmodul.



## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
