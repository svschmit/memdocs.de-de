---
title: Endpunktanalyse (Vorschauversion)
titleSuffix: Configuration Manager
description: Dieser Artikel enthält Anweisungen zur Vorschauversion der Endpunktanalyse.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: da8c52dabf27ddf0992d9f405400b3ac984f2ecc
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455122"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a> Endpunktanalyse (Vorschauversion)

> [!Note]  
> Diese Informationen beziehen sich auf eine Previewfunktion, die sich vor ihrer kommerziellen Freigabe noch grundlegend ändern kann. Microsoft übernimmt bezüglich der hier bereitgestellten Informationen keine Gewährleistungen, weder ausdrücklich noch konkludent. 
>
> Weitere Informationen zu Änderungen an der Endpunktanalyse finden Sie unter [Neues bei der Endpunktanalyse](whats-new-endpoint-analytics.md). 
>
>Wenn Sie an der privaten Vorschau der Endpunktanalyse teilnehmen möchten, geben Sie die Details [in diesem Formular](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u) ein. Mandanten werden bei der fortgesetzten Erweiterung der Vorschau als Flight bereitgestellt.


## <a name="endpoint-analytics-overview"></a>Endpunktanalyse – Übersicht

Es ist nicht ungewöhnlich, dass Endbenutzer lange Startzeiten oder andere Unterbrechungen erleben. Diese Unterbrechungen können auf eine Kombination folgender Punkte zurückzuführen sein:

- Legacyhardware
- Softwarekonfigurationen, die nicht für die Endbenutzererfahrung optimiert sind
- Probleme, die durch Konfigurationsänderungen und Updates verursacht werden

Diese Probleme und andere Probleme bei der Endbenutzererfahrung bleiben bestehen, da die IT-Abteilung nicht über einen großen Einblick in die Endbenutzererfahrung verfügt. Im Allgemeinen erfolgt der einzige Einblick in diese Probleme durch einem langsamen, kostspieligen Supportkanal, der in der Regel keine klaren Informationen zu den zu optimierenden Anforderungen liefert. Es ist nicht nur, dass die IT-Abteilung die Kosten dieser Probleme trägt. Die Zeit, die IT-Mitarbeiter für Probleme aufwenden, ist auch wertvoll. Leistungs-, Zuverlässigkeits- und Supportprobleme, die die Benutzerproduktivität reduzieren, können sich auch stark auf die Bilanz eines Unternehmens auswirken.

Die **Endpunktanalyse** zielt darauf ab, durch Erkenntnisse über die Benutzerfreundlichkeit die Benutzerproduktivität zu verbessern und die IT-Supportkosten zu senken. Anhand der gewonnenen Erkenntnisse können IT-Mitarbeitern die Endbenutzererfahrung durch proaktiven Support optimieren und durch Bewertung der Auswirkungen von Konfigurationsänderungen auf Benutzer Beeinträchtigungen der Benutzerfreundlichkeit erkennen.

Das erste Release konzentriert sich auf drei Dinge:

