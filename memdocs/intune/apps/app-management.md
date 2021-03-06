---
title: Was ist die Microsoft Intune App-Verwaltung?
titleSuffix: ''
description: Erfahren Sie mehr über die plattformspezifischen Client-App-Verwaltungsfunktionen für Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68336d252cb3d3d3d49cc0c7a32e49e94ba5cdd7
ms.sourcegitcommit: d6cbd1a1c2926064e074e3431471534eb142c905
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012662"
---
# <a name="what-is-microsoft-intune-app-management"></a>Was ist die Microsoft Intune App-Verwaltung?

Als IT-Administrator können Sie mit Microsoft Intune die Client-Apps verwalten, die Mitarbeiter Ihres Unternehmens verwenden. Diese Funktion besteht zusätzlich zur Verwaltung von Geräten und dem Schutz von Daten. Eine der Prioritäten eines Administrators ist es, sicherzustellen, dass die Endbenutzer Zugriff auf die Apps haben, die sie für ihre Arbeit benötigen. Dieses Ziel kann aus verschiedenen Gründen eine große Herausforderung darstellen:
- Es gibt eine Vielzahl von Geräteplattformen und App-Typen.
- Sie müssen möglicherweise Apps auf unternehmenseigenen und auf privaten Geräten verwalten.
- Sie müssen sicherstellen, dass Ihr Netzwerk und Ihre Daten weiterhin geschützt sind.

Darüber hinaus sollten Sie Apps auf Geräten, die nicht bei Intune registriert sind, zuweisen und verwalten.

## <a name="mobile-application-management-mam-basics"></a>Grundlagen der Verwaltung mobiler Anwendungen (Mobile Application Management, MAM)

Die [mobile Anwendungsverwaltung (Mobile Application Management, MAM) von Intune](app-lifecycle.md) bezeichnet die Intune-Verwaltungsfunktionen, mit denen Sie mobile Apps für Ihre Benutzer veröffentlichen, per Push bereitstellen, konfigurieren, schützen, überwachen und aktualisieren.

MAM ermöglicht es Ihnen, die Daten Ihres Unternehmens innerhalb einer Anwendung zu verwalten und zu schützen. Mit **MAM ohne Geräteregistrierung** (MAM-WE) kann eine Geschäfts-, Schul- oder Uni-App, die vertrauliche Daten enthält, auf nahezu jedem [Gerät](app-management.md#app-management-capabilities-by-platform) verwaltet werden, auch auf persönlichen Geräten in **BYOD-Szenarios (Bring Your Own Device)** . Viele Produktivitäts-Apps, wie z. B. die Microsoft Office-Apps, können über Intune MAM verwaltet werden. Weitere Informationen finden Sie in der Liste von in [Microsoft Intune verwalteten Apps](apps-supported-intune-apps.md), die für die Öffentlichkeit verfügbar ist.

Intune MAM unterstützt zwei Konfigurationen:

- **Intune MDM und MAM**: IT-Administratoren können Apps mithilfe von MAM und App-Schutzrichtlinien nur auf Geräten verwalten, die bei der Intune-Verwaltung mobiler Geräte (Mobile Device Management, MDM) registriert sind. Um Apps mit MDM und MAM zu verwalten, sollten Kunden Intune im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) verwenden.
- **MAM ohne Geräteregistrierung**: Mit MAM ohne Geräteregistrierung (MAM without enrollment, MAM-WE) können IT-Administratoren Apps mithilfe von MAM und App-Schutzrichtlinien auf Geräten verwalten, die nicht bei Intune MDM registriert sind. Dies bedeutet, dass Apps über Intune auf Geräten verwaltet werden können, die bei EMM-Drittanbietern registriert sind. Um Apps mit MAM-WE zu verwalten, sollten Kunden Intune im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) verwenden. Darüber hinaus können Apps auf Geräten, die entweder bei EMM-Drittanbietern (Enterprise Mobility Management, EMM) oder überhaupt nicht bei einer MDM registriert sind, von Intune verwaltet werden. Weitere Informationen über BYOD und EMS von Microsoft finden Sie unter [ Technologieentscheidungen zur Ermöglichung von BYOD mit Microsoft Enterprise Mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md).

## <a name="app-management-capabilities-by-platform"></a>App-Verwaltungsfunktionen nach Plattform

