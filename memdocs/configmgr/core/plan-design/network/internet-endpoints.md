---
title: Erforderliche Berechtigungen für den Internetzugriff
titleSuffix: Configuration Manager
description: Hier erfahren Sie, welche Internetendpunkten zugelassen werden müssen, um die vollständige Funktionalität der Configuration Manager-Features zu gewährleisten.
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 986b8d83c705be84b04a89c99d9559471c6345c4
ms.sourcegitcommit: 2c5fd7c8603b88b753765f3cc298d0a0bacaf521
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85819949"
---
# <a name="internet-access-requirements"></a>Erforderliche Berechtigungen für den Internetzugriff

Einige Configuration Manager-Features benötigen für die vollständige Funktionalität eine Internetverbindung. Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, stellen Sie sicher, dass diese Endpunkte zugelassen sind.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> Dienstverbindungspunkt

Diese Konfigurationen gelten für den Computer, der den Dienstverbindungspunkt hostet, sowie für alle Firewalls zwischen diesem Computer und dem Internet. Auf beiden Seiten muss die Kommunikation über den ausgehenden **TCP-Port 443** für HTTPS und den ausgehenden **TCP-Port 80** für HTTP zu den unten genannten Internet-URLs zugelassen sein.

Der Dienstverbindungspunkt unterstützt Webproxys (mit oder ohne Authentifizierung) für die Verwendung dieser URLs. Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](proxy-server-support.md).

Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt](../../servers/deploy/configure/about-the-service-connection-point.md).

Andere Configuration Manager-Features erfordern möglicherweise zusätzliche Endpunkte vom Dienstverbindungspunkt. Weitere Informationen finden Sie in den weiteren Abschnitten dieses Artikels.

