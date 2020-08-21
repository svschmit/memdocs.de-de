---
title: Einblicke für die Verwaltung
titleSuffix: Configuration Manager
description: Informationen zur Funktionalität für Verwaltungseinblicke, die in der Configuration Manager-Konsole verfügbar ist.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700513"
---
# <a name="management-insights-in-configuration-manager"></a>Verwaltungseinblicke in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwaltungseinblicke von Configuration Manager stellen Informationen über den aktuellen Zustand Ihrer Umgebung bereit. Die Informationen basieren auf der Analyse von Daten aus der Standortdatenbank. Diese Einblicke vermitteln Ihnen ein genaueres Verständnis Ihrer Umgebung, sodass Sie entsprechende Maßnahmen ergreifen können. <!--1353967-->

## <a name="review-management-insights"></a>Aufrufen der Einblicke für die Verwaltung

Um die Einblicke anzuzeigen, muss Ihr Konto über die **Leseberechtigung** für das **Standortobjekt** verfügen.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Verwaltungseinblicke**, und wählen Sie **Alle Einblicke** aus.

    > [!NOTE]
    > Wenn Sie den Knoten **Management Insights** auswählen, wird das [Management Insights-Dashboard](#bkmk_insights) angezeigt.

1. Öffnen Sie die Management Insights-Gruppe, die Sie überprüfen möchten.

1. Wählen Sie im Menüband **Erkenntnisse anzeigen** aus.

Sie können die folgenden vier Registerkarten überprüfen:

- **Alle Regeln**: Gibt die gesamte Liste der Einblicke für die ausgewählte Gruppe an.

- **Abgeschlossen**:  Listet die Einblicke auf, die keine Aktion erfordern.

- **In Bearbeitung:** Zeigt Einblicke an, für die einige, aber nicht alle Voraussetzungen erfüllt sind.

- **Aktion erforderlich**: Diese Registerkarte listet Einblicke auf, die Sie benötigen, um Maßnahmen zu ergreifen. Wählen Sie **Weitere Details** aus, um Elemente anzuzeigen, für die eine Aktion erforderlich ist.

Der Bereich **Voraussetzungen** enthält zum Ausführen des ausgewählten Einblicks erforderliche Elemente.

Der folgende Screenshot zeigt z. B. ein Beispiel der Registerkarte **Alle Regeln** für die Gruppe **Clouddienste**:

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Verwaltungseinblicke: Alle Regeln und Voraussetzungen für die Clouddienstgruppe":::

Um die Details anzuzeigen, wählen Sie eine Regel und dann **Weitere Details** aus.

## <a name="operations"></a>Operationen (Operations)

Der Standort wertet die Anwendbarkeit der Verwaltungseinblicke wöchentlich neu aus. Wenn Sie einen Einblick manuell neu auswerten möchten, klicken Sie mit der rechten Maustaste auf den Einblick, und wählen Sie **Neu auswerten** aus.

Die Protokolldatei für Verwaltungseinblicke ist **SMS_DataEngine.log** auf dem Standortserver.

<!--1357930-->
Bei manchen Einblicken können Sie Aktionen ausführen. Wählen Sie einen Einblick und dann **Weitere Details** aus, und dann, wenn möglich, **Aktion ausführen**. Abhängig vom Einblick weist diese Aktion eine der folgenden Verhaltensweisen auf:

- Automatisches Navigieren in der Konsole zu dem Knoten, wo Sie weitere Maßnahmen ergreifen können. Wenn der Verwaltungseinblick z. B. die Änderung einer Clienteinstellung empfiehlt, besteht die Aktion im Navigieren zum Knoten **Clienteinstellungen**. Sie können dann weitere Maßnahmen ergreifen, indem Sie das standardmäßige oder ein benutzerdefiniertes Clienteinstellungsobjekt ändern.

- Navigieren Sie basierend auf einer Abfrage zu einer gefilterten Ansicht. Die Durchführung von Aktionen, die sich auf den Einblick für leere Sammlungen bezieht, zeigt z. B. nur diese Sammlungen in der Liste der Sammlungen an. Anschließend können Sie eine weitere Aktion durchführen, z.B. das Löschen einer Sammlung oder Ändern ihrer Mitgliedschaftsregeln.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Dashboard für Einblicke in die Verwaltung

<!--1357979-->

Wählen Sie den Knoten **Verwaltungseinblicke** aus, um ein grafisches Dashboard anzuzeigen. Dieses Dashboard zeigt eine Übersicht der Zustände von Einblicken und erleichtert Ihnen so, Ihren Fortschritt anzuzeigen.

Verwenden Sie die folgenden Filter am oberen Rand des Dashboards, um die Ansicht zu optimieren:

- Abgeschlossene anzeigen
- Optional
- Empfohlen
- Kritisch

Das Dashboard umfasst die folgenden Kacheln:  

- **Management Insights-Index:** Verfolgt den Gesamtfortschritt von Verwaltungseinblicken. Der Index beschreibt einen gewichteten Durchschnitt. Kritische Einblicke weisen den höchsten Wert auf. Optionale Einblicke weisen für diesen Index die geringste Gewichtung auf.

- **Management Insights-Gruppen:** Zeigt unter Berücksichtigung der Filter Prozentwerte für die Einblicke in jeder Gruppe an. Wählen Sie eine Gruppe aus, um einen Drilldown zu den spezifischen Einblicken in dieser Gruppe auszuführen.

- **Management Insights-Priorität:** Zeigt unter Berücksichtigung der Filter Prozentwerte für die Einblicke nach Priorität an.

- **Top 10 der anwendbaren Erkenntnisregeln**: Eine Tabelle der Einblicke, einschließlich der Priorität und des Zustands. Verwenden Sie das Feld **Filter** am oberen Rand der Tabelle, um in den verfügbaren Spalten nach Zeichenfolgen zu filtern. Das Dashboard sortiert die Tabelle in der folgenden Reihenfolge:

  - Status: Aktion erforderlich, Abgeschlossen, Unbekannt  
  - Priorität: Kritisch, Empfohlen, Optional  
  - Zuletzt geändert: Ältere Datumsangaben zuerst  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Screenshot vom Dashboard für die Einblicke in die Verwaltung" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Gruppen und Einblicke

Einblicke werden in folgende Verwaltungseinblickgruppen sortiert:

- [Anwendungen](#applications)
- [Clouddienste](#cloud-services)
- [Sammlungen](#collections)
- [Configuration Manager-Bewertung](#configuration-manager-assessment)
- [Optimierung für Remoteworker](#optimize-for-remote-workers)
- [Proaktive Wartung](#proactive-maintenance)
- [Sicherheit](#security)
- [Vereinfachte Verwaltung](#simplified-management)
- [Softwarecenter](#software-center)
- [Softwareupdates](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> An Ihrem Standort werden möglicherweise nicht alle folgenden Gruppen und Einblicke angezeigt. Einige Einblicke werden nicht angezeigt, wenn Sie den Standort bereits für die Empfehlung konfiguriert haben.

### <a name="applications"></a>Applications

Einblicke für Ihre Anwendungsverwaltung

- **Anwendungen ohne Bereitstellungen oder Verweise**: Listet diejenigen Anwendungen in Ihrer Umgebung auf, für die keine aktiven Bereitstellungen oder Verweise vorliegen. Verweise umfassen Abhängigkeiten, Tasksequenzen und virtuelle Umgebungen. Mit diesem Einblick können Sie nicht verwendete Anwendungen finden und löschen, um die in der Konsole angezeigte Anwendungsliste zu vereinfachen. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../../apps/deploy-use/deploy-applications.md).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Clouddienste

Dadurch werden Sie bei der Integration mit vielen Clouddiensten unterstützt, die die moderne Verwaltung Ihrer Geräte ermöglichen.

- **Bereitschaft für Co-Verwaltung bewerten**: Mit dieser Regel können Sie nachvollziehen, welche Schritte zum Aktivieren der Co-Verwaltung erforderlich sind. Für diesen Einblick gelten Voraussetzungen. Weitere Informationen finden Sie unter [Übersicht über die Co-Verwaltung](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Devices not uploaded to Azure AD** (Nicht in Azure AD hochgeladene Geräte): Ab Version 2002 listet dieser Einblick Geräte auf, die der Standort nicht in Azure Active Directory (Azure AD) hochgeladen hat, da Sie ihn nicht für HTTPS konfiguriert haben.<!--6268489--> Konfigurieren Sie [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md) (Erweitertes HTTP), oder aktivieren Sie mindestens einen Verwaltungspunkt für HTTPS. Wenn Sie den Standort bereits für die HTTPS-Kommunikation konfiguriert haben, wird dieser Einblick nicht angezeigt.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Cloud Management Gateway aktivieren**: Das Cloudverwaltungsgateway (Cloud Management Gateway, CMG) bietet eine einfache Möglichkeit zum Verwalten von Configuration Manager-Clients über das Internet. Durch die Bereitstellung des CMG als Clouddienst in Microsoft Azure können Sie weiterhin Clients verwalten und bedienen, die sich im Internet bewegen. Mit CMG benötigen Sie keine zusätzliche lokale Infrastruktur, die für das Internet verfügbar gemacht wird. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Geräte für Hybrid-Azure AD-Einbindung aktivieren**: In Azure AD eingebundene Geräte ermöglichen Benutzern, sich mit ihren Domänenanmeldeinformationen anzumelden, und stellen sicher, dass die Geräte die Sicherheits- und Konformitätsstandards der Organisation erfüllen. Weitere Informationen finden Sie unter [Überlegungen zum Entwurf der Azure Active Directory-Hybrid-Identität](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Sites that don't have proper HTTPS configuration** (Standorte ohne richtige HTTPS-Konfiguration): Ab Version 2002 listet dieser Einblick Standorte in Ihrer Hierarchie auf, die nicht ordnungsgemäß für HTTPS konfiguriert sind. Diese Konfiguration verhindert, dass der Standort [Sammlungsmitgliedschaftsergebnisse mit Azure AD-Gruppen synchronisiert](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Sie führt möglicherweise dazu, dass Azure AD Sync nicht alle Geräte hochlädt. Die Verwaltung dieser Clients funktioniert möglicherweise nicht richtig.<!--6268489--> Konfigurieren Sie [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md) (Erweitertes HTTP), oder aktivieren Sie mindestens einen Verwaltungspunkt für HTTPS. Wenn Sie den Standort bereits für die HTTPS-Kommunikation konfiguriert haben, wird dieser Einblick nicht angezeigt.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Clients auf die aktuelle Version von Windows 10 aktualisieren**: Windows 10, Version 1709 oder höher, verbessert und modernisiert die Benutzerfreundlichkeit für Ihre Benutzer. Weitere Informationen finden Sie unter [Wichtige Artikel zur Übernahme von Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Sammlungen

Einblicke, die die Verwaltung vereinfachen, indem sie Sammlungen bereinigen und neu konfigurieren.

- **Leere Sammlungen**: Führt die Sammlungen in Ihrer Umgebung auf, die keine Elemente enthalten. Weitere Informationen finden Sie unter [Verwalten von Sammlungen](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Collections with no query rules and no direct members** (Sammlungen ohne Abfrageregeln und ohne direkte Mitglieder): Sie können die Liste der Sammlungen in Ihrer Hierarchie vereinfachen, indem Sie diese Sammlungen löschen.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Collections with the same re-evaluation start time** (Sammlungen mit der gleichen Startzeit für eine Neuauswertung): Diese Sammlungen weisen den gleichen Neuauswertungszeitpunkt wie andere Sammlungen auf. Ändern Sie den Neuauswertungszeitpunkt, um Konflikte zu vermeiden.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Collections with query time over 5 minutes** (Sammlungen mit einer Abfragedauer von mehr als 5 Minuten): Überprüfen Sie die Abfrageregeln für diese Sammlung. Ziehen Sie eine Änderung oder das Löschen der Sammlung in Betracht.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- Die folgenden Einblicke schließen Konfigurationen ein, die unnötige Lasten an dem Standort verursachen können. Überprüfen Sie diese Sammlungen, und löschen Sie diese entweder anschließend, oder deaktivieren Sie die Sammlungsregelauswertung:

  - **Collections with no query rules and incremental updates enabled** (Sammlungen ohne Abfrageregeln und mit aktivierten inkrementellen Updates)<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Collections with no query rules and enabled for any schedule** (Sammlungen ohne Abfrageregeln und aktiviert für jeden Plan)<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Collections with no query rules and schedule full evaluation selected** (Sammlungen ohne Abfrageregeln und aktiviertem Zeitplan für eine vollständige Auswertung)<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Configuration Manager-Bewertung

<!--3607758-->

Ab Version 2002 wird diese Gruppe von Microsoft Premier Field Engineering bereitgestellt. Diese Einblicke sind eine Stichprobe aus einer ganzen Reihe von Überprüfungen, die von Microsoft Premier im [Diensthub](/services-hub/health/getting_started_with_on_demand_assessments) bereitgestellt werden.

- **Active Directory-Sicherheitsgruppenermittlung für eine zu häufige Ausführung konfiguriert:** Sie müssen normalerweise nicht konfigurieren, dass die Active Directory-Sicherheitsgruppenermittlung öfter als alle drei Stunden ausgeführt wird. Eine häufigere Konfiguration kann zu Leistungseinbußen bei Active Directory, dem Netzwerk und Configuration Manager führen. Aktivieren Sie die inkrementelle Installation anstatt einen vollständigen Synchronisierungszeitplan zu verwenden. Weitere Informationen finden Sie unter [Active Directory-Gruppenermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Active Directory-Systemermittlung für eine zu häufige Ausführung konfiguriert:** Sie müssen normalerweise nicht konfigurieren, dass die Active Directory-Systemermittlung öfter als alle drei Stunden ausgeführt wird. Eine häufigere Konfiguration kann zu Leistungseinbußen bei Active Directory, dem Netzwerk und Configuration Manager führen. Aktivieren Sie die inkrementelle Installation anstatt einen vollständigen Synchronisierungszeitplan zu verwenden. Weitere Informationen finden Sie unter [Active Directory-Systemermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Active Directory-Benutzerermittlung für eine zu häufige Ausführung konfiguriert:** Sie müssen normalerweise nicht konfigurieren, dass die Active Directory-Benutzerermittlung öfter als alle drei Stunden ausgeführt wird. Eine häufigere Konfiguration kann zu Leistungseinbußen bei Active Directory, dem Netzwerk und Configuration Manager führen. Aktivieren Sie die inkrementelle Installation anstatt einen vollständigen Synchronisierungszeitplan zu verwenden. Weitere Informationen finden Sie unter [Active Directory-Benutzerermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Auf "Alle Systeme" oder "Alle Benutzer" beschränkte Sammlungen:** Überprüfen Sie alle Sammlungen, die die Sammlungen **Alle Systeme** oder **Alle Benutzer** als begrenzende Sammlung verwenden. Configuration Manager aktualisiert die Mitgliedschaft dieser Standardsammlungen mit Daten aus den Active Directory-Ermittlungsmethoden. Diese Daten sind möglicherweise keine gültigen Informationen für Configuration Manager-Clients.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **Frequenzermittlung ist deaktiviert:** Die Frequenzermittelung erfordert die Installation des Configuration Manager-Clients auf Geräten. Dies stellt die einzige Ermittlungsmethode dar, die von Clients gestartet wird. Alle anderen Methoden kommen auf Standortservern vor. Die Frequenzermittlung ist wichtig, damit der Clientaktivitätstatus aktuell bleibt. Sie stellt sicher, dass für den Standort nicht versehentlich die Ressourcendatensätze aus der Standortdatenbank veralten. Weitere Informationen finden Sie unter [Frequenzermittlung](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Sammlungsabfragen mit langer Ausführungszeit für inkrementelle Updates aktiviert:** Sammlungen, deren letzte inkrementelle Aktualisierung mehr als 30 Sekunden zurückliegt, verwenden Standortserver- und Datenbankressourcen, die potenziell die Gesamtleistung von Configuration Manager beeinträchtigen könnten. Weitere Informationen finden Sie unter [Bewährte Methoden für Sammlungen](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Anzahl von Anwendungen und Paketen auf Verteilungspunkten verringern:** Microsoft unterstützt offiziell eine Gesamtgröße von bis zu 10.000 Paketen und Anwendungen auf einem Verteilungspunkt. Eine Überschreitung dieser Gesamtgröße kann zu Funktionsproblemen führen. Weitere Informationen finden Sie unter [Anpassen und Skalieren von Zahlen: Verteilungspunkt](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **Problem mit Installation am sekundären Standort:** Der Installationsstatus einiger sekundärer Standort ist **ausstehend** oder **fehlerhaft**. Diese Status bedeuten, dass Sie die Installation zwar gestartet haben, diese jedoch nicht erfolgreich abgeschlossen wurde. Bis zur abgeschlossenen Installation des sekundären Standorts können Clients nicht ordnungsgemäß mit dem primären Standort kommunizieren. Überprüfung Sie den Arbeitsbereich **Überwachung**, und wiederholen Sie die Installation. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](install-in-console-updates.md#bkmk_retry).<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Alle Standorte auf dieselbe Version aktualisieren:** Verwenden Sie in einer Hierarchie dieselbe Version von Configuration Manager. Durch diese Konfiguration wird sichergestellt, dass alle Standorte über die gleiche Funktionalität verfügen. Standorte mit unterschiedlichen Versionen in derselben Hierarchie führen zu Interoperabilitätsszenarios. Spätere Versionen von Configuration Manager enthalten neue Features und können bekannte Probleme lösen. Weitere Informationen finden Sie unter [Interoperabilität zwischen verschiedenen Versionen](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Weitere Informationen zu diesen Einblicken finden Sie unter [Schritte zur Bereinigung für Einblicke für die Configuration Manager-Verwaltung](/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Wenn Sie bereits Kunde von Microsoft Unified oder Microsoft Premier sind, melden Sie sich am [Diensthub](https://serviceshub.microsoft.com/assessments/) für weitere bedarfsgesteuerte Bewertungen an.
>
> Weitere Informationen zu Microsoft-Diensten finden Sie in den [Unterstützungslösungen](https://www.microsoft.com/enterprise/services/support).

### <a name="operating-system-deployment"></a>Betriebssystembereitstellung

<!--6982275-->

Ab Version 2006 unterstützen die folgenden Verwaltungseinblicke Sie bei der Verwaltung der Richtliniengröße von Tasksequenzen. Wenn die Größe der Tasksequenzrichtlinie 32 MB überschreitet, kann die große Richtlinie vom Client nicht verarbeitet werden. Der Client kann dann die Tasksequenzbereitstellung nicht ausführen.

- **Große Tasksequenzen können zu einer Überschreitung der maximal zulässigen Richtliniengröße beitragen**: Wenn Sie diese Tasksequenzen bereitstellen, können die großen Richtlinienobjekte möglicherweise von den Clients nicht verarbeitet werden. Verringern Sie die Größe der Tasksequenzrichtlinie, um potenzielle Probleme bei der Richtlinienverarbeitung zu verhindern.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **Die Gesamtgröße der Richtlinien für Tasksequenzen überschreitet den für Richtlinien zulässigen Höchstwert**: Die Richtlinie für diese Tasksequenzen kann von Clients nicht verarbeitet werden, da sie zu groß ist. Verringern Sie die Größe der Tasksequenzrichtlinie, damit die Bereitstellung auf Clients ausgeführt werden kann.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Weitere Informationen finden Sie unter [Reduzieren der Größe einer Tasksequenzrichtlinie](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

In Version 2006 wurden die folgenden Einblicke aus der Gruppe **Proaktive Wartung** in diese Gruppe verschoben:

- **Nicht verwendete Startimages**: Startimages, auf die nicht für die Verwendung für PXE-Start oder Tasksequenz verwiesen wird. Weitere Informationen finden Sie unter [Verwalten von Startimages](../../../osd/get-started/manage-boot-images.md).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Optimierung für Remoteworker

<!--6982226-->

Ab Version 2006 helfen Ihnen die folgenden Einblicke, bessere Funktionen für Remoteworker bereitzustellen und die Last Ihrer Infrastruktur zu verringern:

- **Mit dem VPN verbundene Clients für das Vorziehen cloudbasierter Inhaltsquellen konfigurieren**: Um den Datenverkehr im VPN zu reduzieren, wird die Begrenzungsgruppenoption, **Cloudbasierte Quellen lokalen Quellen vorziehen** aktiviert. Diese Option ermöglicht Clients das Herunterladen von Inhalten aus dem Internet anstelle von Verteilungspunkten über das VPN. Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../deploy/configure/boundary-groups.md#bkmk_bgoptions4).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **VPN-Begrenzungsgruppen definieren**: Erstellen Sie eine VPN-Begrenzung, und ordnen Sie sie einer Begrenzungsgruppe zu. Ordnen Sie der Gruppe VPN-spezifische Standortsysteme zu, und konfigurieren Sie die Einstellungen für Ihre Umgebung. Dieser Einblick prüft auf mindestens eine Begrenzungsgruppe mit mindestens einer vorhandenen VPN-Begrenzung. Wählen Sie in den Eigenschaften dieses Einblicks **Aktionen überprüfen** aus, um zum Knoten **Begrenzungsgruppen** zu gelangen. Weitere Informationen finden Sie unter [VPN-Begrenzungstyp](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Peer-to-Peer-Inhaltsfreigabe für mit dem VPN verbundene Clients deaktivieren**: Um unnötigen Peer-to-Peer-Datenverkehr zu verhindern, der den Remoteclients wahrscheinlich keinen Nutzen bringt, deaktivieren Sie die Begrenzungsgruppenoption  **Peerdownloads in dieser Begrenzungsgruppe zuzulassen**. Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../deploy/configure/boundary-groups.md#bkmk_bgoptions1).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Proaktive Wartung

<!--1352184-->
Die Einblicke in dieser Gruppe markieren potenzielle Konfigurationsprobleme, die Sie durch die Wartung von Configuration Manager-Objekten vermeiden können.

- **Begrenzungsgruppen ohne zugewiesene Standortsysteme**: Ohne zugewiesene Standortsysteme können Begrenzungsgruppen nur zur Standortzuweisung verwendet werden. Weitere Informationen finden Sie unter [Configure boundary groups](../deploy/configure/boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Begrenzungsgruppen ohne Mitglieder**: Begrenzungsgruppen sind nicht für Standortzuweisung oder Inhaltssuche anwendbar, wenn sie keine Mitglieder enthalten. Weitere Informationen finden Sie unter [Configure boundary groups](../deploy/configure/boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Verteilungspunkte, die keinen Inhalt für Clients bereitstellen**: Verteilungspunkte, die in den letzten 30 Tagen keine Inhalte für Clients zur Verfügung gestellt haben. Diese Daten basieren auf Berichten von Clients zu ihrem Downloadverlauf. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **WSUS-Bereinigung aktivieren**: Stellt sicher, dass Sie die Option zum Ausführen der WSUS-Bereinigung für die Eigenschaften der Softwareupdatepunkt-Komponente aktiviert haben. Diese Option verbessert die WSUS-Leistung. Weitere Informationen finden Sie unter [Wartung für Softwareupdates](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Nicht verwendete Konfigurationselemente**: Konfigurationselemente, die nicht Teil einer Konfigurationsbaseline und älter als 30 Tage sind. Weitere Informationen finden Sie unter [Erstellen von Konfigurationsbaselines](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Peercachequellen auf die neueste Version des Configuration Manager-Clients aktualisieren**:<!--1358008--> Identifizieren Sie Clients, die als Peercachequelle dienen, aber nicht von einer Clientversion vor 1806 aktualisiert wurden. Clients vor Version 1806 können nicht als Peercachequelle für Clients verwendet werden, die Version 1806 oder höher ausführen. Wählen Sie **Aktion ausführen** aus, um eine Geräteansicht zu öffnen, die die Clientliste anzeigt.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> In Version 2006 wurde der Einblick für **Nicht verwendete Startimages** in die neue Gruppe [Betriebssystembereitstellung](#operating-system-deployment) verschoben.

### <a name="security"></a>Sicherheit

Einblicke zur Verbesserung der Sicherheit Ihrer Infrastruktur und Geräte.

- **NTLM-Fallback ist aktiviert**:<!--4572953--> Ab Version 1906 erkennt dieser Einblick, ob Sie die weniger sichere NTLM-Authentifizierungs-Fallbackmethode für den Standort aktiviert haben. Wenn die Clientpushmethode zur Installation des Configuration Manager-Clients verwendet wird, kann der Standort eine gegenseitige Kerberos-Authentifizierung anfordern. Diese Verbesserung sichert die Kommunikation zwischen dem Server und dem Client. Weitere Informationen finden Sie unter [Installieren von Clients mittels Clientpush](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Nicht unterstützte Antischadsoftware-Clientversionen**: Auf mehr als 10 % der Clients werden System Center Endpoint Protection-Versionen ausgeführt, die nicht mehr unterstützt werden. Weitere Informationen finden Sie unter [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Vereinfachte Verwaltung

Einblicke zum Vereinfachen der täglichen Verwaltung Ihrer Umgebung.

- **Den Standort mit der Microsoft-Cloud für Configuration Manager-Updates verbinden**: Mit diesem Einblick wird sichergestellt, dass Ihr Configuration Manager-Dienstverbindungspunkt innerhalb der letzten sieben Tage eine Verbindung mit der Microsoft-Cloud hergestellt hat. Diese Verbindung dient zum Herunterladen von Inhalten für reguläre Updates. Überprüfen Sie „DMPDownloader.log“ und „hman.log“. Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Nicht-CB-Clientversionen**: Führt alle Clients auf, deren Versionen nicht dem Current Branch-Build (CB) entsprechen. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Clients auf eine unterstützte Windows 10-Version aktualisieren**:<!--3897268--> Dieser Einblick meldet Clients, auf denen eine nicht mehr unterstützte Windows 10-Version ausgeführt wird. Sie schließt auch Clients mit einer Windows 10-Version ein, bei denen das Serviceende bald erreicht sein wird (drei Monate).<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Software Center

Einblicke für die Softwarecenterverwaltung.

- **Benutzer an das Softwarecenter statt an den Anwendungskatalog weiterleiten**: Überprüfen Sie, ob Benutzer in den letzten 14 Tagen Anwendungen aus dem Anwendungskatalog installiert oder angefordert haben. Die primäre Funktionalität des Anwendungskatalogs ist jetzt im Softwarecenter verfügbar. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Veraltete Features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Neue Softwarecenterversion verwenden**: Die vorherige Version des Softwarecenters wird nicht mehr unterstützt. Legen Sie fest, dass Clients das neue Softwarecenter verwenden, indem Sie die Clienteinstellung **Neue Softwarecenterversion verwenden** in der Gruppe **Computer-Agent** aktivieren. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../clients/deploy/about-client-settings.md#use-new-software-center).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Softwareupdates

- **Clienteinstellungen sind nicht so konfiguriert, dass Clients Deltainhalte herunterladen dürfen.** : Einige Softwareupdates, die in Ihrer Umgebung synchronisiert werden, umfassen Deltainhalte. Aktivieren Sie die Clienteinstellung **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** . Wenn Sie diese Einstellung bei Bereitstellung dieser Updates nicht aktivieren, laden Clients unnötigerweise mehr Inhalte herunter als erforderlich. Weitere Informationen finden Sie unter [Clienteinstellungen – Softwareupdates](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Softwareupdate-Produktkategorie für „Windows 10, Version 1903 und höher“, aktivieren**: Es gibt eine neue Softwareupdate-Produktkategorie für Windows 10, Version 1903 und höher. Wenn Sie Windows 10-Updates synchronisieren und über Clients mit Windows 10, Version 1903 oder höher, verfügen, wählen Sie in den Eigenschaften der Softwareupdatepunktkomponente die Produktkategorie **Windows 10, Version 1903 und höher** aus. Weitere Informationen finden Sie unter [Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Einblicke zur Bereitstellung und Wartung von Windows 10. Die Windows 10-Gruppe für Verwaltungseinblicke ist nur verfügbar, wenn mehr als die Hälfte der Clients unter Windows 7, Windows 8 oder Windows 8.1 ausgeführt wird.

- **Windows-Diagnosedaten und kommerziellen ID-Schlüssel konfigurieren**: Konfigurieren Sie Geräte mit einem kommerziellen ID-Schlüssel, und aktivieren Sie das Sammeln von Diagnosedaten, um Daten aus Desktop Analytics zu verwenden. Legen Sie Windows 10-Geräte auf Stufe **Erweitert (begrenzt)** oder höher fest. Weitere Informationen finden Sie unter [Aktivieren der Datenfreigabe für Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->