Intune bietet eine Reihe von Funktionen, die die Installation der erforderlichen Apps auf den Geräten unterstützen, auf denen sie ausgeführt werden sollen. Die folgende Tabelle enthält eine Zusammenfassung der App-Verwaltungsfunktionen.

| App-Verwaltungsfunktion | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 |
|-------------------------- | -------------------------- | ---------- | ----- | ---------- |
| Hinzufügen und Zuweisen von Apps für Geräte und Benutzer | Ja | Ja | Ja | Ja |
| Zuweisen von Apps für Geräte, die nicht bei Intune registriert sind | Ja | Ja | Nein | Nein |  |
| Steuern des Startverhaltens von Apps mithilfe von App-Konfigurationsrichtlinien | Ja | Ja | Nein | Nein |
| Verwenden von Richtlinien für die Bereitstellung mobiler Apps zum Verlängern abgelaufener Apps | Nein | Ja | Nein | Nein |
| Schützen von Unternehmensdaten in Apps mit App-Schutzrichtlinien | Ja | Ja | Nein | Nein <sup>1</sup> |
| Entfernen ausschließlich von Unternehmensdaten aus einer installierten App (Selektive App-Zurücksetzung) | Ja | Ja | Nein | Ja |
| Überwachen von App-Zuweisungen | Ja | Ja | Ja | Ja |
| Zuweisen und Nachverfolgen von per Volumenlizenz in einem App-Store erworbenen Apps | Nein | Nein | Nein | Ja |
| Obligatorische Installation von Apps auf Geräten (erforderlich) <sup>2</sup> | Ja | Ja | Ja | Ja |
| Optionale Installation auf Geräten über das Unternehmensportal (verfügbare Installation) | Ja <sup>3</sup> | Ja | Ja | Ja |
| Installieren von Verknüpfungen zu Apps im Internet (Weblink) | Ja <sup>4</sup> | Ja | Ja | Ja |
| Interne (branchenspezifische) Apps | Ja | Ja | Ja | Ja |
| Apps aus einem Store | Ja | Ja | Nein | Ja |
| Aktualisierung von Apps | Ja | Ja | Nein | Ja |

