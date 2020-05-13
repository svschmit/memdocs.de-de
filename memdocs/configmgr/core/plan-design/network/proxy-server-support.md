---
title: Proxyserverunterstützung
titleSuffix: Configuration Manager
description: Erfahren Sie, wie für Configuration Manager-Standortsystemserver Proxyserver verwendet werden.
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 89a2f76f394d3bdf8fd6785429ae0ae60302537a
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802088"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Verwenden von Proxyservern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Einige Configuration Manager-Standortsystemserver müssen eine Verbindung mit dem Internet herstellen können. Wenn in Ihrer Umgebung ein Proxyserver für den Internetdatenverkehr erforderlich ist, können Sie für Ihre Standortsystemrollen einen Proxy einrichten.  

- Ein Computer, der einen Standortsystemserver hostet, unterstützt genau eine Proxyserverkonfiguration. Diese wird von allen Standortsystemrollen auf dieser Computerfreigabe verwendet. Wenn Sie unterschiedliche Proxyserver für verschiedene Rollen oder Instanzen einer Rolle benötigen, müssen Sie diese Rollen auf separaten Standortsystemservern platzieren.  

- Wenn Sie neue Proxyservereinstellungen für einen Standortsystemserver konfigurieren, für den es bereits eine Proxyserverkonfiguration gibt, wird die ursprüngliche Konfiguration überschrieben.  

- Für Proxyverbindungen wird standardmäßig das Konto **System** des Computers verwendet, der die Standortsystemrolle hostet.  

- Wenn die Authentifizierung des Computerkontos fehlschlägt, kann der Standortsystemserver Anmeldeinformationen des Benutzers speichern, um damit eine Verbindung zum Proxyserver herzustellen. Diese Anmeldeinformationen entsprechen denen des **Proxyserverkontos des Standortsystems**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Standortsystemrollen, die einen Proxy verwenden

Die folgenden Standortsystemrollen stellen eine Verbindung mit dem Internet her und können ggf. einen Proxyserver verwenden:  

### <a name="asset-intelligence-synchronization-point"></a>Asset Intelligence-Synchronisierungspunkt

Diese Standortsystemrolle stellt eine Verbindung mit Microsoft her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Asset Intelligence-Synchronisierungspunkt gehostet wird.  

### <a name="cloud-distribution-point"></a>Cloudverteilungspunkt

Die Cloudverteilungspunkt-Rolle wird in Microsoft Azure ausgeführt. Für diese Standortsystemrolle wird kein Proxy konfiguriert. Legen Sie die Proxykonfiguration auf dem primären Standortserver fest, der den Cloudverteilungspunkt verwaltet.  

Für diese Konfiguration gilt für den primären Standortserver Folgendes:  

- Er muss in der Lage sein, eine Verbindung mit Microsoft Azure herzustellen, um Inhalte für den Cloudverteilungspunkt einzurichten, zu überwachen und an diesen verteilen.  

- Er verwendet standardmäßig das Konto **System** des Computers, um die Verbindung herzustellen. Er kann bei Bedarf auch das Proxyserverkonto des Standortsystems verwenden.  

- Er verwendet Windows-Webbrowser-APIs.  

### <a name="cloud-management-gateway-connection-point"></a>Verbindungspunkt für das Cloud Management Gateway

Der Verbindungspunkt für das Cloud Management Gateway (CMG) ist eine lokale Rolle, die mit dem CMG-Dienst in Azure kommuniziert. Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="distribution-point"></a>Verteilungspunkt

<!-- 5856396 -->

