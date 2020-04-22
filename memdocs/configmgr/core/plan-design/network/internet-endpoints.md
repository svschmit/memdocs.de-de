---
title: Erforderliche Berechtigungen für den Internetzugriff
titleSuffix: Configuration Manager
description: Hier erfahren Sie, welche Internetendpunkten zugelassen werden müssen, um die vollständige Funktionalität der Configuration Manager-Features zu gewährleisten.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2edcff868a684d5e108626b7372241dd1ec47d1c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701528"
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

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"/> Updates und Wartung

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

- `management.azure.com`  

## <a name="co-management"></a>Co-Verwaltung

Wenn Sie Windows 10-Geräte in Microsoft Intune für die Co-Verwaltung registrieren, stellen Sie sicher, dass diese Geräte auf die von Intune benötigten Endpunkte zugreifen können. Weitere Informationen finden Sie unter [Netzwerkendpunkte für Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store für Unternehmen

Wenn Sie Configuration Manager in den [Microsoft Store für Unternehmen](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) integrieren, stellen Sie sicher, dass der Dienstverbindungspunkt und die entsprechenden Geräte auf den Clouddienst zugreifen können. Weitere Informationen finden Sie unter [Proxykonfiguration](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> Clouddienste

<!-- SCCMDocs-pr #3402 -->

In diesem Abschnitt werden folgende Features behandelt:

- Cloudverwaltungsgateway (Cloud Management Gateway, CMG)
- Cloudverteilungspunkt (Cloud Distribution Point, CDP)
- Integration in Azure Active Directory (Azure AD)
- Azure AD-basierte Ermittlung

Für die Bereitstellung von CMG/CDP-Diensten benötigt der **Dienstverbindungspunkt** Zugriff auf Folgendes:

- Abhängig von der Konfiguration können bestimmte Azure-Endpunkte in einzelnen Umgebungen unterschiedlich sein. Configuration Manager speichert diese Endpunkte in der Standortdatenbank. Fragen sie die Tabelle **AzureEnvironments** in SQL Server nach der Liste der Azure-Endpunkte ab.  

Der **CMG-Verbindungspunkt** benötigt Zugriff auf die folgenden Dienstendpunkte:

- Dienstverwaltungsendpunkt: `https://management.core.windows.net/`  

- Speicherendpunkt: `<name>.blob.core.windows.net` und `<name>.table.core.windows.net`

    Hierbei ist `<name>` der Clouddienstname Ihres CMG oder CDP. Wenn Ihr CMG z. B. `GraniteFalls.CloudApp.Net` lautet, ist `GraniteFalls.blob.core.windows.net` der erste Speicherendpunkt, der zugelassen werden muss.<!-- SCCMDocs#2288 -->

Für das Abrufen von Azure AD-Tokens über die **Configuration Manager-Konsole** und den **Client**:

- ActiveDirectoryEndpoint: `https://login.microsoftonline.com/`  

Für die Azure AD-Benutzerermittlung benötigt der **Dienstverbindungspunkt** Zugriff auf Folgendes:

- Version 1810 und früher: Azure AD Graph-Endpunkt: `https://graph.windows.net/`  

- Version 1902 und höher: Microsoft Graph-Endpunkt: `https://graph.microsoft.com/`

Das CMG-Verbindungspunkt-Standortsystem unterstützt die Verwendung eines Webproxys. Weitere Informationen zum Konfigurieren dieser Rolle für einen Proxy finden Sie unter [Proxyserverunterstützung](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Der CMG-Verbindungspunkt muss nur eine Verbindung mit den CMG-Dienstendpunkten herstellen. Zugriff auf andere Azure-Endpunkte ist nicht erforderlich.

Weitere Informationen zum CMG finden Sie unter [Planen von Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).

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

Wenn Sie Configuration Manager zum Bereitstellen und Aktualisieren von Office 365 verwenden, lassen Sie die folgenden Endpunkte zu:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` zum Synchronisieren des Softwareupdatepunkts für Office 365-Clientupdates

- `config.office.com` zum Erstellen benutzerdefinierter Konfigurationen für Office 365-Bereitstellungen

## <a name="configuration-manager-console"></a>Configuration Manager-Konsole

Computer mit Configuration Manager-Konsole erfordern für bestimmte Features Zugriff auf die folgenden Internetendpunkte:

### <a name="in-console-feedback"></a>Konsoleninternes Feedback

- `http://petrol.office.microsoft.com`

Weitere Informationen zu diesem Feature finden Sie unter [Produktfeedback](../../understand/find-help.md#product-feedback).

### <a name="community-workspace-documentation-node"></a>Arbeitsbereich „Community“, Knoten „Dokumentation“

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Weitere Informationen zu diesem Konsolenknoten finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Arbeitsbereich „Überwachung“, Knoten „Standorthierarchie“

Wenn Sie die **geografische Ansicht** verwenden, lassen Sie den Zugriff auf folgenden Endpunkt zu:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Weitere Informationen zu den erforderlichen Endpunkten für den Desktop Analytics-Clouddienst finden Sie unter [Aktivieren der Datenfreigabe](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="microsoft-public-ip-addresses"></a>Öffentliche IP-Adressen von Microsoft

Weitere Informationen zum IP-Adressbereich von Microsoft finden Sie unter [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602) (Öffentlicher IP-Adressraum von Microsoft). Diese Adressen werden regelmäßig aktualisiert. Es gibt keine dienstspezifische Granularität, alle IP-Adressen in diesen Bereichen können verwendet werden.

## <a name="see-also"></a>Weitere Informationen:

- [In Configuration Manager verwendete Ports](../hierarchy/ports.md)

- [Unterstützung von Proxyservern in Configuration Manager](proxy-server-support.md)