<sup>1</sup> Erwägen Sie die Verwendung [Windows Information Protection](../protect/windows-information-protection-configure.md) für den Schutz von Apps auf Geräten mit Windows 10.<br>
<sup>2</sup> Gilt nur für Geräte, die von Intune verwaltet werden.<br>
<sup>3</sup> Intune unterstützt verfügbare Apps aus dem verwalteten Google Play Store auf Android Enterprise-Geräten.<br>
<sup>4</sup> Intune bietet keine Möglichkeit, eine Verknüpfung zu einer App als Weblink auf Standard Android Enterprise-Geräten zu installieren. Jedoch wird die Unterstützung von Weblinks für [dedizierte Android Enterprise-Geräte mit mehreren Apps](../configuration/device-restrictions-android-for-work.md#device-experience) bereitgestellt. 


## <a name="get-started"></a>Erste Schritte

Sie finden die meisten Informationen zu Apps im Workload **Apps**, auf die Sie wie folgt zugreifen können:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
3. Klicken Sie auf **Apps**.

    ![Apps-Workloadbereich](./media/app-management/apps-workload.png)

„Apps-Workload“ bietet Links für den Zugriff auf allgemeine App-Informationen und -Funktionen. 

Im oberen Bereich des Navigationsmenüs für die App-Workload sind häufig verwendete App-Details enthalten:
- **Übersicht:** Wählen Sie diese Option aus, um den Mandantennamen, die MDM-Autorität, den Mandantenstandort, den Kontostatus, den Status der App-Installation und den Status der App-Schutzrichtlinie anzuzeigen.
- **Alle Apps:** Wählen Sie diese Option aus, um eine Liste aller verfügbaren Apps anzuzeigen. Auf dieser Seite können Sie weitere Apps hinzufügen. Außerdem können Sie den Status und die Zuweisung der einzelnen Apps anzeigen. Weitere Informationen finden Sie unter [Hinzufügen von Apps](apps-add.md) und [Zuweisen von Apps](apps-deploy.md).
- **Überwachen von apps**
    - **App-Lizenzen**: Hiermit können Sie per Volumenlizenz erworbene Apps aus App-Stores anzeigen, zuweisen und überwachen. Weitere Informationen finden Sie unter [Per Volumenlizenzprogramm erworbene iOS-Apps (VPP-Apps)](vpp-apps-ios.md) und [Per Volumenlizenz erworbene Apps aus dem Microsoft Store für Unternehmen](windows-store-for-business.md).
    - **Ermittelte Apps**: Zeigen Sie Apps an, die von Intune zugewiesen oder auf einem Gerät installiert wurden. Weitere Informationen finden Sie unter [Von Intune ermittelte Apps](app-discovered-apps.md).
    - **App-Installationsstatus**: Zeigen Sie den Status einer von Ihnen erstellten App-Zuweisung an. Weitere Informationen finden Sie unter [Überwachen von App-Informationen und -Zuweisungen mit Microsoft Intune](apps-monitor.md#device-and-user-status-graphs).
    - **Status des App-Schutzes**: Zeigen Sie den Status einer App-Schutzrichtlinie für einen ausgewählten Benutzer an.
- **Nach Plattform**: Wählen Sie diese Option aus, um die verfügbaren Apps nach Plattform anzuzeigen.
    - Windows
    - iOS
    - macOS
    - Android
- **Richtlinie:**
    - **App-Schutzrichtlinien**: Wählen Sie diese Option aus, um einer App Einstellungen zuzuweisen und so die Unternehmensdaten zu schützen, die diese App verwendet. Sie können z.B. die Funktionen einer App zur Kommunikation mit anderen Apps einschränken oder erzwingen, dass der Benutzer eine PIN eingeben muss, um auf eine Unternehmens-App zuzugreifen. Weitere Informationen finden Sie unter [App-Schutzrichtlinien](app-protection-policies.md).
    - **App-Konfigurationsrichtlinien**: Wählen Sie diese Option aus, um Einstellungen anzugeben, die beim Ausführen einer App durch einen Benutzer möglicherweise erforderlich sind. Weitere Informationen finden Sie unter [App-Konfigurationsrichtlinien](app-configuration-policies-use-ios.md), [Richtlinien zur Konfiguration von iOS-Apps](app-configuration-policies-use-ios.md) und [Richtlinien zur Konfiguration von Android-Apps](app-configuration-policies-overview.md).
    - **iOS-App-Bereitstellungsprofile**: iOS-Apps enthalten ein Bereitstellungsprofil und Code, der von einem Zertifikat signiert ist. Wenn das Zertifikat abläuft, kann die App nicht mehr ausgeführt werden. Intune stellt Ihnen die Tools zum proaktiven Zuweisen einer neuen Richtlinie für Bereitstellungsprofile auf Geräten zur Verfügung, auf denen Apps installiert sind, die bald ablaufen. Weitere Informationen finden Sie unter [iOS-App-Bereitstellungsprofile](app-provisioning-profile-ios.md).
    - **Zusätzliche Richtlinien für S-Modus**: Wählen Sie diese Option aus, um zusätzliche Anwendungen für die Ausführung auf Ihren verwalteten S-Modus-Geräten zu autorisieren. Weitere Informationen finden Sie unter [Zusätzliche Richtlinien für S-Modus](apps-win32-s-mode.md).
    - **Richtlinien für Office-Apps**: Wählen Sie diese Option aus, um Verwaltungsrichtlinien für mobile Office-Apps zu erstellen, die eine Verbindung mit Microsoft 365-Diensten herstellen. Außerdem können Sie den Zugriff auf lokale Exchange-Postfächer schützen, indem Sie Intune-App-Schutzrichtlinien für Outlook für iOS/iPadOS und Android erstellen, die mit hybrider moderner Authentifizierung aktiviert wurden. Sie müssen die Voraussetzungen für die Verwendung von Richtlinien für Office-Apps erfüllen. Weitere Informationen zu den Voraussetzungen finden Sie unter [Voraussetzungen für die Verwendung des Office-Cloudrichtliniendiensts](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service). App-Schutzrichtlinien werden nicht für andere Apps unterstützt, die eine Verbindung mit lokalen Exchange- oder SharePoint-Diensten herstellen. Verwandte Informationen finden Sie unter [Übersicht über den Office-Cloudrichtliniendienst für Microsoft 365-Apps für Unternehmen](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).
    - **Richtliniensätze**: Wählen Sie diese Option aus, um eine zuweisbare Sammlung von Apps, Richtlinien und anderen von Ihnen definierten Verwaltungsobjekten zu erstellen. Weitere Informationen finden Sie unter [Richtliniensätze](../fundamentals/policy-sets.md).
- **Sonstige**:   
    - **Selektive App-Zurücksetzung**: Wählen Sie diese Option aus, um nur Unternehmensdaten vom Gerät eines ausgewählten Benutzers zu entfernen. Weitere Informationen finden Sie unter [Selektive App-Zurücksetzung](apps-selective-wipe.md).
    - **App-Kategorien**: Hiermit können Sie App-Kategorienamen hinzufügen, anheften und löschen.
    - **E-Books**: Einige App-Stores bieten die Möglichkeit, mehrere Lizenzen für Apps oder Bücher zu erwerben, die in Ihrem Unternehmen verwendet werden sollen. Weitere Informationen finden Sie unter [Verwalten von per Volumenlizenz erworbenen Apps und Büchern mit Microsoft Intune](vpp-apps.md).
- **Hilfe und Support**: Hiermit können Sie Probleme behandeln, Unterstützung anfordern oder den Intune-Status anzeigen. Weitere Informationen finden Sie unter [Problembehandlung](../fundamentals/help-desk-operators.md).

### <a name="try-the-interactive-guide"></a>Interaktiven Leitfaden testen
Der interaktive Leitfaden [Verwalten und Schützen von mobilen Anwendungen und Desktopanwendungen mit dem Microsoft Endpoint Manager](https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager) führt Sie Schritt für Schritt durch das Microsoft Endpoint Manager-Admin Center, um Ihnen zu zeigen, wie Sie in Intune registrierte Geräte verwalten, die Konformität mit Richtlinien erzwingen und die Daten Ihrer Organisation schützen.</br></br>

<div align=”center”>
<iframe allowfullscreen width="95%" height="450" src="https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager" frameborder="0" scrolling="no" loading="lazy"/></iframe>
</div>

## <a name="additional-information"></a>Zusätzliche Informationen
Die folgenden Konsolenelemente stellen App-bezogene Funktionen bereit:
- **Microsoft Store für Unternehmen**: Richten Sie die Integration in den Microsoft Store für Unternehmen ein. Anschließend können Sie erworbene Anwendungen mit Intune synchronisieren, sie zuweisen und Ihre Lizenznutzung verfolgen. Weitere Informationen finden Sie unter [Per Volumenlizenz erworbene Apps aus dem Microsoft Store für Unternehmen](windows-store-for-business.md).
- **Windows Enterprise-Zertifikat**: Hiermit können Sie den Status eines codesignierenden Zertifikats anwenden oder anzeigen, das zur Verteilung von branchenspezifischen Apps an Ihre verwalteten Windows-Geräte verwendet wird.
- **Windows-Symantec-Zertifikat**: Anwenden oder Anzeigen des Status eines codesignierenden Symantec-Zertifikats.
- **Windows-Schlüssel zum Querladen**: Fügen Sie einen Windows-Schlüssel zum Querladen hinzu, mit dem Sie eine App direkt auf Geräten installieren können, anstatt die App im Microsoft Store zu veröffentlichen und aus diesem herunterzuladen. Weitere Informationen finden Sie unter [Querladen einer Windows-App](app-sideload-windows.md).
- **Apple-VPP-Tokens**: Hiermit können Sie Ihre iOS-/iPadOS-VPP-Lizenzen (Volume Purchase Program) anzeigen und anwenden. Weitere Informationen finden Sie unter [How to manage iOS and macOS apps purchased through Apple Volume Purchase Program with Microsoft Intune (Verwalten von iOS- und macOS-Apps, die über das Apple Volume Purchase Program mit Microsoft Intune erworben wurden)](vpp-apps-ios.md).
- **Verwaltetes Google Play**: Verwaltetes Google Play ist der Enterprise App Store von Google und die einzige Quelle von Anwendungen für Android Enterprise. Weitere Informationen finden Sie unter [Hinzufügen von verwalteten Google Play-Apps für Android Enterprise-Geräte mit Intune](apps-add-android-for-work.md).
- **Anpassung**: Passen Sie das Unternehmensportal mit Ihrem Unternehmensbranding an. Weitere Informationen finden Sie unter [How to configure the Microsoft Intune Company Portal app (Konfigurieren der Microsoft Intune-Unternehmensportal-App)](company-portal-app.md).

Weitere Informationen zu Apps finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](../apps/apps-add.md).

## <a name="next-steps"></a>Nächste Schritte

- [So fügen Sie eine App zu Microsoft Intune hinzu](apps-add.md)
