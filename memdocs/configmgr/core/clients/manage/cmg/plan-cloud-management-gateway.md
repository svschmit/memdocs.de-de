---
title: Planen des Cloudverwaltungsgateways
titleSuffix: Configuration Manager
description: Planen und Entwerfen des Cloudverwaltungsgateways (Cloud Management Gateway, CMG) zur Vereinfachung der Verwaltung internetbasierter Clients.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d6165678331811f4b04e8b1f540f3dcbb7f015d
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502254"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planen von Cloud Management Gateway in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1101764-->
Das Cloudverwaltungsgateway (Cloud Management Gateway, CMG) bietet eine einfache Möglichkeit zum Verwalten von Configuration Manager-Clients im Internet. Durch die Bereitstellung des CMG als Clouddienst in Microsoft Azure können Sie herkömmliche Clients verwalten, die sich ohne zusätzliche lokale Infrastruktur im Internet bewegen. Zudem müssen Sie Ihre lokale Infrastruktur nicht im Internet verfügbar machen.

> [!NOTE]
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Nachdem die Voraussetzungen geschaffen wurden, müssen für die Erstellung des CMG die folgenden drei Schritte in der Configuration Manager-Konsole ausgeführt werden:

1. Bereitstellen des CMG-Clouddiensts in Azure.
2. Hinzufügen der Rolle des CMG-Verbindungspunkts.
3. Konfigurieren von Standort und Standortrollen für den Dienst.
Nach Abschluss der Bereitstellung und der Konfiguration können Clients über das Intranet oder das Internet nahtlos auf lokale Standortrollen zugreifen.

Dieser Artikel befasst sich mit Grundkenntnissen des CMG, mit der Frage, wie das CMG in Ihre Umgebung passt, und mit der Planung der Implementierung.

## <a name="scenarios"></a>Szenarien

Es gibt verschiedene Szenarios, in denen ein CMG von Vorteil ist. Die folgenden Szenarios zählen zu den häufiger auftretenden Szenarios:  

- Verwalten herkömmlicher Windows-Clients mit einer mit der Active Directory-Domäne verknüpften Identität. Zu diesen Clients zählen Windows 8.1 und Windows 10. In dem Szenario werden PKI-Zertifikate zur Sicherung des Kommunikationskanals verwendet. Zu den Verwaltungsaktivitäten zählen:  

  - Softwareupdates und Endpoint Protection
  - Inventar- und Clientstatus
  - Kompatibilitätseinstellungen
  - Softwareverteilung für das Gerät
  - Tasksequenz für direktes Windows 10-Upgrade

- Verwalten Sie herkömmliche Windows 10-Clients mit moderner Identität, die entweder in eine hybride oder eine reine Clouddomäne eingebunden sind, mit Azure Active Directory (Azure AD). Clients verwenden Azure AD eher für die Authentifizierung als für PKI-Zertifikate. Mit Azure AD ist die Einrichtung, Konfiguration und Verwaltung einfacher als mit komplexeren PKI-Systemen. Verwaltungsaktivitäten entsprechen denen aus dem ersten Szenario. Zusätzlich dazu gibt es folgende Aktivitäten:  

  - Softwareverteilung für den Benutzer  

- Installieren des Configuration Manager-Clients auf Windows 10-Geräten über das Internet. Mit Azure AD kann das Gerät sich beim CMG für die Clientregistrierung und -zuweisung authentifizieren. Sie können den Client manuell installieren oder eine andere Softwareverteilungsmethode verwenden, z.B. Microsoft Intune.  

- Neue Gerätebereitstellung bei Co-Verwaltung. Bei der automatischen Registrierung vorhandener Clients ist CMG für die Co-Verwaltung nicht erforderlich. Erforderlich ist es bei neuen Geräten mit Windows AutoPilot, Azure AD, Microsoft Intune und Configuration Manager. Weitere Informationen finden Sie unter [Pfade zur Co-Verwaltung](../../../../comanage/quickstart-paths.md).

### <a name="specific-use-cases"></a>Spezifische Anwendungsfälle

In diesen Szenarios können folgende Anwendungsfälle für bestimmte Geräte gelten:

- Roaminggeräte wie z.B. Laptops  

- Remote-/Filialengeräte, die kostengünstiger sind und die effizienter über das Internet statt über ein WAN oder VPN verwaltet werden können.  

- Fusionen und Übernahmen, bei denen eine Einbindung von Geräten in Azure AD und eine Verwaltung über ein CMG möglicherweise am einfachsten ist.  

- Arbeitsgruppenclients. Diese Geräte erfordern möglicherweise eine zusätzliche Konfiguration, z. B. Zertifikate.<!-- SCCMDocs#1925 -->

    Ab Version 2002 unterstützt Configuration Manager die tokenbasierte Authentifizierung, die bei der Verwaltung von Remotearbeitsgruppen-Clients helfen kann. Weitere Informationen finden Sie unter [Tokenbasierte Authentifizierung für CMG](../../deploy/deploy-clients-cmg-token.md).