> [!TIP]  
> Der Dienstverbindungspunkt verwendet den Microsoft Intune-Dienst beim Herstellen einer Verbindung mit `go.microsoft.com` oder `manage.microsoft.com`. Es ist bekannt, dass beim Intune-Connector Verbindungsprobleme auftreten, wenn das Stammzertifikat „Baltimore CyberTrust“ auf dem Standortverbindungspunkt nicht installiert, abgelaufen oder beschädigt ist. Weitere Informationen finden Sie unter [KB 3187516: Configuration Manager-Dienstverbindungspunkt lädt keine Updates herunter](https://support.microsoft.com/help/3187516).  

Seit Version 2002 gilt Folgendes: Wenn die Verbindung des Configuration Manager-Standorts mit den erforderlichen Endpunkten für einen Clouddienst nicht hergestellt werden kann, wird eine kritische Statusmeldung mit der ID 11488 ausgegeben. Wenn keine Verbindung mit dem Dienst hergestellt werden kann, wird der Status der Komponente „SMS_SERVICE_CONNECTOR“ in „kritisch“ geändert. Zeigen Sie detaillierte Statusinformationen im Knoten [Komponentenstatus](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) in der Configuration Manager-Konsole an.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> Updates und Wartung

Weitere Informationen zu dieser Funktion finden Sie unter [Updates und Wartung für Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Aktivieren Sie diese Endpunkte für die [Management Insights](../../servers/manage/management-insights.md)-Regel **Verbindungsherstellung zwischen Standort und Microsoft-Cloud für Configuration Manager-Updates**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Windows 10-Wartung

Weitere Informationen zu dieser Funktion finden Sie unter [Verwalten von Windows als Dienst](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure-Dienste

Weitere Informationen zu dieser Funktion finden Sie unter [Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com` (öffentliche Azure-Cloud)
- `management.usgovcloudapi.net` (Azure-Cloud für US-Behörden)

## <a name="co-management"></a>Co-Verwaltung

Wenn Sie Windows 10-Geräte in Microsoft Intune für die Co-Verwaltung registrieren, stellen Sie sicher, dass diese Geräte auf die von Intune benötigten Endpunkte zugreifen können. Weitere Informationen finden Sie unter [Netzwerkendpunkte für Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store für Unternehmen

Wenn Sie Configuration Manager in den [Microsoft Store für Unternehmen](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) integrieren, stellen Sie sicher, dass der Dienstverbindungspunkt und die entsprechenden Geräte auf den Clouddienst zugreifen können. Weitere Informationen finden Sie unter [Proxykonfiguration](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="delivery-optimization"></a>Übermittlungsoptimierung

Wenn Sie die Übermittlungsoptimierung verwenden, müssen Clients mit dem Clouddienst kommunizieren: `*.do.dsp.mp.microsoft.com`

Verteilungspunkte, die Microsoft Connected Cache unterstützen, benötigen auch diese Endpunkte.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Häufig gestellte Fragen zur Übermittlungsoptimierung](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Grundlegende Konzepte für die Inhaltsverwaltung in Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Microsoft Connected Cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> Clouddienste

<!-- SCCMDocs-pr #3402 -->

In diesem Abschnitt werden folgende Features behandelt:

- Cloudverwaltungsgateway (Cloud Management Gateway, CMG)
- Cloudverteilungspunkt (Cloud Distribution Point, CDP)
- Integration in Azure Active Directory (Azure AD)
- Azure AD-basierte Ermittlung

Weitere Informationen zum CMG finden Sie unter [Planen von Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).

In den folgenden Abschnitten sind die Endpunkte nach Rolle aufgelistet. Einige Endpunkte verweisen auf einen Dienst anhand von `<name>`. Dies ist der Clouddienstname des CMG oder CDP. Wenn Ihr CMG z. B. `GraniteFalls.CloudApp.Net` heißt, ist der tatsächliche Speicherendpunkt `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>Dienstverbindungspunkt

Für die Bereitstellung von CMG-/CDP-Diensten benötigt der Dienstverbindungspunkt Zugriff auf Folgendes:

- Abhängig von der Konfiguration können bestimmte Azure-Endpunkte in einzelnen Umgebungen unterschiedlich sein. Configuration Manager speichert diese Endpunkte in der Standortdatenbank. Fragen sie die Tabelle **AzureEnvironments** in SQL Server nach der Liste der Azure-Endpunkte ab.

- [Azure-Dienste](#azure-services)

- Für die Azure AD-Benutzerermittlung:

  - Version 1902 und höher: Microsoft Graph-Endpunkt: `https://graph.microsoft.com/`

  - Version 1810 und früher: Azure AD Graph-Endpunkt: `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG-Verbindungspunkt

Der CMG-Verbindungspunkt benötigt Zugriff auf die folgenden Dienstendpunkte:

- Clouddienstname (für CMG oder CDP):
  - `<name>.cloudapp.net` (öffentliche Azure-Cloud)
  - `<name>.usgovcloudapp.net` (Azure-Cloud für US-Behörden)

- Dienstverwaltungsendpunkt: `https://management.core.windows.net/`  

- Speicherendpunkt (für inhaltsfähiges CMG oder CDP):
  - `<name>.blob.core.windows.net` (öffentliche Azure-Cloud)
  - `<name>.blob.core.usgovcloudapi.net` (Azure-Cloud für US-Behörden)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

Das CMG-Verbindungspunktstandortsystem unterstützt die Verwendung eines Web-Proxys. Weitere Informationen zum Konfigurieren dieser Rolle für einen Proxy finden Sie unter [Proxyserverunterstützung](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Der CMG-Verbindungspunkt muss nur eine Verbindung mit den CMG-Dienstendpunkten herstellen. Zugriff auf andere Azure-Endpunkte ist nicht erforderlich.

### <a name="configuration-manager-client"></a>Configuration Manager-Client

- Clouddienstname (für CMG oder CDP):
  - `<name>.cloudapp.net` (öffentliche Azure-Cloud)
  - `<name>.usgovcloudapp.net` (Azure-Cloud für US-Behörden)

- Speicherendpunkt (für inhaltsfähiges CMG oder CDP):
  - `<name>.blob.core.windows.net` (öffentliche Azure-Cloud)
  - `<name>.blob.core.usgovcloudapi.net` (Azure-Cloud für US-Behörden)

- Der Azure AD-Endpunkt für den Abruf von Azure AD-Token:
  - `login.microsoftonline.com` (öffentliche Azure-Cloud)
  - `login.microsoftonline.us` (Azure-Cloud für US-Behörden)

### <a name="configuration-manager-console"></a>Configuration Manager-Konsole

- Der Azure AD-Endpunkt für den Abruf von Azure AD-Token:

  - (öffentliche Azure-Cloud)
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - (Azure-Cloud für US-Behörden)
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a> Softwareupdates

Lassen Sie den Zugriff auf die folgenden Endpunkte durch den aktiven Softwareupdatepunkt zu, sodass WSUS und automatische Updates mit dem Microsoft Update-Clouddienst kommunizieren können:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Weitere Informationen zu Softwareupdates finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Intranetfirewall

In den folgenden Fällen müssen Sie möglicherweise Endpunkte zu einer Firewall hinzufügen, die sich zwischen zwei Standortsystemen befindet:

- Wenn untergeordnete Standorte einen Softwareupdatepunkt aufweisen
- Wenn an einem Standort ein aktiver internetbasierter Remote-Softwareupdatepunkt vorhanden ist

#### <a name="software-update-point-on-the-child-site"></a>Softwareupdatepunkt am untergeordneten Standort

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Verwalten von Office 365

> [!NOTE]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

Wenn Sie Configuration Manager zum Bereitstellen und Aktualisieren von Microsoft 365 Apps for Enterprise verwenden, lassen Sie die folgenden Endpunkte zu:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` zum Synchronisieren des Softwareupdatepunkts für Clientupdates von Microsoft 365 Apps for Enterprise

- `config.office.com` zum Erstellen benutzerdefinierter Konfigurationen für Bereitstellungen von Microsoft 365 Apps for Enterprise

- `contentstorage.osi.office.net` zum Unterstützen der Bereitschaftsbewertung von Office-Add-Ins<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Configuration Manager-Konsole

Computer mit Configuration Manager-Konsole erfordern für bestimmte Features Zugriff auf die folgenden Internetendpunkte:

### <a name="in-console-feedback"></a>Konsoleninternes Feedback

- `http://petrol.office.microsoft.com`

Weitere Informationen zu diesem Feature finden Sie unter [Produktfeedback](../../understand/find-help.md#product-feedback).

### <a name="community-workspace"></a>Arbeitsbereich „Community“

#### <a name="documentation-node"></a>Knoten „Dokumentation“

Weitere Informationen zu diesem Konsolenknoten finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md).

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>Community Hub

Weitere Informationen zu diesem Feature finden Sie unter [Community Hub](../../servers/manage/community-hub.md).

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>Arbeitsbereich „Überwachung“, Knoten „Standorthierarchie“

Wenn Sie die **geografische Ansicht** verwenden, lassen Sie den Zugriff auf folgenden Endpunkt zu:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Weitere Informationen zu den erforderlichen Endpunkten für den Desktop Analytics-Clouddienst finden Sie unter [Aktivieren der Datenfreigabe](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="tenant-attach"></a>Mandantenanfügung

Weitere Informationen zu den erforderlichen Endpunkten für Features zur Mandantenanfügung finden Sie unter [Aktivieren der Mandantenanfügung](../../../tenant-attach/device-sync-actions.md#internet-endpoints).

## <a name="endpoint-analytics"></a>Endpunktanalyse

Weitere Informationen zu den erforderlichen Endpunkten für die Endpunktanalyse finden Sie unter [Proxykonfiguration](../../../../analytics/troubleshoot.md#bkmk_endpoints).

## <a name="microsoft-public-ip-addresses"></a>Öffentliche IP-Adressen von Microsoft

Weitere Informationen zum IP-Adressbereich von Microsoft finden Sie unter [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602) (Öffentlicher IP-Adressraum von Microsoft). Diese Adressen werden regelmäßig aktualisiert. Es gibt keine dienstspezifische Granularität, alle IP-Adressen in diesen Bereichen können verwendet werden.

## <a name="see-also"></a>Weitere Informationen:

- [In Configuration Manager verwendete Ports](../hierarchy/ports.md)

- [Unterstützung von Proxyservern in Configuration Manager](proxy-server-support.md)