- [**Empfohlene Software**](#bkmk_uea_rs): Empfehlungen, die für die optimale Benutzererfahrung sorgen
- [**Skripterstellung für proaktive Korrekturen**](#bkmk_uea_prs): Beheben allgemeiner Supportprobleme, bevor Endbenutzer Probleme bemerken
- [**Startleistung**](#bkmk_uea_bp): Unterstützung der IT-Mitarbeiter bei Bestrebungen, Benutzern die Zeit vom Einschalten bis zur Produktivität zu verkürzen und lange Start- und Anmeldeverzögerungen zu vermeiden

Dieses Release ist erst der Anfang. Schon bald nach diesem ersten Release werden wir neue Einblicksmöglichkeiten für weitere zentrale Faktoren des Benutzererlebnisses verfügbar machen. Weitere Informationen zu Änderungen an der Endpunktanalyse finden Sie unter [Neues bei der Endpunktanalyse](whats-new-endpoint-analytics.md).

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a> Erste Schritte

Stellen Sie sicher, dass Sie die Voraussetzungen erfüllen, und beginnen Sie dann mit dem Sammeln von Daten, um die Endpunktanalyse zu verwenden. 

### <a name="technical-prerequisites"></a>Technische Voraussetzungen

Für diese Vorschau können Sie Geräte über Configuration Manager oder Microsoft Intune registrieren. 

#### <a name="to-enroll-devices-via-intune-this-preview-requires"></a><a name="bkmk_uea__intune_prereq"></a> Zum Registrieren von Geräten über Intune ist bei dieser Vorschau Folgendes erforderlich:
- Bei Intune registrierte Windows 10-Geräte
- Erkenntnisse zur Startleistung sind nur für Geräte verfügbar, auf denen Version 1903 oder höher von Windows 10 Enterprise ausgeführt wird (Home- und Professional-Editionen werden derzeit nicht unterstützt). Darüber hinaus muss es sich bei den Geräten um in Azure AD eingebundene (Hybrid-) Geräte handeln. Geräte, die dem Arbeitsplatz beigetreten sind, werden derzeit nicht unterstützt.
- Netzwerkkonnektivität von Geräten zur öffentlichen Microsoft-Cloud. Weitere Informationen finden Sie unter [Endpunkte](#bkmk_uea_endpoints).
- Die [Intune-Rolle „Dienstadministrator“](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) ist erforderlich, um mit dem [Sammeln von Daten beginnen zu können](#bkmk_uea_start).
   - Durch Klicken auf **Start** stimmen Sie zu und bestätigen, dass Ihre Kundendaten außerhalb des von Ihnen bei der Bereitstellung Ihres Microsoft Intune-Clients ausgewählten Speicherorts gespeichert werden können.
   - Nachdem Sie zum Sammeln von Daten auf **Starten** geklickt haben, können andere schreibgeschützte Rollen die Daten anzeigen.

#### <a name="to-enroll-devices-via-configuration-manager-this-preview-requires"></a><a name="bkmk_uea__cm_prereq"></a> Zum Registrieren von Geräten über Configuration Manager ist bei dieser Vorschau Folgendes erforderlich:
- Configuration Manager, Version 2002 oder höher
- Clients mit Upgrade auf Version 2002 oder höher
- Aktiviertes [Anfügen von Mandanten in Microsoft Endpoint Manager](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) mit Nordamerika oder Europa als Azure-Mandantenstandort (wird bald auf andere Regionen ausgeweitet)

#### <a name="proactive-remediation-scripting-requires"></a><a name="bkmk_uea__prs_prereq"></a> Die Skripterstellung für proaktive Korrekturen erfordert Folgendes:
Unabhängig davon, ob Geräte über Intune oder Configuration Manager registriert werden, gelten für die [**Skripterstellung für proaktive Korrekturen**](#bkmk_uea_prs) die folgenden Anforderungen:
- Bei den Geräten muss es sich um in Azure AD eingebundene (Hybrid-) Geräte handeln, die eine der folgenden Bedingungen erfüllen:
- Ein Windows 10 Enterprise-, Professional- oder Education-Gerät, das von Intune verwaltet wird
- Ein [gemeinsam verwaltetes](../../comanage/overview.md) Gerät, auf dem Version 1607 oder höher von Windows 10 Enterprise ausgeführt wird, und dessen [Arbeitsauslastung der Client-Apps](../../comanage/workloads.md#client-apps) auf Intune zeigt.
- Ein [gemeinsam verwaltetes](../../comanage/overview.md) Gerät, auf dem Version 1903 oder höher von Windows 10 Enterprise ausgeführt wird, und dessen [Arbeitsauslastung der Client-Apps](../../comanage/workloads.md#client-apps) auf Configuration Manager zeigt.

### <a name="licensing-prerequisites"></a>Lizenzvoraussetzungen

Die Endpunktanalyse ist in den folgenden Plänen enthalten: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) oder höher
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) oder höher

Für proaktive Wartungsmaßnahmen ist auch eine der folgenden Lizenzen für die verwalteten Geräte erforderlich:
- Windows 10 Enterprise E3 oder E5 (enthalten in Microsoft 365 F3, E3 oder E5)
- Windows 10 Education A3 oder A5 (enthalten in Microsoft 365 A3 oder A5)
- Windows Virtual Desktop Access E3 oder E5

### <a name="permissions"></a>Berechtigungen

#### <a name="endpoint-analytics-permissions"></a>Endpunktanalyseberechtigungen

Für die Endpunktanalyse werden die folgenden Berechtigungen verwendet:
- **Lesen** in der Kategorie **Gerätekonfigurationen**.
- **Lesen** in der Kategorie **Organisation**. <!--temporary for pp-->
- Die der Rolle des Benutzers entsprechenden Berechtigungen in der Kategorie **Endpunktanalyse**.

Ein schreibgeschützter Benutzer benötigt sowohl für die Kategorie **Gerätekonfigurationen** als auch für die Kategorie **Endpunktanalyse** lediglich die Berechtigung **Lesen**. Ein Intune-Administrator benötigt normalerweise alle Berechtigungen.

#### <a name="proactive-remediations-permissions"></a>Berechtigungen für proaktive Korrekturen

Für proaktive Korrekturen benötigt der Benutzer in der Kategorie **Gerätekonfigurationen** Berechtigungen, die seiner Rolle entsprechen.  Berechtigungen in der Kategorie **Endpunktanalyse** sind nicht erforderlich, wenn der Benutzer nur proaktive Korrekturen verwendet.

Ein [Intune-Dienstadministrator](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) muss die Lizenzierungsanforderungen bestätigen, bevor die proaktiven Korrekturen zum ersten Mal verwendet werden.

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a> Beginn des Sammelns von Daten
- Wenn Sie nur von Intune verwaltete Geräte registrieren, fahren Sie mit dem Abschnitt [Durchführen des Onboardings im Endpunktanalyseportal](#bkmk_uea_onboard) fort.

- Wenn Sie Geräte registrieren, die von Configuration Manager verwaltet werden, müssen Sie die folgenden Schritte ausführen:
   - [Aktivieren der Datensammlung für Endpunktanalyse in Configuration Manager](#bkmk_uea_cm_enroll)
   - [Aktivieren des Datenuploads in Configuration Manager](#bkmk_uea_cm_upload)
   - [Durchführen des Onboardings im Endpunktanalyseportal](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a> Registrieren von Geräten, die von Configuration Manager verwaltet werden
<!--6051638, 5924760-->
Bevor Sie Configuration Manager-Geräte registrieren, überprüfen Sie die [Voraussetzungen](#bkmk_uea_prereq) beispielsweise dass [Microsoft Endpoint Manager-Mandanten anfügen](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) aktiviert ist. 

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a> Aktivieren der Datensammlung für Endpunktanalyse in Configuration Manager

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen**.
1. Klicken Sie auf die rechte Maustaste, und wählen Sie **Eigenschaften** und dann **Computer-Agent** aus.
1. Legen Sie **Datensammlung für Endpunktanalyse aktivieren** auf **Ja** fest.
   > [!Important] 
   > Wenn Sie über eine bereits auf Ihren Geräten bereitgestellte benutzerdefinierte Client-Agent-Einstellung verfügen, müssen Sie die Option **Datensammlung für Endpunktanalyse aktivieren** in dieser benutzerdefinierten Einstellung aktualisieren und dann erneut auf Ihren Computern bereitstellen, damit sie wirksam wird.

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a> Aktivieren des Datenuploads in Configuration Manager

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste** > **Co-Verwaltung**.
1. Wählen Sie **CoMgmtSettingsProd** aus, und klicken Sie auf **Eigenschaften**.
1. Aktivieren Sie auf der Registerkarte **Upload konfigurieren** die Option **Endpunktanalyse für Geräte aktivieren, die in Microsoft Endpoint Manager hochgeladen werden**.

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Endpunktanalyse für Geräte aktivieren, die in Microsoft Endpoint Manager hochgeladen werden" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a> Durchführen des Onboardings im Endpunktanalyseportal
Das Onboarding über das Endpunktanalyseportal ist sowohl für mit Configuration Manager als auch für mit Intune verwaltete Geräte erforderlich.

1. Wechseln Sie zu `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`.
1. Klicken Sie auf **Start**. Dadurch wird automatisch ein Konfigurationsprofil zur Erfassung von Startleistungsdaten von allen infrage kommenden Geräten zugewiesen. Sie können die Liste der [zugewiesenen Geräte später ändern](#bkmk_uea_profile). Es kann bis zu 24 Stunden dauern, bis Startleistungsdaten von Ihren bei Intune registrierten Geräten nach einem Neustart eingetragen werden.
   - Weitere Informationen zu häufigen Problemen finden Sie unter [Beheben von Problemen bei der Geräteregistrierung der Startleistung](#bkmk_uea_enrollment_tshooter).

## <a name="overview-page"></a>Übersichtsseite

Sobald Ihre Daten fertig sind, werden einige Informationen auf der Seite **Übersicht** angezeigt, die unten ausführlicher erläutert werden:

- Die **Bewertung der Benutzerfreundlichkeit** ist ein im Verhältnis 50:50 gewichteter Durchschnitt aus den Werten für **Empfohlene Software** und **Startleistung**. Wir werden künftig weitere Teilbewertungen ergänzen.

- Sie können Ihre aktuelle Bewertung mit anderen Bewertungen vergleichen, indem Sie eine Baseline festlegen.
  - Wie im Abschnitt [Baseline](#bkmk_uea_baselines) beschrieben, gibt es eine integrierte Baseline für den *Kommerziellen Median*, damit Sie sehen, wie Sie im Vergleich mit einem typischen Unternehmen abschneiden. Sie können neue Baselines auf Basis Ihrer aktuellen Metriken erstellen, sodass Sie den Fortschritt nachverfolgen oder Regressionen im Laufe der Zeit anzeigen können.
   - Für Ihre Gesamtbewertung und Ihre Teilbewertungen werden Baselinemarker angezeigt. Wenn eine der Bewertungen über den konfigurierbaren Schwellenwert hinaus von der ausgewählten Baseline abweichend rückläufig ist, wird die Bewertung rot angezeigt, und die Bewertung, die sich am meisten verschlechtert, erhält die Kennzeichnung, dass Eingreifen erforderlich ist.
  - Der Status **Nicht genügend Daten** bedeutet, dass Sie nicht über genügend Geräte für eine aussagekräftige Bewertung verfügen. Zurzeit sind mindestens fünf Geräte erforderlich.

- **Filter** ermöglichen Ihnen, Ihre Bewertung für eine Teilmenge von Geräten oder Benutzern anzuzeigen. Die Filterfunktionalität ist in dieser Vorschau jedoch nicht aktiviert.

- **Erkenntnisse und Empfehlungen** ist eine priorisierte Liste zur Verbesserung der Bewertung. Diese Liste wird nach dem Kontext des Unterknotens gefiltert, wenn Sie zu **Bewährte Methoden** oder **Empfohlene Software** navigieren.

[![Übersichtsseite zur Endpunktanalyse](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a> Empfohlene Software

> [!Important]  
> Mit Endpunktanalyse wird die Bewertung der **Softwareakzeptanz** für alle Ihre mit Intune verwalteten Geräte berechnet, unabhängig davon, ob sie in der Endpunktanalyse registriert wurden oder nicht.

Bestimmte Software ist dafür bekannt, dass sie die Endbenutzerleistung unabhängig von Integritätsmetriken auf niedrigerer Ebene verbessert. Windows 10 hat z. B. einen viel höheren Net Promoter Score als Windows 7. Bei der **Softwareakzeptanz** handelt es sich um eine Zahl zwischen 0 und 100, die einen gewichteten Durchschnitt des Prozentsatzes der Geräte darstellt, auf denen verschiedene empfohlene Software bereitgestellt ist. Die aktuelle Gewichtung ist für Windows höher als für die anderen Metriken, da Benutzer damit häufiger interagieren. Die Metriken werden unten beschrieben: 

[![Softwareempfehlungsseite für die Endpunktanalyse](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10 bietet eine bessere Benutzererfahrung als ältere Versionen von Windows. Weitere Informationen finden Sie im [TEI-Whitepaper](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf).

Diese Metrik misst den Prozentsatz der Geräte unter Windows 10 im Vergleich zu denen mit einer älteren Windows-Version.

Die empfohlene Wartungsaktion zum Verschieben von Geräten aus älteren Versionen von Windows besteht darin, einen Bereitstellungsplan mit [Desktop Analytics](../../desktop-analytics/overview.md) zu erstellen.

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a> Autopilot

Microsoft Autopilot ermöglicht eine einfachere erste Bereitstellung für Windows 10-PCs als die native Bereitstellung durch Reduzierung der Anzahl von Anzeigen bei der Willkommensseite und Bereitstellung von Standardwerten, um sicherzustellen, dass die Bereitstellung auf Mitarbeitergeräten bei neuen Geräten und nach dem Zurücksetzen korrekt funktioniert.

Diese Metrik misst den Prozentsatz der Windows 10-Geräte, die für Autopilot registriert sind.

Die empfohlene Wartungsaktion ist das Registrieren vorhandener Geräte in Autopilot mit [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) bietet Benutzern zahlreiche Produktivitätsvorteile, z. B. das geräteweite einmalige Anmelden bei Apps und Diensten, Anmeldung mit Windows Hello, Self-Service-BitLocker-Wiederherstellung und Datenroaming innerhalb des Unternehmens.

Diese Metrik misst den Prozentsatz der Geräte, die in Azure AD registriert sind.

Ihre von Microsoft Intune verwalteten Geräte sind bereits in Azure AD registriert. Die empfohlene Wartungsaktion für Geräte, die von Configuration Manager verwaltet werden, ist entweder [deren Registrierung in Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) oder [deren gemeinsame Verwaltung](../../comanage/overview.md). Die Co-Verwaltung von Geräten verbessert auch Ihre Cloudverwaltungsbewertung.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a> Cloudverwaltung

Microsoft Intune stellt Benutzern verschiedene Produktivitätsvorteile zur Verfügung, z. B. Zugriff auf Unternehmensressourcen auch außerhalb des Unternehmensnetzwerks. Außerdem sorgt Intune dafür, dass das Tool „Gruppenrichtlinie“ und der entsprechende Leistungsaufwand nicht mehr erforderlich sind, was zu einer optimierten Benutzerfreundlichkeit führt. Diese Metrik misst den Prozentsatz der PCs, die in Microsoft Intune registriert sind. Erfahren Sie, wie [Microsoft dies unseren Mitarbeitern ermöglicht](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

Die empfohlene Wartungsaktion für noch nicht in Intune registrierte Geräte, die von Configuration Manager verwaltet werden, ist deren [gemeinsame Verwaltung](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a> Kein kommerzieller Median

Die integrierte Baseline **Kommerzieller Median** verfügt zurzeit nicht über Metriken für die Teilbewertungen, die in den obigen Abschnitten aufgeführt sind.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a> Startleistung

> [!NOTE]
> Wenn keine Startleistungsdaten von allen Geräten angezeigt werden, finden Sie weitere Informationen im Abschnitt zur [Problembehandlung der Startleistung von registrierten Geräten](#bkmk_uea_enrollment_tshooter).

Die Bewertung der Startleistung unterstützt IT-Mitarbeiter bei Bestrebungen, Benutzern die Zeit vom Einschalten bis zur Produktivität zu verkürzen und lange Start- und Anmeldeverzögerungen zu vermeiden. Die **Startbewertung** ist eine Zahl zwischen 0 und 100. Diese Bewertung ist ein gewichteter Durchschnitt der **Startbewertung** und der **Anmeldungsbewertung**, die wie folgt berechnet werden:

- **Startbewertung**: Basiert auf der Zeit vom Einschalten bis zum Anmelden. Wir betrachten die letzten Startzeiten der einzelnen Geräte, die Updatephase ausgenommen, und bewerten sie dann von 0 (schlecht) bis 100 (außerordentlich). Diese Bewertungen werden gemittelt, um eine Gesamtstartbewertung des Mandanten zu erhalten.
- **Anmeldungsbewertung**: Basiert auf dem Zeitraum zwischen dem Zeitpunkt, an dem die Anmeldeinformationen eingegeben wurden, und dem Zeitpunkt, an dem der Benutzer auf einen reaktionsfähigen Desktop zugreifen kann (dies bedeutet, dass der Desktop gerendert wurde und die CPU-Nutzung mindestens 2 Sekunden lang unter 50 % gesunken ist). Wir betrachten die letzten Anmeldezeiten der einzelnen Geräte, die ersten Anmeldungen oder Anmeldungen unmittelbar nach einem Featureupdate ausgenommen, und bewerten sie dann von 0 (schlecht) bis 100 (außergewöhnlich). Diese Bewertungen werden gemittelt, um eine Gesamtstartbewertung des Mandanten zu erhalten.

[![Startleistungsseite für die Endpunktanalyse](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Einblicke

Die Seite **Startleistung** bietet auch eine priorisierte Liste mit **Erkenntnissen und Empfehlungen**, die in den folgenden Abschnitten beschrieben werden:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a> Festplattenlaufwerke

Die Startleistung bietet Erkenntnisse über die Anzahl der Geräte, deren Startlaufwerk eine Festplatte ist. Die Startzeiten von Festplattenlaufwerken sind in der Regel drei- bis viermal so lang wie die von Solid-State-Laufwerken. Außerdem wird die erwartete Verbesserung der Startleistung beim Wechsel zu Solid-State-Laufwerken berichtet.

Klicken Sie durch, um die Liste der Geräte mit Festplattenlaufwerken anzuzeigen. Als Aktion wird empfohlen, diese Geräte mit Solid-State-Laufwerken upzugraden.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a> Gruppenrichtlinie

Die Startleistung bietet Erkenntnisse über die Anzahl der Geräte, bei denen die Gruppenrichtlinie Start- und Anmeldezeiten verlängert. Wenn Sie durchklicken, gelangen Sie zur Geräteansicht. Die Ansicht ist nach der Gruppenrichtlinienzeit sortiert, sodass Sie betroffene Geräte für die weitere Problembehandlung sehen können.

Wenn Sie auf ein bestimmtes Gerät durchklicken, wird dessen Start- und Anmeldeverlauf angezeigt. Mithilfe des Verlaufs können Sie feststellen, ob eine Regression vorliegt, und wann sie aufgetreten sein könnte.

Es gibt zwar viele Artikel zum Optimieren der Leistung von Gruppenrichtlinien, aber Sie können stattdessen auch die Migration zur Cloudverwaltung auswählen. Die Migration zur Cloudverwaltung erlaubt Ihnen die Verwendung von [Intune-Sicherheitsbaselines](https://docs.microsoft.com/intune/protect/security-baselines) und des demnächst veröffentlichten Richtlinienanalyse-Tools.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a> Lange Start- und Anmeldezeiten

Die Startleistung bietet Erkenntnisse über die Anzahl der Geräte mit langen Start- oder Anmeldezeiten. Die Start- oder Anmeldebewertung „0“ bedeutet „langsam“. Wenn Sie durchklicken, gelangen Sie zur Geräteansicht. Die Geräte sind nach der Kernstartzeit bzw. Kernanmeldezeit sortiert, sodass Sie betroffene Geräte zur weiteren Problembehandlung anzeigen können.

Wenn Sie auf ein bestimmtes Gerät durchklicken, wird dessen Start- und Anmeldeverlauf angezeigt. Mithilfe des Verlaufs können Sie feststellen, ob eine Regression vorlag, und wann sie aufgetreten sein könnte.

### <a name="reporting-tabs"></a>Registerkarten für die Berichterstellung

Die Seite **Startleistung** enthält Registerkarten für die Berichterstellung, die Unterstützung für die Erkenntnisse bieten, wie z. B.:
1. **Modellleistung**. Auf dieser Registerkarte sehen Sie die Leistung für Systemstart und Anmeldung aufgeschlüsselt nach Gerätemodell. Damit können Sie ermitteln, ob Leistungsprobleme auf bestimmte Modelle beschränkt sind.
1. **Geräteleistung**. Diese Registerkarte zeigt Metriken für Systemstart und Anmeldung für all Ihre Geräte. Sie können nach einer bestimmten Metrik sortieren (z. B. nach der Anmeldezeit für Gruppenrichtlinien), um zu ermitteln, welche Geräte die schlechtesten Werte für diese Metrik aufweisen. So erhalten Sie Informationen zu einer möglichen Problembehandlung. Sie können auch anhand des Namens nach einem Gerät suchen. Wenn Sie auf ein Gerät klicken, können Sie den Start- und Anmeldeverlauf anzeigen und so ermitteln, ob vor Kurzem ein Wertrückgang verzeichnet wurde.
1. **Startprozesse**. Startprozesse können sich für Benutzer negativ auf die Dienstqualität auswirken, da sie die Wartezeit erhöhen, bis der Desktop reaktionsfähig wird. Diese Registerkarte (sofern sie angezeigt wird; wir haben einen Flight dieses Features nur für einige Benutzer bereitgestellt, da es sich noch in der Entwicklung befindet) zeigt, welche Prozesse sich auf die Anmeldephase „Zeit bis Desktopreaktion“ in einer Weise auswirken, dass nach dem Rendern des Desktops eine CPU-Auslastung von über 50 % bestehen bleibt. In der Tabelle werden nur Prozesse aufgelistet, die mindestens 10 Geräte in Ihrem Mandanten betreffen.  

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a> Proaktive Korrekturen

Proaktive Korrekturen sind Skriptpakete, die häufige Supportprobleme auf dem Gerät eines Benutzers sogar erkennen und beheben können, bevor er bemerkt, dass ein Problem vorliegt. Diese Korrekturen können dazu beitragen, die Anzahl von Supportanrufen zu verringern. Sie können ein eigenes Skriptpaket erstellen oder eines der Skriptpakete bereitstellen, die wir geschrieben und in unserer Umgebung verwendet haben, um die Zahl der Supporttickets zu verringern.

Jedes Skriptpaket besteht aus einem Erkennungsskript, einem Wiederherstellungsskript und Metadaten. Mithilfe von Intune können Sie diese Skriptpakete bereitstellen und Berichte zu ihrer Effektivität anzeigen. Wir entwickeln aktiv neue Skriptpakete und sind an Ihrem Feedback zur Verwendung dieser Pakete interessiert. Wenn Sie Feedback zu den Skriptpaketen geben möchten, wenden Sie sich an Ihren Ansprechpartner für die Vorschauversion der Endpunktanalyse.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a> Abrufen von Erkennungs- und Wiederherstellungsskripts

1. Kopieren Sie die Skripts aus dem Abschnitt [PowerShell-Skripts](#bkmk_uea_ps_scripts) am Ende dieses Artikels.
    - Skriptdateien, deren Namen mit `det` beginnen, sind Erkennungsskripts. Wiederherstellungsskripts beginnen mit `rem`.
    - Eine Beschreibung der Skripts finden Sie unter [Skriptbeschreibungen](#bkmk_uea_scripts).
1. Speichern Sie jedes Skript unter Verwendung des angegebenen Namens. Der Name wird auch in den Kommentaren im oberen Teil jedes Skripts angezeigt.
    - Sie können einen anderen Skriptnamen verwenden, der dann jedoch nicht mit dem Namen übereinstimmt, der im Abschnitt [Skriptbeschreibungen](#bkmk_uea_scripts) aufgeführt ist.


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a> Bereitstellen und Überwachen von Skripts
Der Dienst **Microsoft Intune-Verwaltungserweiterung** ruft die Skripts aus Intune ab und führt sie aus. Die Skripts werden alle 24 Stunden noch mal ausgeführt. Gehen Sie wie folgt vor, um die Skripts bereitzustellen und zu überwachen:

1. Wechseln Sie in der Konsole zum Knoten **Proaktive Korrekturen**.
1. Klicken Sie auf die Schaltfläche **Skriptpaket erstellen**, um ein Skriptpaket zu erstellen.
     [![Seite der Endpunktanalyse für proaktive Korrekturen Auswählen des Links zum Erstellen.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. Weisen Sie im Schritt **Grundlagen** dem Skriptpaket einen **Namen** und optional eine **Beschreibung** zu. Das Feld **Herausgeber** kann bearbeitet werden, jedoch wird standardmäßig der Name Ihres Mandanten verwendet. **Version** kann nicht bearbeitet werden. 
1. Kopieren Sie im Schritt **Einstellungen** den Text aus den Skripts, die Sie heruntergeladen haben, in die Felder **Erkennungsskript** und **Wiederherstellungsskript**. 
   - Das entsprechende Erkennungs- und Wiederherstellungsskript müssen sich im selben Paket befinden. Beispielsweise entspricht das `Detect_stale_Group_Policies.ps1`-Erkennungsskript dem `Remediate_stale_GroupPolicies.ps1`-Wiederherstellungsskript.
       [![Seite der Endpunktanalyse mit den Einstellungen für das Skript für proaktive Korrekturen](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Beenden Sie die Optionen auf der Seite **Einstellungen** mit den folgenden empfohlenen Konfigurationen:
   - **Dieses Skript mit den Anmeldeinformationen des angemeldeten Benutzers ausführen**: Dies ist vom Skript abhängig. Weitere Informationen finden Sie unter [Skriptbeschreibungen](#bkmk_uea_scripts).
   - **Skriptsignaturprüfung erzwingen:** Nein
   - **Skript in 64-Bit-PowerShell ausführen**: Nein
1. Klicken Sie auf **Weiter**, und weisen Sie dann nach Bedarf **Bereichstags** zu.
1. Wählen Sie im Schritt **Zuweisungen** die Gerätegruppen aus, für die Sie das Skriptpaket bereitstellen möchten.
1. Vervollständigen Sie den Schritt **Bewerten + erstellen** für Ihre Bereitstellung.
1. Unter **Berichterstellung** > **Endpunktanalyse – Proaktive Korrekturen** finden Sie eine Übersicht über den Erkennungs- und Wiederherstellungsstatus.
       [![Übersichtsseite der Endpunktanalyse mit dem Bericht für proaktive Korrekturen](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Klicken Sie auf **Gerätestatus**, um Statusdetails für jedes Gerät in Ihrer Bereitstellung abzurufen.
       [![Endpunktanalyse: proaktive Korrekturen – Gerätestatus](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a> Einstellungen der Endpunktanalyse

Auf der Seite „Einstellungen“ können Sie **Allgemein** oder **Baseline** auswählen. Die einzelnen Einstellungen werden im Folgenden beschrieben:

### <a name="general"></a><a name="bkmk_uea_gen"></a> Allgemein

Auf der Seite **Allgemein** in **Einstellungen** können Sie feststellen, ob die Erfassung der Intune-Startleistungsdaten aktiviert wurde. Sie ist standardmäßig automatisch für alle Ihre Geräte aktiviert, wenn Sie auf **Start** klicken, um die Benutzererlebnisanalyse zu aktivieren. Sie haben die Möglichkeit, zum Datensammlungs-Richtlinienknoten von Intune zu navigieren, um den Satz von Geräten zu ändern, auf denen Start- und Anmeldedatensätze gesammelt werden.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a> Intune-Richtlinie für die Datensammlung

Wenn Sie diese Einstellung für einen Teil der Geräte aktivieren möchten, [erstellen Sie ein Profil](/intune/configuration/device-profile-create#create-the-profile) mit den folgenden Informationen: 

  - **Name:** Geben Sie einen beschreibenden Namen für das Profil ein, z. B. **Intune-Richtlinie für die Datensammlung**.
   
  - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    
  - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
   
  - **Profiltyp**: Wählen Sie **Windows-Integritätsüberwachung** aus.
   
  - Konfigurieren Sie die **Einstellungen**:
   
       - **Systemüberwachung**: Klicken Sie auf **Aktivieren**, um Ereignisinformationen von Windows 10-Geräten zu erfassen.
    
    - **Bereich**: Wählen Sie **Startleistung** aus. 

  - Filtern Sie das Profil mithilfe der [Bereichstags](/intune/configuration/device-profile-create#scope-tags) und [Anwendbarkeitsregeln](/intune/configuration/device-profile-create#applicability-rules) nach bestimmten IT-Gruppen oder Geräten in einer Gruppe, die einem bestimmten Kriterium entsprechen.

> [!NOTE]
> Es gibt einen Platzhalter für Anweisungen, mit denen der Configuration Manager-Datenkonnektor konfiguriert wird. Diese Funktionalität wurde jedoch in dieser ersten privaten Vorschau nicht implementiert.

  [![Endpunktanalyse: Seite mit allgemeinen Einstellungen](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a> Baselineverwaltung

Sie können Ihre aktuellen Bewertungen und Teilbewertungen mit anderen Bewertungen vergleichen, indem Sie eine Baseline festlegen.

1. Es gibt eine integrierte Baseline für den **kommerziellen Median**, mit der Sie Ihre Bewertungen mit einem typischen Unternehmen vergleichen können.
1. Sie können neue Baselines auf Basis Ihrer aktuellen Metriken erstellen, um den Fortschritt nachzuverfolgen oder Regressionen im Laufe der Zeit anzuzeigen. Klicken Sie auf die Schaltfläche **Neu erstellen**, und benennen Sie die neue Baseline. Um die Auswahl in der Dropdownliste auf den Berichtsseiten zu vereinfachen, sollte der Name das Datum enthalten.
1. Es gibt ein Limit von 100 Baselines pro Mandant. Sie können alte Baselines löschen, die nicht mehr benötigt werden.
1. Ihre aktuellen Metriken werden rot gekennzeichnet und als rückläufig angezeigt, wenn sie in ihren Berichten die aktuelle Baseline unterschreiten. Da es völlig normal ist, dass Metriken von Tag zu Tag abweichen, können Sie einen standardmäßigen Regressionsschwellenwert von 10 % festlegen. Mit diesem Schwellenwert werden Metriken nur als rückläufig gekennzeichnet, wenn sie um mehr als 10 % rückläufig sind.

   [![Endpunktanalyse: Seite mit grundlegenden Einstellungen](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a> Problembehandlung

Die folgenden Abschnitte können Ihnen beim Beheben von möglicherweise auftretenden Problemen helfen.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a> Beheben von Problemen bei der Geräteregistrierung der Startleistung

Wenn auf der Übersichtsseite ein Startleistungsscore von 0 zusammen mit einem Banner angezeigt wird, auf dem angegeben ist, dass auf Daten gewartet wird, oder wenn auf der Registerkarte zur Geräteleistung der Startleistung weniger Geräte als erwartet angezeigt werden, helfen Ihnen einige Schritte beim Beheben des Problems.

Hier zunächst eine kurze Zusammenfassung der Einschränkungen bei der Datensammlung für die Startleistung:
1. Auf den Geräten muss Windows 10 Version 1903 oder höher ausgeführt werden.
2. Die Geräte müssen in Azure AD eingebunden sein. Geräte, die dem Arbeitsplatz beigetreten sind, werden derzeit nicht unterstützt, aber wir prüfen aktiv die Möglichkeit, diese Funktionalität zu Windows hinzuzufügen.
3. Auf den Geräten muss die Windows 10 Enterprise-Edition ausgeführt werden. Windows 10 Home und Professional werden derzeit nicht unterstützt, aber wir prüfen aktiv die Möglichkeit, diese Funktionalität zu Windows hinzuzufügen.

Beachten Sie, dass diese Probleme nicht für Daten gelten, die über den neuen Configuration Manager-Connector eingehen. Dieser kann Daten von jedem Configuration Manager-Client-PC sammeln, unabhängig von Version, Edition oder Verzeichniskonfiguration.

Im Folgenden finden Sie nun eine Checkliste zur Problembehandlung:
1. Stellen Sie sicher, dass das Profil der Windows-Integritätsüberwachung alle Geräte als Ziel verwendet, von denen Sie Leistungsdaten sammeln möchten. Auf der Seite mit den Einstellungen der Endpunktanalyse finden Sie einen Link zu diesem Profil. Sie gelangen aber auch wie auf jedes andere Intune-Profil darauf. Stellen Sie über die Registerkarte „Zuweisung“ sicher, dass das Profil den erwarteten Geräten zugewiesen ist. 
1. Prüfen Sie, welche Geräte erfolgreich für die Datensammlung konfiguriert wurden. Diese Information wird Ihnen auch auf der Übersichtsseite des Profils angezeigt.  
   - Ein bekanntes Problem ist, dass manchen Kunden Profilzuweisungsfehler angezeigt werden, wobei die betroffenen Geräte den Fehlercode `-2016281112 (Remediation failed)` anzeigen. Wir sind momentan dabei, dieses Problem zu untersuchen.
1. Geräte, die erfolgreich für die Datensammlung konfiguriert wurden, müssen nach Aktivieren der Datensammlung neu gestartet werden. Anschließend kann es bis zu 24 Stunden dauern, bis das Gerät auf der Registerkarte zur Geräteleistung angezeigt wird.
1. Wenn Ihr Gerät erfolgreich für die Datensammlung konfiguriert und anschließend neu gestartet wurde und nach 24 Stunden immer noch nicht angezeigt wird, kann das Gerät unsere Sammlungsendpunkte möglicherweise nicht erreichen. Dieses Problem kann auftreten, wenn Ihr Unternehmen einen Proxyserver verwendet und die Endpunkte im Proxy nicht aktiviert wurden. Weitere Informationen finden Sie unter [Problembehandlung für Endpunkte](#bkmk_uea_endpoints).

### <a name="data-collection-for-intune-managed-devices"></a>Datensammlung für Geräte, die über Intune verwaltet werden

Endpoint Analytics nutzt die Windows 10- und Windows Server-Komponente „Benutzererfahrung und Telemetrie im verbundenen Modus“ (DiagTrack), um die Daten der Geräte zu erfassen, die über Intune verwaltet werden. Stellen Sie sicher, dass der Dienst **Benutzererfahrung und Telemetrie im verbundenen Modus** auf dem Gerät ausgeführt wird.

#### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a> Endpunkte

Damit Geräte bei der Endpunktanalyse registriert werden können, müssen sie die erforderlichen Funktionsdaten an Microsoft senden. Wenn in Ihrer Umgebung ein Proxyserver verwendet wird, orientieren Sie sich beim Konfigurieren des Proxys an diesen Informationen.

Konfigurieren Sie zum Aktivieren der Freigabe von Funktionsdaten den Proxyserver so, dass die folgenden Endpunkte zulässig sind:

> [!Important]  
> Aus Gründen des Datenschutzes und der Datenintegrität führt Windows bei der Kommunikation mit den erforderlichen Endpunkten zur Freigabe von Funktionsdaten eine Prüfung auf ein Microsoft SSL-Zertifikat (Anheften von Zertifikaten) durch. SSL-Abfangen und -Untersuchung sind somit nicht möglich. Sie müssen diese Endpunkte aus der SSL-Untersuchung ausschließen, um die Endpunktanalyse verwenden zu können.<!-- BUG 4647542 -->

| Endpunkt  | Funktion  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Dieser Endpunkt wird verwendet, um [erforderliche, funktionale Daten](#bkmk_uea_datacollection) an den Endpunkt für die Intune-Datensammlung zu senden. |
| `https://graph.windows.net` | Dieser Endpunkt wird beim Anfügen Ihrer Hierarchie an die Endpunktanalyse (auf der Configuration Manager-Serverrolle) zum automatischen Abrufen von Einstellungen verwendet. Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Dieser Endpunkt wird zum Synchronisieren von Gerätesammlung und Geräten mit der Endpunktanalyse verwendet (nur auf der Configuration Manager-Serverrolle). Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |


#### <a name="proxy-server-authentication"></a>Proxyserverauthentifizierung

Wenn Ihre Organisation die Proxyserverauthentifizierung für den Internetzugriff verwendet, stellen Sie sicher, dass die Daten nicht aufgrund der Authentifizierung blockiert werden. Wenn Ihr Proxy es nicht zulässt, dass Geräte diese Daten senden, werden sie in Desktop Analytics nicht angezeigt.

##### <a name="bypass-recommended"></a>Umgehung (empfohlen)

Konfigurieren Sie die Proxyserver so, dass keine Proxyauthentifizierung für den Datenverkehr zu den Datenfreigabe-Endpunkten erforderlich ist. Diese Option ist die umfassendste Lösung. Sie funktioniert für alle Windows 10-Versionen.  

##### <a name="user-proxy-authentication"></a>Benutzerproxyauthentifizierung

Konfigurieren Sie die Geräte so, dass der Kontext des angemeldeten Benutzers für die Proxyauthentifizierung verwendet wird. Für diese Methode werden die folgenden Konfigurationen benötigt:

- Die Geräte verfügen über das aktuelle Qualitätsupdate für eine unterstützte Version von Windows

- Konfigurieren Sie in der Gruppe „Netzwerk und Internet“ der Windows-Einstellungen in **Proxyeinstellungen** den Proxy auf Benutzerebene (WinINET-Proxy). Sie können auch „Internetoptionen“ in der Legacy-Systemsteuerung verwenden.

- Stellen Sie sicher, dass die Benutzer über die Proxyberechtigung für den Zugriff auf die Datenfreigabe-Endpunkte verfügen. Für diese Option müssen die Geräte über Konsolenbenutzer mit Proxyberechtigungen verfügen; daher können Sie diese Methode nicht auf monitorlosen Geräten verwenden.

> [!IMPORTANT]
> Die Benutzerproxyauthentifizierung ist inkompatibel mit der Verwendung von Microsoft Defender Advanced Threat Protection. Dieses Verhalten ist darauf zurückzuführen, dass bei dieser Authentifizierung der Registrierungsschlüssel **DisableEnterpriseAuthProxy** auf `0` festgelegt ist, während er für Microsoft Defender ATP auf `1` festgelegt sein muss. Weitere Informationen finden Sie unter [Konfigurieren von Computerproxy- und Internetverbindungseinstellungen in Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

##### <a name="device-proxy-authentication"></a>Geräteproxyauthentifizierung

Dieser Ansatz unterstützt folgende Szenarien:

- Monitorlose Geräte, bei denen sich kein Benutzer anmeldet oder die Benutzer des Geräts keinen Internetzugriff haben

- Authentifizierte Proxys, die keine integrierte Windows-Authentifizierung verwenden

- Wenn Sie auch Microsoft Defender Advanced Threat Protection verwenden

Dies ist der Ansatz mit der höchsten Komplexität, da er die folgenden Konfigurationen erfordert:

- Stellen Sie sicher, dass die Geräte über WinHTTP im lokalen Systemkontext auf den Proxyserver zugreifen können. Verwenden Sie zum Konfigurieren dieses Verhaltens eine der folgenden Optionen:

  - Die Befehlszeile `netsh winhttp set proxy`

  - WPAD-Protokoll (Web Proxy Auto-Discovery)

  - Transparenter Proxy

  - Konfigurieren Sie den geräteweiten WinINET-Proxy unter Verwendung der folgenden Gruppenrichtlinieneinstellung: **Erstellen Sie Proxyeinstellungen pro Computer (anstatt pro Benutzer)** (ProxySettingsPerUser = `1`)

  - Geroutete Verbindung, oder Verwendung von Netzwerkadressübersetzung (Network Address Translation, NAT)

- Konfigurieren Sie Proxyserver so, dass den Computerkonten in Active Directory der Zugriff auf die Datenendpunkte ermöglicht wird. Für diese Konfiguration müssen Proxyserver die integrierte Windows-Authentifizierung unterstützen.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a> Häufig gestellte Fragen

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>Werden meine Endpunktanalysedaten migriert, wenn ich meinen Intune-Mandanten an einen anderen Mandantenstandort verschiebe?

Wenn Sie Ihren Intune-Mandanten zu einem anderen Standort migrieren, gehen alle Daten in Ihrer Endpunktanalyselösung zum Zeitpunkt der Migration verloren. Da Endpunkte fortlaufend an die Endpunktanalyse berichten, werden alle Ereignisse, die nach der Migration auftreten, automatisch an Ihren neuen Mandantenstandort hochgeladen, und die Berichte werden wieder neu aufgefüllt, sofern die Geräte weiterhin ordnungsgemäß registriert sind. 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Warum werden die Skripts mit dem Code 1 beendet?

Die Skripts werden mit dem Code 1 beendet, um Intune zu signalisieren, dass eine Wiederherstellung stattfinden sollte. In diesem Fall bedeutet das Beenden eines Erkennungsskripts mit 1, dass eine Wiederherstellung erforderlich ist. Viele Skriptpakete, die ausschließlich im CM ausgeführt werden, können kompatibel sein, werden aber mit dem Code 1 beendet. Bei diesen Skripts ist das Beenden mit dem Code 1 nicht alarmierend, aber Sie können überprüfen, ob das Gerät ordnungsgemäß wiederhergestellt wird.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Warum wurde für das Skript zur Aktualisierung veralteter Gruppenrichtlinien der Fehler 0x87D00321 zurückgegeben?

0x87D00321 ist ein Timeoutfehler bei der Skriptausführung. Dieser Fehler tritt normalerweise bei remote verbundenen Computern auf. Die ausschließliche Bereitstellung für eine dynamische Sammlung von Computern, die über eine interne Netzwerkverbindung verfügen, könnte für Abhilfe sorgen.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a> Skriptbeschreibungen

In dieser Tabelle werden die Skriptnamen, Beschreibungen, Erkennungen, Wiederherstellungen und konfigurierbaren Elemente angezeigt. Skriptdateien, deren Namen mit `Detect` beginnen, sind Erkennungsskripts. Wiederherstellungsskripts beginnen mit `Remediate`. Diese Skripts können aus dem nächsten Abschnitt dieses Artikels kopiert werden.

|Skriptname|Beschreibung|
|---|---|
|**Aktualisieren veralteter Gruppenrichtlinien** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Erkennt, ob die letzte Gruppenrichtlinienaktualisierung mehr als `7 days` zurückliegt.  </br>Passen Sie den 7-Tage-Schwellenwert an, indem Sie den Wert für `$numDays` im Erkennungsskript ändern. </br></br>Wird durch Ausführen von `gpupdate /target:computer /force` und `gpupdate /target:user /force` wiederhergestellt.  </br> </br>Dies kann dazu beitragen, auf die Netzwerkkonnektivität bezogene Supportanrufe zu reduzieren, wenn Zertifikate und Konfigurationen über Gruppenrichtlinien bereitgestellt werden. </br> </br> **Dieses Skript mit den Anmeldeinformationen des angemeldeten Benutzers ausführen**: Ja|
|**Office-Klick-und-Los-Dienst neu starten** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Erkennt, ob der Klick-und-Los-Dienst auf automatischen Start eingestellt ist, und ob der Dienst angehalten wurde. </br> </br> Wiederherstellung durch Einstellung des Diensts auf automatischen Start und Starten des Diensts, wenn er angehalten wurde. </br></br> Hilft bei der Behebung von Problemen, bei denen Win32 Microsoft 365-Apps für Unternehmen nicht gestartet werden, da der Klick-und-Los-Dienst angehalten wurde. </br> </br> **Dieses Skript mit den Anmeldeinformationen des angemeldeten Benutzers ausführen**: Nein|
|**Netzwerkzertifikate überprüfen** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Erkennt, ob von einer Zertifizierungsstelle ausgestellte Zertifikate, die sich entweder im persönlichen Speicher des Computers oder des Benutzers befinden, abgelaufen oder fast abgelaufen sind. </br> Geben Sie die Zertifizierungsstelle an, indem Sie den Wert für `$strMatch` im Erkennungsskript ändern. Geben Sie 0 für `$expiringDays` an, um abgelaufene Zertifikate zu suchen, oder geben Sie eine andere Anzahl von Tagen an, um fast abgelaufene Zertifikate zu finden.  </br></br>Wiederherstellung durch Senden einer Popupbenachrichtigung an den Benutzer. </br> Geben Sie die Werte für `$Title` und `$msgText` mit dem Nachrichtentitel und -text an, den die Benutzer sehen sollen. </br> </br> Unterrichtet Benutzer über abgelaufene Zertifikate, die möglicherweise erneuert werden müssen. </br> </br> **Dieses Skript mit den Anmeldeinformationen des angemeldeten Benutzers ausführen**: Nein|
|**Veraltete Zertifikate löschen** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Erkennt von einer Zertifizierungsstelle ausgestellte abgelaufene Zertifikate im persönlichen Speicher des aktuellen Benutzers. </br> Geben Sie die Zertifizierungsstelle an, indem Sie den Wert für `$certCN` im Erkennungsskript ändern. </br> </br> Wiederherstellung durch Löschen von einer Zertifizierungsstelle ausgestellter abgelaufener Zertifikate im persönlichen Speicher des aktuellen Benutzers. </br> Geben Sie die Zertifizierungsstelle an, indem Sie den Wert für `$certCN` im Wiederherstellungsskript ändern. </br> </br> Sucht und löscht von einer Zertifizierungsstelle ausgestellte abgelaufene Zertifikate im persönlichen Speicher des aktuellen Benutzers. </br> </br> **Dieses Skript mit den Anmeldeinformationen des angemeldeten Benutzers ausführen**: Ja|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a> PowerShell-Skripts

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a> Endpunktanalyse – Datenschutz

### <a name="data-flow"></a>Datenfluss

In der folgenden Abbildung wird der Fluss der erforderlichen Funktionsdaten von einzelnen Geräten über den Datendienst, den vorübergehenden Speicher und zu Ihrem Mandanten veranschaulicht. Daten fließen unabhängig von Windows-Diagnosedaten durch unsere vorhandenen Unternehmenspipelines.

[![Diagramm des Flusses von Benutzererfahrungsdaten](media/dataflow.png)](media/dataflow.png#lightbox)

1. Konfigurieren Sie die **Intune-Datensammlungsrichtlinie** für registrierte Geräte. Diese Richtlinie wird standardmäßig allen Geräten zugewiesen, wenn Sie die Endpunktanalyse **starten**. Allerdings können Sie die [Zuweisung jederzeit ändern](#bkmk_uea_set) und einer Teilmenge von Geräten oder gar keinem Gerät zuweisen.

2. Geräte senden erforderliche Funktionsdaten.

    - Daten werden über die Intune-Verwaltungserweiterung an Intune-Geräte mit der zugewiesenen Richtlinie gesendet. Weitere Informationen finden Sie in den [Anforderungen](#bkmk_uea_prereq).
    - Für Geräte, die vom Configuration Manager verwaltet werden, können Daten auch über den ConfigMgr-Konnektor an die Microsoft Endpoint-Verwaltung übertragen werden. Der ConfigMgr-Konnektor ist der Cloud angefügt. Es ist nur eine Verbindung mit einem Intune-Mandanten erforderlich, ohne die Co-Verwaltung zu aktivieren.

> [!Note]  
> Die Daten, die zum Berechnen der Startbewertung für ein Gerät erforderlich sind, werden während des Startvorgangs generiert. Abhängig von den Energieeinstellungen und dem Benutzerverhalten kann es nach der erfolgreichen Zuweisung einer Richtlinie zu einem Gerät ggf. Wochen dauern, bis das Ergebnis der Startbewertung in der Verwaltungskonsole angezeigt wird.  

3. Der Microsoft Endpoint Manager-Dienst verarbeitet Daten für jedes Gerät und veröffentlicht die Ergebnisse mithilfe von Microsoft Graph-APIs sowohl für einzelne Geräte als auch für Organisationsaggregate in der Verwaltungskonsole.

Die durchschnittliche End-to-End-Wartezeit beträgt ungefähr 12 Stunden und wird von der Zeit, die für die tägliche Verarbeitung benötigt wird, abgegrenzt. Alle anderen Teile des Datenflusses sind nahezu in Echtzeit.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Datensammlung

Derzeit werden mit der Grundfunktion der Endpunktanalyse Informationen gesammelt, die mit Startleistungsdaten im Zusammenhang stehen, die in die [identifizierten](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) und [pseudonymisierten](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data) Kategorien fallen. Wenn im Laufe der Zeit zusätzliche Funktionen hinzugefügt werden, variieren die gesammelten Daten je nach Bedarf. Dies sind die derzeit gesammelten Hauptdatenpunkte:

#### <a name="identified-data"></a>Identifizierte Daten

- Hardwareinventurinformationen
  - **make:** Dies ist der Gerätehersteller.
  - **model:** Dies ist das Gerätemodell.
  - **deviceClass:** Dies ist die Geräteklassifizierung. Beispiel: Desktop, Server oder Mobil
  - **Country:** Dies ist die Einstellung für die Geräteregion.
- Anwendungsbestand, z.B.:
  - **name:** Windows
  - **ver:** Dies beschreibt die aktuelle Betriebssystemversion.
  
#### <a name="pseudonymized-data"></a>Pseudonymisierte Daten

- Diagnose-, Leistungs- und Nutzungsdaten, die an einen Benutzer oder an ein Gerät gebunden sind
  - **logOnId**
  - **bootId:** Dies ist die Systemstart-ID.
  - **coreBootTimeInMilliseconds:** Dies ist die Kernstartzeit.
  - **totalBootTimeInMilliseconds:** Dies ist die gesamte Startzeit.
  - **updateTimeInMilliseconds:** Dies ist die Zeit für den Abschluss von Betriebssystemupdates.
  - **gpLogonDurationInMilliseconds:** Dies ist die Zeit für die Verarbeitung von Gruppenrichtlinien.
  - **desktopShownDurationInMilliseconds:** Dies ist die Zeit für das Laden des Desktops (explorer.exe).
  - **desktopUsableDurationInMilliseconds:** Dies ist die Zeit für die Verwendbarkeit des Desktops (explorer.exe).
  - **topProcesses:** Dies ist die Liste der während des Starts geladenen Prozesse mit Namen, CPU-Nutzungsstatistiken und App-Details (Name, Herausgeber, Version). Beispiel: *{\"ProcessName\":\"svchost\",\"CpuUsage\":43,\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\",\"ProductName\":\"Microsoft&reg; Windows&reg; Operating System\",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*
- Gerätedaten, die nicht an ein Gerät oder einen Benutzer gebunden sind (wenn die Daten an ein Gerät oder an einen Benutzer gebunden sind, behandelt Intune diese als identifizierte Daten)
  - **ID:** Dies ist die eindeutige, von Windows Update verwendete Geräte-ID.
  - **localId:** Hierbei handelt es sich um eine lokal definierte, eindeutige ID für das Gerät. Dies ist nicht der lesbare Gerätename. Sie gleicht höchstwahrscheinlich dem Wert, der unter „HKLM\Software\Microsoft\SQMClient\MachineId“ gespeichert ist.
  - **aaddeviceid:** Azure Active Directory-Geräte-ID
  - **orgId:** Dies ist die eindeutige GUID, die den Microsoft O365-Mandanten darstellt.
  
> [!Important]  
> Unsere Richtlinien zur Datenverarbeitung werden in der [Microsoft Intune Privacy Statement](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement) (Microsoft Intune-Datenschutzerklärung) beschrieben. Wir verwenden Ihre Kundendaten nur, um Ihnen die Dienste zur Verfügung zu stellen, für die Sie sich registriert haben. Wie während des Onboardingprozesses beschrieben wurde, werden die Ergebnisse aller registrierten Organisationen anonymisiert und aggregiert, um die Baseline auf dem neuesten Stand zu halten.


### <a name="resources"></a>Ressourcen

Weitere Informationen zu datenschutzrelevanten Aspekten finden Sie in den folgenden Artikeln:

- [Microsoft Intune Datenschutzbestimmungen](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 und Datenschutzrichtlinien: Ein Leitfaden für IT- und Compliance-Experten](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licensing terms and documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) (Lizenzbedingungen und Dokumentation)  
- [Security and privacy at Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/) (Sicherheit und Datenschutz in Microsoft Azure-Rechenzentren)  
- [Vertrauen Sie Ihrer Cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Trust Center](https://www.microsoft.com/trustcenter)  