> [!Important]
> Standardmäßig erhalten alle Clients eine Richtlinie für ein CMG und beginnen mit ihrer Verwendung, sobald sie internetbasiert sind. Abhängig von dem Szenario und dem Anwendungsfall, der für Ihre Organisation gilt, müssen Sie die Nutzung des CMG möglicherweise eingrenzen. Weitere Informationen finden Sie unter der Clienteinstellung [Ermöglichen Sie Clients die Verwendung eines Cloudverwaltungsgateways](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

## <a name="topology-design"></a>Topologieentwurf

### <a name="cmg-components"></a>CMG-Komponenten

Die Bereitstellung und der Betrieb des CMG umfassen folgende Komponenten:  

- Der **CMG-Clouddienst** in Azure authentifiziert Clientanforderungen von Configuration Manager und leitet sie an den CMG-Verbindungspunkt weiter.  

- Die Standortsystemrolle **CMG-Verbindungspunkt** ermöglicht eine konsistente Hochleistungsverbindung zwischen dem lokalen Netz und dem CMG-Dienst in Azure. Sie veröffentlicht zudem Einstellungen im Cloudverwaltungsgateway, einschließlich Verbindungsinformationen und Sicherheitseinstellungen. Der CMG-Verbindungspunkt leitet Clientanforderungen entsprechend den URL-Zuordnungen vom CMG zu lokalen Rollen weiter.

- Die Standortsystemrolle [**Serviceverbindungspunkt**](../../../servers/deploy/configure/about-the-service-connection-point.md) führt die Clouddienst-Manager-Komponente aus, die alle CMG-Bereitstellungstasks verarbeitet. Darüber hinaus überwacht die Komponente alle Informationen von Azure AD zu Dienstintegrität und -protokollierung und erstellt entsprechende Berichte. Stellen Sie sicher, dass sich Ihr Dienstverbindungspunkt im [Onlinemodus](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes) befindet.  

- Die Standortsystemrolle **Verwaltungspunkt** wartet Clientanforderungen regulär.

- Die Standortsystemrolle **Softwareupdatepunkt** wartet Clientanforderungen regulär.

    > [!NOTE]
    > Die Größenempfehlungen für Verwaltungspunkte ändern sich nicht abhängig davon, ob sie Anforderungen lokaler oder internetbasierter Clients erfüllen. Weitere Informationen finden Sie unter [Größe und Skalierung von Zahlen](../../../plan-design/configs/size-and-scale-numbers.md#management-point).

- **Internetbasierte Clients** stellen eine Verbindung mit dem CMG her, um auf lokale Configuration Manager-Komponenten Zugriff zu haben.

- Das CMG verwendet einen **zertifikatbasierten HTTPS**-Webdienst für eine sichere Netzwerkkommunikation mit Clients.  

- Internetbasierte Clients verwenden **PKI-Zertifikate oder Azure AD** für Identität und Authentifizierung.  

- Ein [**Cloudverteilungspunkt**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) stellt ggf. Inhalte für internetbasierte Clients bereit.  

  - Ein CMG kann auch als Inhalt für Clients dienen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs. Weitere Informationen finden Sie unter [Ändern eines CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Erstellen Sie das CMG unter Verwendung einer **Azure Resource Manager-Bereitstellung**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) ist eine moderne Plattform zum Verwalten aller Lösungsressourcen als eine einzige Entität, die als [Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) bezeichnet wird. Beim Bereitstellen eines Cloudverwaltungsgateways mit Azure Resource Manager verwendet der Standort Azure Active Directory (Azure AD), um die erforderlichen Cloudressourcen zu authentifizieren und zu erstellen. Für diese modernisierte Bereitstellung ist kein klassisches Azure-Verwaltungszertifikat erforderlich.  

> [!NOTE]
> Mit dieser Funktion wird nicht die Unterstützung für Azure-Clouddienstanbieter (Cloud Service Providers, CSP) aktiviert. Die CMG-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSP nicht unterstützt wird. Weitere Informationen finden Sie unter [verfügbare Azure-Dienste in Azure-CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).

Ab Configuration Manager Version 1902 ist Azure Resource Manager der einzige Mechanismus zur Bereitstellung neuer Instanzen des Cloudverwaltungsgateways. Vorhandene Bereitstellungen funktionieren weiterhin.<!-- 3605704 -->

In Configuration Manager, Version 1810 und früher, bietet der CMG-Assistent weiterhin die Option einer **klassischen Dienstbereitstellung** mit einem Azure-Verwaltungszertifikat. Um die Bereitstellung und Verwaltung von Ressourcen zu vereinfachen, wird das Azure Resource Manager-Bereitstellungsmodell für alle neuen CMG-Instanzen empfohlen. Stellen Sie nach Möglichkeit vorhandene CMG-Instanzen über Resource Manager erneut bereit. Weitere Informationen finden Sie unter [Ändern eines CMG](setup-cloud-management-gateway.md#modify-a-cmg).

> [!IMPORTANT]
> Die klassische Dienstbereitstellungen in Azure ist für die Verwendung in Configuration Manager veraltet. Version 1810 ist die letzte, die das Erstellen dieser Azure-Bereitstellungen unterstützt. Diese Funktionalität wird in einer zukünftigen Version von Configuration Manager entfernt.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Hierarchieentwurf

Erstellen Sie das CMG am Standort der obersten Ebene in Ihrer Hierarchie. Wenn es sich dabei um einen Standort der zentralen Verwaltung handelt, sollten Sie an untergeordneten primären Standorten CMG-Verbindungspunkte erstellen. Die Clouddienst-Manager-Komponente befindet sich am Dienstverbindungspunkt, der sich ebenfalls am Standort der zentralen Verwaltung befindet. Mit diesem Entwurf kann der Dienst ggf. über verschiedene primäre Standorte hinweg geteilt werden.

Sie können mehrere CMG-Dienste in Azure und mehrere CMG-Verbindungspunkte erstellen. Mehrere CMG-Verbindungspunkte bieten einen Lastenausgleich des Clientdatenverkehrs vom CMG zu den lokalen Rollen.

Ab Version 1902 können Sie einer Begrenzungsgruppe ein CMG zuordnen. Mit dieser Konfiguration können Clients für die Clientkommunikation entsprechend der [Begrenzungsgruppenbeziehungen](../../../servers/deploy/configure/boundary-groups.md) den Standardwert für das CMG verwenden oder Fallbacks zum CMG durchführen. Dieses Verhalten ist besonders in Zweigstellen- und VPN-Szenarios nützlich. Sie können für Clientdatenverkehr anstelle von kostspieligen und langsamen WAN-Verknüpfungen die schnelleren Dienste in Microsoft Azure verwenden.<!--3640932-->

> [!NOTE]
> Internetbasierte Clients gehören zu keiner Begrenzungsgruppe.
>
> In Configuration Manager, Version 1810 und früher, gehört das CMG zu keiner Begrenzungsgruppe.

Andere Faktoren, wie z.B. die Anzahl der zu verwaltenden Clients, haben ebenfalls Auswirkungen auf den CMG-Entwurf. Weitere Informationen finden Sie unter [Leistung und Skalierbarkeit](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Beispiel 1: Eigenständiger primärer Standort

Contoso verfügt an seinem Hauptsitz in New York City über einen eigenständigen primären Standort in einem lokalen Datacenter.

- Das Unternehmen erstellt zur Reduzierung der Netzwerklatenz ein CMG in der Azure-Region im Osten der USA.
- Es erstellt zwei CMG-Verbindungspunkte, die beide mit dem CMG-Einzeldienst verknüpft sind.  

Wenn sich Clients im Internet bewegen, kommunizieren sie mit dem CMG in der Azure-Region im Osten der USA. Der CMG leitet diese Kommunikation über beide CMG-Verbindungspunkte weiter.

#### <a name="example-2-hierarchy"></a>Beispiel 2: Hierarchie

Fourth Coffee verfügt an seinem Hauptsitz in Seattle über einen Standort der zentralen Verwaltung in einem lokalen Datacenter. Ein primärer Standort befindet sich in demselben Datacenter, und der andere primäre Standort befindet sich in der europäischen Zentrale in Paris.

- Am Standort der zentralen Verwaltung wird ein CMG-Dienst in der Azure-Region „USA, Westen“ erstellt. Die Anzahl von VMs wird entsprechend der erwarteten Last durch Roamingclients in der gesamten Hierarchie skaliert.
- Am primären Standort in Seattle wird ein CMG-Verbindungspunkt erstellt, der mit dem einzelnen CMG verknüpft ist.
- Am primären Standort in Paris wird ein CMG-Verbindungspunkt erstellt, der mit dem einzelnen CMG verknüpft ist.

Wenn sich Clients im Internet bewegen, kommunizieren sie mit dem CMG in der Azure-Region „USA, Westen“. Das CMG leitet diese Kommunikation an den CMG-Verbindungspunkt am zugewiesenen primären Standort des Clients weiter.

> [!TIP]
> Sie müssen nicht mehr als ein Cloud Management Gateway zum Zwecke der Geolocation bereitstellen. Die geringfügige Latenz, die mit dem Clouddienst auftreten kann, wirkt sich auch bei größerer geografischer Entfernung zumeist nicht auf den Configuration Manager-Client aus.

### <a name="test-environments"></a>Testumgebungen
<!-- SCCMDocs#1225 -->
In vielen Organisationen gibt es getrennte Umgebungen für Produktion, Test, Entwicklung oder Qualitätssicherung. Berücksichtigen Sie beim Planen Ihrer CMG-Bereitstellung die folgenden Fragen:

- Wie viele Azure AD-Mandanten hat Ihre Organisation?
  - Gibt es einen separaten Mandanten für Tests?
  - Befinden sich Benutzer- und Geräteidentitäten im gleichen Mandanten?

- Wie viele Abonnements weist jeder Mandant auf?
  - Gibt es Abonnements spezifisch für Tests?

Der Azure-Dienst von Configuration Manager für die **Cloudverwaltung** unterstützt mehrere Mandanten. Mehrere Configuration Manager-Standorte können eine Verbindung mit dem gleichen Mandanten herstellen. Ein einzelner Standort kann mehrere CMG-Dienste in unterschiedlichen Abonnements bereitstellen. Mehrere Standorte können CMG-Dienste im selben Abonnement bereitstellen. Configuration Manager bietet je nach Ihrer Umgebung und Ihren Geschäftsanforderungen Flexibilität.

Weitere Informationen finden Sie unter den folgenden FAQ: [Müssen sich die Benutzerkonten im gleichen Azure AD-Mandanten befinden wie der Mandant, der mit dem Abonnement verbunden ist, das den CMG-Clouddienst hostet?](cloud-management-gateway-faq.md#bkmk_tenant)

## <a name="requirements"></a>Anforderungen

- Ein **Azure-Abonnement** zum Hosten des CMG.

    > [!IMPORTANT]
    > CMG unterstützt keine Abonnements bei einem Azure-Cloud-Dienstanbieter.<!-- MEMDocs#320 -->

- Sie benötigen ein Benutzerkonto als **Hauptadministrator** oder **Infrastrukturadministrator** in Configuration Manager.<!-- SCCMDocs#2146 -->

- Ein **Azure-Administrator** muss, abhängig von Ihrem Entwurf, an der Ersterstellung bestimmter Komponenten teilnehmen. Diese Persona kann mit dem Configuration Manager-Administrator identisch sein oder auch nicht. Falls nicht, sind keine Berechtigungen in Configuration Manager erforderlich.

  - Ein **Abonnementbesitzer** muss das CMG bereitstellen.
  - Zum Integrieren des Standorts in Azure AD, damit das CMG mithilfe von Azure Resource Manager bereitgestellt werden kann, benötigen Sie einen **globalen Administrator**.

- Mindestens ein lokaler Windows-Server zum Hosten des **CMG-Verbindungspunkts**. Sie können diese Rolle mit anderen Configuration Manager-Standortsystemrollen zusammenstellen.  

- Der **Dienstverbindungspunkt** muss sich im [Onlinemodus](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes) befinden.  

- Zur Bereitstellung des Diensts mit Azure Resource Manager ist die Integration in **Azure AD** erforderlich. Weitere Informationen finden Sie unter [Konfigurieren von Azure-Diensten](../../../servers/deploy/configure/azure-services-wizard.md).  

- Ein [**Serverauthentifizierungszertifikat**](certificates-for-cloud-management-gateway.md#bkmk_serverauth) für das CMG.  

- Abhängig von der Betriebssystemversion Ihres Clients und dem Authentifizierungsmodell sind möglicherweise **weitere Zertifikate** erforderlich. Weitere Informationen finden Sie unter [CMG-Zertifikate](certificates-for-cloud-management-gateway.md).  

    Wenn Sie die Standortoption **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** verwenden, kann der Verwaltungspunkt HTTP sein. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../../../plan-design/hierarchy/enhanced-http.md).

- Wenn Sie die klassische Azure-Bereitstellungsmethode verwenden, benötigen Sie in Configuration Manager, Version 1810 oder früher, ein [**Azure-Verwaltungszertifikat**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt).  

    > [!TIP]  
    > Verwenden Sie das Bereitstellungsmodell **Azure Resource Manager**. Dieses Verwaltungszertifikat ist dafür nicht erforderlich.
    >
    > Die klassische Bereitstellungsmethode ist ab Version 1810 veraltet.  

- Clients müssen **IPv4** verwenden.  

## <a name="specifications"></a>Spezifikationen

- Alle unter [Unterstützte Betriebssysteme für Clients und Geräte](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) aufgeführten Windows-Versionen werden für das CMG unterstützt.  

- Das CMG unterstützt nur die Rollen „Verwaltungspunkt“ und „Softwareupdatepunkt“.  

- Das CMG unterstützt keine Clients, die nur mit IPv6-Adressen kommunizieren.<!--495606-->  

- Softwareupdatepunkte, die ein Netzwerklastenausgleichsmodul verwenden, können nicht mit dem CMG ausgeführt werden. <!--505311-->  

- CMG-Bereitstellungen mit dem Azure Resource Model aktivieren keine Unterstützung für Azure Cloud-Dienstanbieter. Die CMG-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSP nicht unterstützt wird. Weitere Informationen finden Sie unter [Im Azure Cloud Solution Provider (CSP)-Programm verfügbare Azure-Dienste](https://docs.microsoft.com/partner-center/azure-plan-available).

### <a name="support-for-configuration-manager-features"></a>Unterstützung für Configuration Manager-Features

Die folgende Tabelle enthält die CMG-Unterstützung für Configuration Manager-Features:

|Komponente  |Unterstützung  |
|---------|---------|
| Softwareupdates     | ![Unterstützt](media/green_check.png) |
| Endpoint Protection     | ![Unterstützt](media/green_check.png) <sup>[Hinweis 1](#bkmk_note1)</sup> |
| Hardware- und Softwareinventur     | ![Unterstützt](media/green_check.png) |
| Clientstatus und Benachrichtigungen     | ![Unterstützt](media/green_check.png) |
| Skripts ausführen     | ![Unterstützt](media/green_check.png) |
| CMPivot     | ![Unterstützt](media/green_check.png) |
| Kompatibilitätseinstellungen     | ![Unterstützt](media/green_check.png) |
| Clientinstallation<br>(mit [Azure AD-Integration](../../deploy/deploy-clients-cmg-azure.md)) | ![Unterstützt](media/green_check.png) |
| Clientinstallation<br>(mit [Tokenauthentifizierung](../../deploy/deploy-clients-cmg-token.md)) | ![Unterstützt](media/green_check.png) (2002) |
| Softwareverteilung (geräteorientiert)     | ![Unterstützt](media/green_check.png) |
| Softwareverteilung (benutzerorientiert, erforderlich)<br>(mit Azure AD-Integration)     | ![Unterstützt](media/green_check.png) |
| Softwareverteilung (benutzerorientiert, verfügbar)<br>([alle Anforderungen](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Unterstützt](media/green_check.png) |
| [Tasksequenz für direktes Windows 10-Upgrade](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) | ![Unterstützt](media/green_check.png) |
| Tasksequenzen, die keine Startimages verwenden und mit einer Option bereitgestellt werden: **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** | ![Unterstützt](media/green_check.png) |
| Tasksequenzen, die keine Startimages verwenden und über [sämtliche Downloadoptionen](../../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg) verfügbar sind | ![Unterstützt](media/green_check.png) (1910)|
| Alle anderen Tasksequenzszenarios     | ![Nicht unterstützt](media/Red_X.png) |
| Clientpush     | ![Nicht unterstützt](media/Red_X.png) |
| Automatische Standortzuweisung     | ![Nicht unterstützt](media/Red_X.png) |
| Genehmigungsanforderungen für Software     | ![Nicht unterstützt](media/Red_X.png) |
| Configuration Manager-Konsole     | ![Nicht unterstützt](media/Red_X.png) |
| Remotetools     | ![Nicht unterstützt](media/Red_X.png) |
| Berichterstellungswebsite     | ![Nicht unterstützt](media/Red_X.png) |
| Wake-On-LAN     | ![Nicht unterstützt](media/Red_X.png) |
| Mac-, Linux- und UNIX-Clients     | ![Nicht unterstützt](media/Red_X.png) |
| Peercache     | ![Nicht unterstützt](media/Red_X.png) |
| Lokale Verwaltung mobiler Geräte     | ![Nicht unterstützt](media/Red_X.png) |
| BitLocker-Verwaltung     | ![Nicht unterstützt](media/Red_X.png) |

|Key|
|--|
|![Unterstützt](media/green_check.png) = Dieses Feature wird mit dem CMG von allen unterstützten Versionen von Configuration Manager unterstützt  |
|![Unterstützt](media/green_check.png) (*JJMM*) = Dieses Feature wird mit dem CMG ab Version *JJMM* von Configuration Manager unterstützt  |
|![Nicht unterstützt](media/Red_X.png) = Dieses Feature wird nicht mit dem CMG unterstützt |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a> Hinweis 1: Unterstützung für Endpoint Protection
<!-- 4350561 -->
Damit in die Domäne eingebundene Geräte die Endpoint Protection-Richtlinie anwenden können, benötigen sie Zugriff auf die Domäne. Bei Geräten mit seltenem Zugriff auf das interne Netzwerk kann es zu Verzögerungen bei der Anwendung der Endpoint Protection-Richtlinie kommen. Wenn Sie fordern, dass Geräte die Endpoint Protection-Richtlinie sofort nach Erhalt anwenden, ziehen Sie eine der folgenden Optionen in Betracht:

- Verwenden Sie die Co-Verwaltung, und wechseln Sie mit der [Endpoint Protection-Workload](../../../../comanage/workloads.md#endpoint-protection) zu Intune. Dann verwalten Sie [Microsoft Defender Antivirus](https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus) von der Cloud aus.

- Verwenden Sie [Konfigurationselemente](../../../../compliance/deploy-use/create-configuration-items.md) anstelle des nativen Features der [Antischadsoftwarerichtlinien](../../../../protect/deploy-use/endpoint-antimalware-policies.md) zum Anwenden der Endpoint Protection-Richtlinie.

## <a name="cost"></a>Kosten

> [!IMPORTANT]  
> Die nachfolgenden Kosteninformationen stellen lediglich Schätzwerte dar. Ihre Umgebung weist möglicherweise andere Variablen auf, die sich auf die Gesamtkosten für die Verwendung des CMG auswirken.

Das CMG verwendet folgende Azure-Komponenten, durch die Gebühren für das Azure-Abonnementkonto anfallen:

### <a name="virtual-machine"></a>Virtuelle Maschine

- Das CMG verwendet Azure Cloud-Dienste als Platform-as-a-Service (PaaS). Dieser Dienst verwendet virtuelle Computer (Virtual Machines, VM), durch die Computekosten anfallen.  

- CMG verwendet eine A2 Standard V2-VM.  

- Sie wählen aus, von wie vielen VM-Instanzen das CMG unterstützt wird. Der Standardwert ist 1, und 16 ist die Höchstwert. Diese Zahl wird bei der Erstellung des CMG festgelegt und kann nachträglich geändert werden, um den Dienst nach Bedarf zu skalieren.

- Weitere Informationen darüber, wie viele VMs Sie für die Unterstützung Ihrer Clients benötigen, finden Sie unter [Leistung und Skalierung](#performance-and-scale).

- Der [Azure-Preisrechner](https://azure.microsoft.com/pricing/calculator/) hilft Ihnen, die potenziellen Kosten zu ermitteln.

    > [!NOTE]  
    > Die Kosten für virtuelle Computer variieren je nach Region.

### <a name="outbound-data-transfer"></a>Ausgehende Datenübertragungen

- Die aus Azure fließenden Daten (ausgehender Datenverkehr oder Download) bilden die Grundlage für die Gebühren. Alle Datenflüsse in Azure sind kostenlos (eingehender Datenverkehr oder Upload). CMG-Datenflüsse aus Azure umfassen eine Richtlinie für den Client, Clientbenachrichtigungen und vom CMG an den Standort weitergeleitete Clientantworten. Diese Antworten enthalten Inventurberichte, Statusmeldungen und den Kompatibilitätsstatus.  

- Selbst wenn kein Client mit einem CMG kommuniziert, verursacht Kommunikation im Hintergrund Netzwerkdatenverkehr zwischen dem CMG und dem lokalen Standort.  

- Zeigen Sie die **ausgehende Datenübertragungen (GB)** in der Configuration Manager-Konsole an. Weitere Informationen finden Sie unter [Überwachen von Clients auf dem CMG](monitor-clients-cloud-management-gateway.md).  

- Beachten Sie die [Preisübersicht „Bandbreite“ für Azure](https://azure.microsoft.com/pricing/details/bandwidth/), um die potenziellen Kosten zu ermitteln. Die Preise für Datenübertragungen sind gestaffelt. Je größer die Datennutzung ist, desto weniger zahlen Sie pro Gigabyte.  

- Rechnen Sie *als Schätzwert* mit ca. 100 bis 300 MB pro Client und Monat für internetbasierte Clients. Die untere Schätzung ist für eine Standardclientkonfiguration. Die obere Schätzung ist für eine dynamischere Clientkonfiguration. Ihre tatsächliche Datennutzung kann abhängig von der Konfiguration der Clienteinstellungen variieren.  

    > [!NOTE]  
    > Durch das Ausführen weiterer Aktionen, wie z.B. die Bereitstellung von Softwareaktualisierungen oder Anwendungen, erhöht sich die Menge der ausgehenden Datenübertragungen aus Azure.

- Internetbasierte Clients erhalten gebührenfrei Inhalte der Microsoft-Softwareupdates von Windows Update. Verteilen Sie keine Updatepakete mit Inhalten von Microsoft-Updates auf einen Cloudverteilungspunkt. Andernfalls entstehen Kosten für den Speicher und abgehende Daten.  

- Das fälschliche Festlegen der CMG-Option auf **Clientzertifikatsperre überprüfen** kann zusätzlichen Datenverkehr von Clients zum CMG bewirken. Dieser zusätzliche Datenverkehr bringt eine Zunahme der Azure Ausgangsdaten mit sich, wodurch u. U. Ihre Azure-Kosten steigen.<!-- SCCMDocs#1434 --> Weitere Informationen finden Sie unter [Veröffentlichen der Zertifikatsperrungsliste](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

### <a name="content-storage"></a>Inhaltsspeicher

- Internetbasierte Clients erhalten gebührenfrei Inhalte der Microsoft-Softwareupdates von Windows Update. Verteilen Sie keine Updatepakete mit Inhalten von Microsoft-Updates auf einen Cloudverteilungspunkt. Andernfalls entstehen Kosten für den Speicher und abgehende Daten.  

- Bei allen anderen notwendigen Inhalten, z.B. Anwendungen oder Updates von Drittanbietersoftware, müssen die Updatepakete auf einen Cloudverteilungspunkt verteilt werden. Das CMG unterstützt derzeit nur den Cloudverteilungspunkt zum Senden von Inhalten an Clients.
   - Bei der Verwendung eines CMG zum Speichern von Inhalten werden die Inhalte für Updates für Drittanbietersoftware nicht auf Clients heruntergeladen, wenn die [Clienteinstellung](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** aktiviert ist. <!--6598587--> 

- Weitere Informationen finden Sie im Abschnitt „Kosten einer cloudbasierten Verteilung“ unter [Verwenden eines cloudbasierten Verteilungspunkts](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).  

- Ein CMG kann auch als Cloudverteilungspunkt dienen, um Inhalte für Clients bereitzustellen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs. Weitere Informationen finden Sie unter [Ändern eines CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

- CMG verwendet den lokal redundanten Azure-Speicher (LRS). Weitere Informationen finden Sie unter [Lokal redundanter Speicher (LRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

### <a name="other-costs"></a>Sonstige Kosten

- Jeder Clouddienst verfügt über eine dynamische IP-Adresse. Jedes andere CMG verwendet eine neue dynamische IP-Adresse. Durch das Hinzufügen zusätzlicher VMs pro CMG wird die Anzahl dieser Adressen nicht erhöht.  

## <a name="performance-and-scale"></a>Leistung und Skalierbarkeit

Weitere Informationen zur CMG-Skalierbarkeit finden Sie unter [Anpassen und Skalieren von Zahlen](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg).

Mithilfe der folgenden Empfehlungen können Sie die CMG-Leistung verbessern:

- Bei der Verbindung zwischen dem Configuration Manager-Client und dem Cloud Management Gateway wird nicht zwischen Regionen unterschieden. Die Clientkommunikation ist von der Latenztrennung/geografischen Trennung weitgehend unbeeinflusst. Es ist nicht erforderlich, zum Zweck der geografischen Nähe mehrere CMGs bereitzustellen. Stellen Sie das CMG am Standort der obersten Ebene in Ihrer Hierarchie bereit, und fügen Sie Instanzen hinzu, um das System zu skalieren.

- Erstellen Sie für eine Hochverfügbarkeit des Diensts pro Standort ein CMG mit mindestens zwei CMG-Instanzen und zwei CMG-Verbindungspunkten.  

- Skalieren Sie das Cloudverwaltungsgateway, um durch Hinzufügen weiterer VM-Instanzen mehr Clients zu unterstützen. Mit dem Azure-Lastenausgleich werden Clientverbindungen mit dem Dienst gesteuert.  

- Erstellen Sie weitere CMG-Verbindungspunkte, um die Last auf diese aufzuteilen. Das CMG verteilt den Datenverkehr per Roundrobin an die verbundenen CMG-Verbindungspunkte.  

- Wenn das CMG unter hoher Beanspruchung steht und die unterstützte Anzahl der Clients überschritten wurde, werden Anforderungen weiterhin verarbeitet, es können jedoch Verzögerungen auftreten.  

> [!NOTE]
> Während der Configuration Manager im Hinblick auf die Anzahl der Clients für einen CMG-Verbindungspunkt keine harte Grenze aufweist, ist in Windows Server standardmäßig ein Maximalwert von 16.384 für den dynamischen TCP-Portbereich festgelegt. Wenn an einem Configuration Manager-Standort mehr als 16.384 Clients mit einem einzelnen CMG-Verbindungspunkt verwaltet werden, müssen Sie den Windows Server-Grenzwert erhöhen. Alle Clients verwalten einen Kanal für Clientbenachrichtigungen, in dem ein Port für den CMG-Verbindungspunkt offen gehalten wird. Weitere Informationen zur Verwendung des Befehls „netsh“ zur Erhöhung dieses Grenzwerts finden Sie im [Microsoft Support-Artikel 929851](https://support.microsoft.com/help/929851).

## <a name="ports-and-data-flow"></a>Ports und Datenflüsse

Sie müssen keine eingehenden Ports für Ihr lokales Netzwerk öffnen. Der Dienstverbindungspunkt und der CMG-Verbindungspunkt starten sämtliche Kommunikation mit Azure und dem CMG. Diese beiden Standortsystemrollen müssen ausgehende Verbindungen zur Microsoft-Cloud erstellen können. Der Dienstverbindungspunkt sorgt für die Bereitstellung und Überwachung des Diensts in Azure und muss daher im Onlinemodus sein. Der CMG-Verbindungspunkt stellt eine Verbindung mit dem CMG her, um die Kommunikation zwischen dem CMG und lokalen Standortsystemrollen zu verwalten.

Bei dem folgenden Diagramm handelt es sich um einen grundlegenden konzeptuellen Datenfluss für das CMG:

[![CMG-Datenfluss](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. Der Dienstverbindungspunkt stellt über den HTTPS-Port 443 eine Verbindung zu Azure her. Die Authentifizierung erfolgt über Azure AD oder das Azure-Verwaltungszertifikat. Der Dienstverbindungspunkt stellt das CMG in Azure bereit. Das CMG erstellt den HTTPS-Clouddienst mithilfe des Serverauthentifizierungszertifikats.  

2. Der CMG-Verbindungspunkt stellt über TCP-TLS oder HTTPS eine Verbindung mit dem CMG in Azure her. Es hält die Verbindung geöffnet und erstellt den Kanal für die zukünftige bidirektionale Kommunikation.  

3. Der Client stellt über den HTTPS-Port 443 eine Verbindung mit dem CMG her. Die Authentifizierung erfolgt über Azure AD oder das Clientauthentifizierungszertifikat.  

    > [!NOTE]
    > Wenn Sie das CMG so aktivieren, dass Inhalte bereitgestellt oder ein Cloudverteilungspunkt verwendet wird, verbindet sich der Client über den HTTPS-Port 443 direkt mit Azure Blob Storage. Weitere Informationen finden Sie unter [Verwenden eines cloudbasierten Verteilungspunkts](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).<!-- SCCMDocs#2332 -->

4. Das CMG leitet die Clientkommunikation über die bestehende Verbindung an den lokalen CMG-Verbindungspunkt weiter. Sie müssen keine eingehenden Firewall-Ports öffnen.  

5. Der CMG-Verbindungspunkt leitet die Clientkommunikation an den lokalen Verwaltungspunkt und den Softwareupdatepunkt weiter.  

Weitere Informationen zum Hosten von Inhalten in Azure finden Sie unter [Verwenden eines cloudbasierten Verteilungspunkts](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="required-ports"></a>Erforderliche Ports

In dieser Tabelle werden die erforderlichen Netzwerkports und -protokolle aufgeführt. Der *Client* ist das Gerät zum Initiieren der Verbindung. Hierfür ist ein ausgehender Port erforderlich. Der *Server* ist das Gerät zum Akzeptieren der Verbindung. Hierfür ist ein eingehender Port erforderlich.

| Client | Protokoll | Port | Server | Beschreibung |
|--------|----------|------|--------|-------------|
| Dienstverbindungspunkt | HTTPS | 443 | Azure | CMG-Bereitstellung |
| CMG-Verbindungspunkt | TCP-TLS | 10140-10155 | CMG-Dienst | Bevorzugtes Protokoll für die Erstellung des CMG-Kanals <sup>[Hinweis 1](#bkmk_port-note1)</sup> |
| CMG-Verbindungspunkt | HTTPS | 443 | CMG-Dienst | Fallbackprotokoll zur Erstellung eines CMG-Kanals für nur eine VM-Instanz <sup>[Hinweis 2](#bkmk_port-note2)</sup> |
| CMG-Verbindungspunkt | HTTPS | 10124-10139 | CMG-Dienst | Fallbackprotokoll zur Erstellung eines CMG-Kanals für mindestens zwei VM-Instanzen <sup>[Hinweis 3](#bkmk_port-note3)</sup> |
| Client | HTTPS | 443 | CMG | Allgemeine Clientkommunikation |
| Client | HTTPS | 443 | Blobspeicher | Herunterladen von cloudbasiertem Inhalt |
| CMG-Verbindungspunkt | HTTPS oder HTTP | 443 oder 80 | Verwaltungspunkt | Lokaler Datenverkehr, Port hängt von der Konfiguration des Verwaltungspunkts ab |
| CMG-Verbindungspunkt | HTTPS oder HTTP | 443 oder 80 | Softwareupdatepunkt | Lokaler Datenverkehr, Port hängt von der Konfiguration des Softwareupdatepunkts ab |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a> Hinweis 1: TCP-TLS-Ports für CMG-Verbindungspunkt

Der CMG-Verbindungspunkt versucht zunächst, eine langlebige TCP-TLS-Verbindung mit den einzelnen CMG-VM-Instanzen herzustellen. Er stellte eine Verbindung mit der ersten VM-Instanz an Port 10140 her. Die zweite VM-Instanz verwendet Port 10141, bis zur 16. an Port 10155. Eine TCP-TLS-Verbindung erbringt beste Leistung, sie unterstützt jedoch keinen Internetproxy. Wenn der CMG-Verbindungspunkt über TCP-TLS keine Verbindung herstellen kann, greift er auf HTTPS zurück<sup>[Hinweis 2](#bkmk_port-note2)</sup>.

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a> Hinweis 2: CMG-Verbindungspunkt-HTTPS-Ports für eine VM

Wenn der CMG-Verbindungspunkt über TCP-TLS<sup>[Hinweis 1](#bkmk_port-note1)</sup> keine Verbindung zum CMG herstellen kann, stellt er über HTTPS 443 nur für eine VM-Instanz eine Verbindung zum Azure-Netzwerklastenausgleich her.  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a> Hinweis 3: CMG-Verbindungspunkt-HTTPS-Ports für mindestens zwei VMs

Wenn mindestens zwei VM-Instanzen vorhanden sind, verwendet der CMG-Verbindungspunkt für die erste VM-Instanz HTTPS 10124, nicht HTTPS 443. Er stellt an HTTPS-Port 10125 eine Verbindung zur zweiten VM-Instanz her, bis zur 16. an HTTPS-Port 10139.

### <a name="internet-access-requirements"></a>Erforderliche Berechtigungen für den Internetzugriff

Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, müssen Sie den Zugriff auf Internetendpunkte durch den CMG-Verbindungspunkt und den Dienstverbindungspunkt zulassen.

Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../../plan-design/network/internet-endpoints.md#bkmk_cloud).

## <a name="next-steps"></a>Nächste Schritte

- [Zertifikate für Cloud Management Gateway](certificates-for-cloud-management-gateway.md)
- [Sicherheit und Datenschutz für Cloud Management Gateway](security-and-privacy-for-cloud-management-gateway.md)
- [Größe und Skalierungszahlen für das Cloudverwaltungsgateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](cloud-management-gateway-faq.md)
- [Einrichten des Cloudverwaltungsgateways](setup-cloud-management-gateway.md)
