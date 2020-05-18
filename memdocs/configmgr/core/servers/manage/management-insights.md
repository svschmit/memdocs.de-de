---
title: Einblicke für die Verwaltung
titleSuffix: Configuration Manager
description: Informationen zur Funktionalität für Verwaltungseinblicke, die in der Configuration Manager-Konsole verfügbar ist.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69b2533dd5c86124a6aff9feac7306ecf16c6e5a
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268962"
---
# <a name="management-insights-in-configuration-manager"></a>Verwaltungseinblicke in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwaltungseinblicke von Configuration Manager stellen Informationen über den aktuellen Zustand Ihrer Umgebung bereit. Die Informationen basieren auf der Analyse von Daten aus der Standortdatenbank. Diese Einblicke vermitteln Ihnen ein genaueres Verständnis Ihrer Umgebung, sodass Sie entsprechende Maßnahmen ergreifen können. <!--1353967-->

## <a name="review-management-insights"></a>Aufrufen der Einblicke für die Verwaltung

Ihr Konto muss über die **Leseberechtigung** für das **Standortobjekt** verfügen, damit Sie die Regeln anzeigen können.

1. Öffnen Sie die Configuration Manager-Konsole.  

2. Navigieren Sie zum Arbeitsbereich **Verwaltung**, erweitern Sie **Management Insights**, und klicken Sie dann auf **Alle Erkenntnisse**.  

    > [!Note]  
    > Wenn Sie den Knoten **Management Insights** auswählen, wird das [Management Insights-Dashboard](#bkmk_insights) angezeigt.  

3. Öffnen Sie die Management Insights-Gruppe, die Sie überprüfen möchten. Klicken Sie im Menüband auf **Erkenntnisse anzeigen**.  

Sie können die folgenden vier Registerkarten überprüfen:

- **Alle Regeln**: Bietet eine vollständige Liste der Regeln für die ausgewählte Gruppe von Verwaltungserkenntnissen.  

- **Abgeschlossen**:  Listet die Regeln auf, die keine Aktion erfordern.  

- **In Bearbeitung:** Zeigt Regeln an, für die einige, aber nicht alle Voraussetzungen erfüllt sind.  

- **Aktion erforderlich**: Führt die Regeln auf, die Aktionen erfordern. Klicken Sie auf **Weitere Details**, um die Elemente abzurufen, für die eine Aktion erforderlich ist.  

Der Bereich **Voraussetzungen** enthält die zum Ausführen der Regel erforderlichen Elemente.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Alle Regeln und Voraussetzungen für die Clouddienstgruppe

![Verwaltungseinblicke: Alle Regeln und Voraussetzungen für die Clouddienstgruppe](./media/Management-insights-all-cloud-rules.png)

Wählen Sie eine Regel aus, und klicken Sie dann auf **Weitere Details**, um die Regeldetails anzuzeigen.

## <a name="operations"></a>Vorgänge

Die Anwendbarkeit der Regeln für Verwaltungseinblicke werden wöchentlich neu ausgewertet. Klicken Sie mit der rechten Maustaste auf eine Regel, und wählen Sie **Neu auswerten** aus, um eine Regel bei Bedarf erneut auszuwerten.

Die Protokolldatei für Regeln für Verwaltungseinblicke ist **SMS_DataEngine.log** auf dem Standortserver.

<!--1357930-->
Für manche Regeln können Sie Maßnahmen ergreifen. Wählen Sie eine Regel aus, klicken Sie auf **Weitere Details**, und klicken Sie dann, wenn möglich, auf **Aktion ausführen**.

Abhängig von der Regel weist diese Aktion eine der folgenden Verhaltensweisen auf:  

- Automatisches Navigieren in der Konsole zu dem Knoten, wo Sie weitere Maßnahmen ergreifen können. Wenn der Verwaltungseinblick z.B. die Änderung einer Clienteinstellung empfiehlt, besteht die Aktion im Navigieren zum Knoten für Clienteinstellungen. Sie können dann weitere Maßnahmen ergreifen, indem Sie das standardmäßige oder ein benutzerdefiniertes Clienteinstellungsobjekt ändern.  

- Navigieren Sie basierend auf einer Abfrage zu einer gefilterten Ansicht. Die Durchführung von Aktionen, die sich auf die Regel für leere Sammlungen bezieht, zeigt z.B. nur diese Sammlungen in der Liste der Sammlungen an. Anschließend können Sie eine weitere Aktion durchführen, z.B. das Löschen einer Sammlung oder Ändern ihrer Mitgliedschaftsregeln.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Dashboard für Einblicke in die Verwaltung

<!--1357979-->

Der Knoten **Management Insights** enthält ein grafisches Dashboard. Dieses Dashboard zeigt nun eine Übersicht der Zustände von Regeln an, wodurch das Anzeigen des Fortschritts vereinfacht wird.

Verwenden Sie die folgenden Filter am oberen Rand des Dashboards, um die Ansicht zu optimieren:

- Abgeschlossene anzeigen
- Optional
- Empfohlen
- Kritisch

Das Dashboard umfasst die folgenden Kacheln:  

- **Management Insights-Index:** Verfolgt den Gesamtfortschritt von Management Insights-Regeln. Der Index beschreibt einen gewichteten Durchschnitt. Kritische Regeln weisen den höchsten Wert auf. Optionale Regeln weisen für diesen Index die geringste Gewichtung auf.  

- **Management Insights-Gruppen:** Zeigt unter Berücksichtigung der Filter Prozentwerte für die Regeln in jeder Gruppe an. Wählen Sie eine Gruppe aus, um einen Drilldown zu den spezifischen Regeln in dieser Gruppe auszuführen.  

- **Management Insights-Priorität:** Zeigt unter Berücksichtigung der Filter Prozentwerte für die Regeln nach Priorität an.  

- **Alle Erkenntnisse:** Eine Tabelle der Einblicke, einschließlich der Priorität und des Zustands. Verwenden Sie das Feld **Filter** am oberen Rand der Tabelle, um in den verfügbaren Spalten nach Zeichenfolgen zu filtern. Das Dashboard sortiert die Tabelle in der folgenden Reihenfolge:

  - Status: Aktion erforderlich, Abgeschlossen, Unbekannt  
  - Priorität: Kritisch, Empfohlen, Optional  
  - Zuletzt geändert: Ältere Datumsangaben zuerst  

![Screenshot vom Dashboard für die Einblicke in die Verwaltung](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Gruppen und Regeln

Regeln werden in folgende Management Insight-Gruppen sortiert:

- [Anwendungen](#applications)
- [Clouddienste](#cloud-services)
- [Sammlungen](#collections)
- [Configuration Manager-Bewertung](#configuration-manager-assessment)
- [Proaktive Wartung](#proactive-maintenance)
- [Sicherheit](#security)
- [Vereinfachte Verwaltung](#simplified-management)
- [Softwarecenter](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Applications

Einblicke für Ihre Anwendungsverwaltung

- **Anwendungen ohne Bereitstellungen:** Listet diejenigen Anwendungen in Ihrer Umgebung auf, für die keine aktiven Bereitstellungen vorliegen. Mit dieser Regel können Sie nicht verwendete Anwendungen finden und löschen, um die in der Konsole angezeigte Anwendungsliste zu vereinfachen. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../../apps/deploy-use/deploy-applications.md).  

### <a name="cloud-services"></a>Clouddienste

Dadurch werden Sie bei der Integration mit vielen Clouddiensten unterstützt, die die moderne Verwaltung Ihrer Geräte ermöglichen.

- **Bereitschaft für Co-Verwaltung bewerten**: Mit dieser Regel können Sie nachvollziehen, welche Schritte zum Aktivieren der Co-Verwaltung erforderlich sind. Für diese Regel gibt es Voraussetzungen. Weitere Informationen finden Sie unter [Übersicht über die Co-Verwaltung](../../../comanage/overview.md).  

- **Devices not uploaded to Azure AD** (Nicht in Azure AD hochgeladene Geräte): Ab Version 2002 listet diese Regel Geräte auf, die nicht in Azure AD hochgeladen wurden, weil der Standort nicht ordnungsgemäß für HTTPS konfiguriert ist.<!--6268489--> Konfigurieren Sie [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md) (Erweitertes HTTP), oder aktivieren Sie mindestens einen Verwaltungspunkt für HTTPS. Wenn Sie den Standort bereits für die HTTPS-Kommunikation konfiguriert haben, wird diese Regel nicht angezeigt.

- **Azure-Dienste für die Verwendung mit Configuration Manager konfigurieren**: Mit dieser Regel können Sie Configuration Manager in Azure AD integrieren, wodurch Clients sich beim Standort mit Azure AD authentifizieren können. Weitere Informationen finden Sie unter [Konfigurieren von Azure-Diensten](../deploy/configure/azure-services-wizard.md).  

- **Geräte für Hybrid-Azure AD-Einbindung aktivieren**: In Azure AD eingebundene Geräte ermöglichen es Benutzern, sich mit ihren Domänenanmeldeinformationen anzumelden, und stellen gleichzeitig sicher, dass die Geräte die Sicherheits- und Konformitätsstandards der Organisation erfüllen. Weitere Informationen finden Sie unter [Überlegungen zum Entwurf der Azure Active Directory-Hybrid-Identität](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Sites that don't have proper HTTPS configuration** (Standorte ohne richtige HTTPS-Konfiguration): Ab Version 2002 listet diese Regel Standorte in Ihrer Hierarchie auf, die nicht ordnungsgemäß für HTTPS konfiguriert sind. Diese Konfiguration verhindert, dass der Standort [Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen (Azure AD) synchronisiert](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Sie führt möglicherweise dazu, dass Azure AD Sync nicht alle Geräte hochlädt. Die Verwaltung dieser Clients funktioniert möglicherweise nicht richtig.<!--6268489--> Konfigurieren Sie [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md) (Erweitertes HTTP), oder aktivieren Sie mindestens einen Verwaltungspunkt für HTTPS. Wenn Sie den Standort bereits für die HTTPS-Kommunikation konfiguriert haben, wird diese Regel nicht angezeigt.

- **Clients auf die aktuelle Version von Windows 10 aktualisieren**: Windows 10, Version 1709 oder höher, verbessert und modernisiert die Benutzerfreundlichkeit für Ihre Benutzer. Weitere Informationen finden Sie unter [Wichtige Artikel zur Übernahme von Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Sammlungen

Einblicke, die die Verwaltung vereinfachen, indem sie Sammlungen bereinigen und neu konfigurieren.

- **Leere Sammlungen**: Führt die Sammlungen in Ihrer Umgebung auf, die keine Elemente enthalten. Weitere Informationen finden Sie unter [Verwalten von Sammlungen](../../clients/manage/collections/manage-collections.md).  

Ab Version 1902 gibt es neue Regeln mit Empfehlungen für die Verwaltung von Sammlungen.<!--3555752--> Nutzen Sie die daraus gewonnenen Erkenntnisse, um die Verwaltung zu vereinfachen und die Leistung zu verbessern:

- **Collections with no query rules and no direct members** (Sammlungen ohne Abfrageregeln und ohne direkte Mitglieder): Sie können die Liste der Sammlungen in Ihrer Hierarchie vereinfachen, indem Sie diese Sammlungen löschen.  

- **Collections with the same re-evaluation start time** (Sammlungen mit der gleichen Startzeit für eine Neuauswertung): Diese Sammlungen weisen den gleichen Neuauswertungszeitpunkt wie andere Sammlungen auf. Ändern Sie den Neuauswertungszeitpunkt, um Konflikte zu vermeiden.  

- **Collections with query time over 5 minutes** (Sammlungen mit einer Abfragedauer von mehr als 5 Minuten): Überprüfen Sie die Abfrageregeln für diese Sammlung. Ziehen Sie eine Änderung oder das Löschen der Sammlung in Betracht.

- Die folgenden Regeln schließen Konfigurationen ein, die unnötige Lasten an dem Standort verursachen können. Überprüfen Sie diese Sammlungen, und löschen Sie diese entweder anschließend, oder deaktivieren Sie die Regelauswertung:  

  - **Collections with no query rules and incremental updates enabled** (Sammlungen ohne Abfrageregeln und mit aktivierten inkrementellen Updates)  

  - **Collections with no query rules and enabled for any schedule** (Sammlungen ohne Abfrageregeln und aktiviert für jeden Plan)  

  - **Collections with no query rules and schedule full evaluation selected** (Sammlungen ohne Abfrageregeln und aktiviertem Zeitplan für eine vollständige Auswertung)  

### <a name="configuration-manager-assessment"></a>Configuration Manager-Bewertung

<!--3607758-->

Ab Version 2002 wird diese Gruppe von Microsoft Premier Field Engineering bereitgestellt. Diese Regeln sind eine Stichprobe aus einer ganzen Reihe von Überprüfungen, die von Microsoft Premier im [Diensthub](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments) bereitgestellt werden.

- **Active Directory-Sicherheitsgruppenermittlung für eine zu häufige Ausführung konfiguriert:** Sie müssen normalerweise nicht konfigurieren, dass die Active Directory-Sicherheitsgruppenermittlung öfter als alle drei Stunden ausgeführt wird. Eine häufigere Konfiguration kann zu Leistungseinbußen bei Active Directory, dem Netzwerk und Configuration Manager führen. Aktivieren Sie die inkrementelle Installation anstatt einen vollständigen Synchronisierungszeitplan zu verwenden. Weitere Informationen finden Sie unter [Active Directory-Gruppenermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).

- **Active Directory-Systemermittlung für eine zu häufige Ausführung konfiguriert:** Sie müssen normalerweise nicht konfigurieren, dass die Active Directory-Systemermittlung öfter als alle drei Stunden ausgeführt wird. Eine häufigere Konfiguration kann zu Leistungseinbußen bei Active Directory, dem Netzwerk und Configuration Manager führen. Aktivieren Sie die inkrementelle Installation anstatt einen vollständigen Synchronisierungszeitplan zu verwenden. Weitere Informationen finden Sie unter [Active Directory-Systemermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).

- **Active Directory-Benutzerermittlung für eine zu häufige Ausführung konfiguriert:** Sie müssen normalerweise nicht konfigurieren, dass die Active Directory-Benutzerermittlung öfter als alle drei Stunden ausgeführt wird. Eine häufigere Konfiguration kann zu Leistungseinbußen bei Active Directory, dem Netzwerk und Configuration Manager führen. Aktivieren Sie die inkrementelle Installation anstatt einen vollständigen Synchronisierungszeitplan zu verwenden. Weitere Informationen finden Sie unter [Active Directory-Benutzerermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

- **Auf "Alle Systeme" oder "Alle Benutzer" beschränkte Sammlungen:** Überprüfen Sie alle Sammlungen, die die Sammlungen **Alle Systeme** oder **Alle Benutzer** als begrenzende Sammlung verwenden. Configuration Manager aktualisiert die Mitgliedschaft dieser Standardsammlungen mit Daten aus den Active Directory-Ermittlungsmethoden. Diese Daten sind möglicherweise keine gültigen Informationen für Configuration Manager-Clients.

- **Frequenzermittlung ist deaktiviert:** Die Frequenzermittelung erfordert die Installation des Configuration Manager-Clients auf Geräten. Dies stellt die einzige Ermittlungsmethode dar, die von Clients gestartet wird. Alle anderen Methoden kommen auf Standortservern vor. Die Frequenzermittlung ist wichtig, damit der Clientaktivitätstatus aktuell bleibt. Sie stellt sicher, dass für den Standort nicht versehentlich die Ressourcendatensätze aus der Standortdatenbank veralten. Weitere Informationen finden Sie unter [Frequenzermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).

- **Sammlungsabfragen mit langer Ausführungszeit für inkrementelle Updates aktiviert:** Sammlungen, deren letzte inkrementelle Aktualisierung mehr als 30 Sekunden zurückliegt, verwenden Standortserver- und Datenbankressourcen, die potenziell die Gesamtleistung von Configuration Manager beeinträchtigen könnten. Weitere Informationen finden Sie unter [Bewährte Methoden für Sammlungen](../../clients/manage/collections/best-practices-for-collections.md).

- **Anzahl von Anwendungen und Paketen auf Verteilungspunkten verringern:** Microsoft unterstützt offiziell eine Gesamtgröße von bis zu 10.000 Paketen und Anwendungen auf einem Verteilungspunkt. Eine Überschreitung dieser Gesamtgröße kann zu Funktionsproblemen führen. Weitere Informationen finden Sie unter [Anpassen und Skalieren von Zahlen: Verteilungspunkt](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **Problem mit Installation am sekundären Standort:** Der Installationsstatus einiger sekundärer Standort ist **ausstehend** oder **fehlerhaft**. Diese Status bedeuten, dass Sie die Installation zwar gestartet haben, diese jedoch nicht erfolgreich abgeschlossen wurde. Bis zur abgeschlossenen Installation des sekundären Standorts können Clients nicht ordnungsgemäß mit dem primären Standort kommunizieren. Überprüfung Sie den Arbeitsbereich **Überwachung**, und wiederholen Sie die Installation. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](install-in-console-updates.md#bkmk_retry).

- **Alle Standorte auf dieselbe Version aktualisieren:** Verwenden Sie in einer Hierarchie dieselbe Version von Configuration Manager. Durch diese Konfiguration wird sichergestellt, dass alle Standorte über die gleiche Funktionalität verfügen. Standorte mit unterschiedlichen Versionen in derselben Hierarchie führen zu Interoperabilitätsszenarios. Spätere Versionen von Configuration Manager enthalten neue Features und können bekannte Probleme lösen. Weitere Informationen finden Sie unter [Interoperabilität zwischen verschiedenen Versionen](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Weitere Informationen zu diesen Regeln finden Sie unter [Schritte zur Bereinigung für Einblicke für die Configuration Manager-Verwaltung](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Wenn Sie bereits Kunde von Microsoft Unified oder Microsoft Premier sind, melden Sie sich am [Diensthub](https://serviceshub.microsoft.com/assessments/) für weitere bedarfsgesteuerte Bewertungen an.
>
> Weitere Informationen zu Microsoft-Diensten finden Sie in den [Unterstützungslösungen](https://www.microsoft.com/enterprise/services/support).

### <a name="proactive-maintenance"></a>Proaktive Wartung

<!--1352184-->
Die Regeln in dieser Gruppe markieren potenzielle Konfigurationsprobleme, die Sie durch die Wartung von Configuration Manager-Objekten vermeiden können.

- **Begrenzungsgruppen ohne zugewiesene Standortsysteme**: Ohne zugewiesene Standortsysteme können Begrenzungsgruppen nur zur Standortzuweisung verwendet werden. Weitere Informationen finden Sie unter [Configure boundary groups](../deploy/configure/boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).  

- **Begrenzungsgruppen ohne Mitglieder**: Begrenzungsgruppen sind nicht für Standortzuweisung oder Inhaltssuche anwendbar, wenn sie keine Mitglieder enthalten. Weitere Informationen finden Sie unter [Configure boundary groups](../deploy/configure/boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).  

- **Verteilungspunkte, die keinen Inhalt für Clients bereitstellen**: Verteilungspunkte, die in den letzten 30 Tagen keine Inhalte für Clients zur Verfügung gestellt haben. Diese Daten basieren auf Berichten von Clients zu ihrem Downloadverlauf. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../deploy/configure/install-and-configure-distribution-points.md).  

- **WSUS-Bereinigung aktivieren**: Stellt sicher, dass Sie die Option zum Ausführen der WSUS-Bereinigung für die Eigenschaften der Softwareupdatepunkt-Komponente aktiviert haben. Diese Option verbessert die WSUS-Leistung. Weitere Informationen finden Sie unter [Wartung für Softwareupdates](../../../sum/deploy-use/software-updates-maintenance.md).  

- **Nicht verwendete Startimages**: Startimages, auf die nicht für die Verwendung für PXE-Start oder Tasksequenz verwiesen wird. Weitere Informationen finden Sie unter [Verwalten von Startimages](../../../osd/get-started/manage-boot-images.md).  

- **Nicht verwendete Konfigurationselemente**: Konfigurationselemente, die nicht Teil einer Konfigurationsbaseline und älter als 30 Tage sind. Weitere Informationen finden Sie unter [Erstellen von Konfigurationsbaselines](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Peercachequellen auf die neueste Version des Configuration Manager-Clients aktualisieren**: Identifizieren Sie Clients, die als Peercachequelle dienen, aber nicht von einer Clientversion vor 1806 aktualisiert wurden. Clients vor Version 1806 können nicht als Peercachequelle für Clients verwendet werden, die Version 1806 oder höher ausführen. Wählen Sie **Aktion ausführen** aus, um eine Geräteansicht zu öffnen, die die Clientliste anzeigt.<!--1358008-->  

### <a name="security"></a>Sicherheit

Einblicke zur Verbesserung der Sicherheit Ihrer Infrastruktur und Geräte.

- **NTLM-Fallback ist aktiviert**:<!--4572953--> Ab Version 1906 erkennt diese Regel, ob Sie die weniger sichere NTLM-Authentifizierungs-Fallbackmethode für den Standort aktiviert haben. Wenn die Clientpushmethode zur Installation des Configuration Manager-Clients verwendet wird, kann der Standort eine gegenseitige Kerberos-Authentifizierung anfordern. Diese Verbesserung sichert die Kommunikation zwischen dem Server und dem Client. Weitere Informationen finden Sie unter [Installieren von Clients mittels Clientpush](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

- **Nicht unterstützte Antischadsoftware-Clientversionen**: Auf mehr als 10 % der Clients werden System Center Endpoint Protection-Versionen ausgeführt, die nicht mehr unterstützt werden. Weitere Informationen finden Sie unter [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Vereinfachte Verwaltung

Einblicke zum Vereinfachen der täglichen Verwaltung Ihrer Umgebung.

- **Den Standort mit der Microsoft-Cloud für Configuration Manager-Updates verbinden**: Mit dieser Regel wird sichergestellt, dass Ihr Configuration Manager-Dienstverbindungspunkt innerhalb der letzten sieben Tage eine Verbindung mit der Microsoft-Cloud hergestellt hat. Diese Verbindung dient zum Herunterladen von Inhalten für reguläre Updates. Überprüfen Sie „DMPDownloader.log“ und „hman.log“. Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).

- **Nicht-CB-Clientversionen**: Führt alle Clients auf, deren Versionen nicht dem Current Branch-Build (CB) entsprechen. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../../clients/manage/upgrade/upgrade-clients.md).  

- **Clients auf eine unterstützte Windows 10-Version aktualisieren**: Ab Version 1902 meldet diese Regel Clients, auf denen eine nicht mehr unterstützte Windows 10-Version ausgeführt wird. Sie schließt auch Clients mit einer Windows 10-Version ein, bei denen das Serviceende bald erreicht sein wird (drei Monate).<!--3897268-->  

### <a name="software-center"></a>Software Center

Einblicke für die Softwarecenterverwaltung.

- **Benutzer an das Softwarecenter statt an den Anwendungskatalog weiterleiten**: Überprüfen Sie, ob Benutzer in den letzten 14 Tagen Anwendungen aus dem Anwendungskatalog installiert oder angefordert haben. Die primäre Funktionalität des Anwendungskatalogs ist jetzt im Softwarecenter verfügbar. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Veraltete Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).  

- **Neue Softwarecenterversion verwenden**: Die vorherige Version des Softwarecenters wird nicht mehr unterstützt. Legen Sie fest, dass Clients das neue Softwarecenter verwenden, indem Sie die Clienteinstellung **Neue Softwarecenterversion verwenden** in der Gruppe **Computer-Agent** aktivieren. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../clients/deploy/about-client-settings.md#use-new-software-center).  

### <a name="software-updates"></a>Softwareupdates

- **Clienteinstellungen sind nicht so konfiguriert, dass Clients Deltainhalte herunterladen dürfen.** : Einige Softwareupdates, die in Ihrer Umgebung synchronisiert werden, umfassen Deltainhalte. Aktivieren Sie die Clienteinstellung **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** . Wenn Sie diese Einstellung bei Bereitstellung dieser Updates nicht aktivieren, laden Clients unnötigerweise mehr Inhalte herunter als erforderlich. Weitere Informationen finden Sie unter [Clienteinstellungen – Softwareupdates](../../clients/deploy/about-client-settings.md#software-updates).

- **Softwareupdate-Produktkategorie für „Windows 10, Version 1903 und höher“, aktivieren**: Es gibt eine neue Softwareupdate-Produktkategorie für Windows 10, Version 1903 und höher. Wenn Sie Windows 10-Updates synchronisieren und über Clients mit Windows 10, Version 1903 oder höher, verfügen, wählen Sie in den Eigenschaften der Softwareupdatepunktkomponente die Produktkategorie **Windows 10, Version 1903 und höher** aus. Weitere Informationen finden Sie unter [Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Einblicke zur Bereitstellung und Wartung von Windows 10. Die Windows 10-Gruppe für Verwaltungseinblicke ist nur verfügbar, wenn mehr als die Hälfte der Clients unter Windows 7, Windows 8 oder Windows 8.1 ausgeführt wird.

- **Windows-Diagnosedaten und kommerziellen ID-Schlüssel konfigurieren**: Konfigurieren Sie Geräte mit einem kommerziellen ID-Schlüssel, und aktivieren Sie das Sammeln von Diagnosedaten, um Daten aus Desktop Analytics zu verwenden. Legen Sie Windows 10-Geräte auf Stufe **Erweitert (begrenzt)** oder höher fest. Weitere Informationen finden Sie unter [Aktivieren der Datenfreigabe für Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Regeln für Verwaltungseinblicke in Windows 10

![Verwaltungseinblicke: Regeln für Windows 10](./media/Windows-10-insights-group.png)