Ab Version 2002 gilt Folgendes: Wenn Sie einen Configuration Manager-Verteilungspunkt für Microsoft Connected Cache aktivieren, kann dieser über einen nicht authentifizierten Proxyserver für den Internetzugriff kommunizieren. Weitere Informationen finden Sie unter [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

### <a name="exchange-server-connector"></a>Exchange Server-Connector

Diese Standortsystemrolle stellt eine Verbindung mit einem Exchange Server her. Sie greift auf eine Proxyserverkonfiguration auf dem Computer zurück, auf dem der Exchange Server-Connector gehostet wird.  

### <a name="service-connection-point"></a>Dienstverbindungspunkt

Diese Standortsystemrolle stellt eine Verbindung mit dem Configuration Manager-Clouddienst her, um Versionsupdates für Configuration Manager herunterzuladen. Die Standortsystemrolle greift auf einen Proxyserver zurück, der auf dem Computer konfiguriert ist, auf dem der Dienstverbindungspunkt gehostet wird.  

### <a name="software-update-point"></a>Softwareupdatepunkt

Die Standortsystemrolle greift bei einer Verbindung mit Microsoft Update auf den Proxy zurück, um Patches herunterzuladen und Updateinformationen zu synchronisieren. Wie bei allen anderen Standortsystemrollen auch müssen Sie zunächst die Proxyeinstellungen des Standortsystems konfigurieren. Anschließend konfigurieren Sie die folgenden Optionen für den Softwareupdatepunkt:  

- **Verwenden von Proxyserver beim Synchronisieren von Softwareupdates**  

- **Verwenden von Proxyserver beim Herunterladen von Inhalt mit automatischen Bereitstellungsregeln**  

    > [!NOTE]
    > Diese Einstellung ist zwar verfügbar, wird aber nicht von Softwareupdatepunkten an sekundären Standorten verwendet.  

Die Einstellungen finden Sie in den Eigenschaften des Softwareupdatepunkts auf der Registerkarte **Proxy- und Kontoeinstellungen**.  

> [!NOTE]
> Das Konto **System** auf dem Standortserver des Standorts, an dem eine Regel für die automatische Bereitstellung erstellt wurde, wird bei der Ausführung der Regel standardmäßig zum Herstellen der Verbindung mit dem Internet und zum Herunterladen von Softwareupdates verwendet. Alternativ können Sie das Proxyserverkonto des Standortsystems konfigurieren und nutzen. 
>
> Wenn über dieses Konto kein Zugriff auf das Internet möglich ist, werden Softwareupdates nicht heruntergeladen. Der folgende Eintrag wird in der Datei **ruleengine.log** protokolliert:  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a> Weitere Features, die den Proxy für einen Standortsystemserver verwenden

*(Eingeführt in Version 2002)*

Ab Configuration Manager, Version 2002, verwenden die folgenden Features den Proxy des Standortsystemservers, der die Rolle [Dienstverbindungspunkt](#service-connection-point) hostet: <!--5913817-->

- [Azure Active Directory-Benutzerermittlung](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Azure Active Directory-Benutzergruppenermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>Konfigurieren des Proxys für einen Standortsystemserver  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie anschließend auf den Knoten **Server und Standortsystemrollen**.  

2. Wählen Sie den Standortsystemserver aus, den Sie bearbeiten möchten. Klicken Sie im Detailbereich mit der rechten Maustaste zunächst auf die **Standortsystem**-Rolle und anschließend auf **Eigenschaften**.  

3. Wechseln Sie in den Eigenschaften des Standortsystems zur Registerkarte **Proxy**. Konfigurieren Sie die folgenden Proxyeinstellungen:  

    - **Proxyserver beim Synchronisieren von Informationen aus dem Internet verwenden:** Wählen Sie diese Option aus, damit der Standortsystemserver einen Proxyserver verwenden kann.  

    - **Proxyservername:** Geben Sie den Hostnamen oder FQDN des Proxyservers in Ihrer Umgebung an.  

    - **Port:** Geben Sie den Netzwerkport an, der für die Kommunikation mit dem Proxyserver verwendet wird. Standardmäßig wird Port **80** verwendet.  

    - **Anmeldeinformationen zum Verbinden mit dem Proxyserver verwenden:** Für viele Proxyserver wird ein Benutzer zur Authentifizierung benötigt. Standardmäßig verwendet der Standortsystemserver das zugehörige Computerkonto für die Verbindung mit dem Proxyserver. Aktivieren Sie die Option bei Bedarf, indem Sie auf **Festlegen** klicken und ein **Vorhandenes Konto** auswählen oder ein **Neues Konto** angeben. Diese Anmeldeinformationen entsprechen denen des **Proxyserverkontos des Standortsystems**.  Weitere Informationen finden Sie unter [In Configuration Manager verwendete Konten](../hierarchy/accounts.md).  

4. Wählen Sie **OK**, um die neue Proxyserverkonfiguration zu speichern.  

## <a name="next-steps"></a>Nächste Schritte

Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, müssen Sie den Zugriff auf Internetendpunkte zulassen. Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](internet-endpoints.md).
