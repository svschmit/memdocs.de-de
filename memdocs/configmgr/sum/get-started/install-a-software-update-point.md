---
title: Installieren und Konfigurieren eines Softwareupdatepunkts
titleSuffix: Configuration Manager
description: Primäre Standorte setzen einen Softwareupdatepunkt am Standort der zentralen Verwaltung voraus, da damit die Bewertung der Konformität von Softwareupdates und die Bereitstellung von Softwareupdates an Clients durchgeführt werden können.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 1f3ab3c108a7f8481aee84b6df5cd41b4b186246
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718840"
---
# <a name="install-and-configure-a-software-update-point"></a>Installieren und Konfigurieren eines Softwareupdatepunkts  

*Gilt für: Configuration Manager (Current Branch)*


> [!IMPORTANT]  
>  Installieren Sie die Standortsystemrolle „Softwareupdatepunkt“ (SUP) erst, nachdem Sie überprüft haben, ob der Server die erforderlichen Abhängigkeiten aufweist, und nachdem Sie die Infrastruktur der Softwareupdatepunkte am Standort bestimmt haben. Weitere Informationen zum Planen von Softwareupdates und zum Bestimmen der Infrastruktur der Softwareupdatepunkte finden Sie unter [Planen von Softwareupdates](../plan-design/plan-for-software-updates.md).  

 Der Softwareupdatepunkt ist am Standort der zentralen Verwaltung und an primären Standorten erforderlich, da andernfalls die Bewertung der Konformität von Softwareupdates und die Bereitstellung von Softwareupdates an Clients nicht möglich wären. An sekundären Standorten ist der Softwareupdatepunkt optional. Die Standortsystemrolle „Softwareupdatepunkt“ muss auf einem Computer erstellt werden, auf dem WSUS installiert ist. Durch die Interaktion mit WSUS werden vom Softwareupdatepunkt die Softwareupdateeinstellungen konfiguriert, und die Synchronisierung von Metadaten für Softwareupdates wird angefordert. Wenn Sie über eine Configuration Manager-Hierarchie verfügen, installieren und konfigurieren Sie den Softwareupdatepunkt zuerst am Standort der zentralen Verwaltung, dann an untergeordneten primären Standorten und schließlich optional an sekundären Standorten. Wenn Sie über einen eigenständigen primären Standort verfügen (nicht über einen Standort der zentralen Verwaltung), installieren und konfigurieren Sie den Softwareupdatepunkt zuerst am primären Standort und dann optional an sekundären Standorten. Einige Einstellungen sind nur verfügbar, wenn Sie den Softwareupdatepunkt an einem Standort der obersten Ebene konfigurieren. Je nachdem, wo Sie den Softwareupdatepunkt installiert haben, müssen Sie unterschiedliche Optionen in Erwägung ziehen.  

> [!IMPORTANT]  
>  Sie können an einem Standort mehrere Softwareupdatepunkte installieren. Der zuerst installierte Softwareupdatepunkt wird als Synchronisierungsquelle konfiguriert. Er dient zur Synchronisierung der Updates von Microsoft Update oder von der Upstreamsynchronisierungsquelle. Die übrigen Softwareupdatepunkte am Standort werden als Replikate des ersten Softwareupdatepunkts konfiguriert. Daher sind einige Einstellungen nach der Installation und Konfiguration des ersten Softwareupdatepunkts nicht verfügbar.  

> [!IMPORTANT]  
>  Die Installation der Standortsystemrolle „Softwareupdatepunkt“ auf einem Server, der als eigenständiger WSUS-Server konfiguriert und verwendet wird, oder die Verwendung eines Softwareupdatepunkts für die direkte Verwaltung von WSUS-Clients wird nicht unterstützt. Vorhandene WSUS-Server werden nur als Upstreamsynchronisierungsquellen für den aktiven Softwareupdatepunkt unterstützt. Siehe [Über eine Upstreamdatenquelle synchronisieren](#BKMK_wsussync).

 Sie können die Standortsystemrolle „Softwareupdatepunkt“ einem vorhandenen Standortsystemserver hinzufügen oder einen neuen erstellen. Je nachdem, ob Sie die Standortsystemrolle einem neuen oder einem vorhandenen Standortserver hinzufügen, wählen Sie im **Assistenten zum Erstellen von Standortsystemservern** oder im **Assistenten zum Hinzufügen von Standortsystemrollen** auf der Seite **Systemrollenauswahl** die Option **Softwareupdatepunkt** aus. Konfigurieren Sie dann die Einstellungen für den Softwareupdatepunkt im Assistenten. Die Einstellungen sind je nach der von Ihnen verwendeten Version von Configuration Manager unterschiedlich. Weitere Informationen zum Installieren einer Standortsystemrolle finden Sie unter [Installieren von Standortsystemrollen](../../core/servers/deploy/configure/install-site-system-roles.md).  

 In den folgenden Abschnitten finden Sie Informationen über die Einstellungen für Softwareupdatepunkte an einem Standort.  

## <a name="proxy-server-settings"></a>Proxyservereinstellungen  
 Je nach verwendeter Configuration Manager-Version können Sie die Proxyservereinstellungen auf unterschiedlichen Seiten des **Assistenten zum Erstellen von Standortsystemservern** oder des **Assistenten zum Hinzufügen von Standortsystemrollen** konfigurieren.  

-   Sie müssen den Proxyserver konfigurieren und dann angeben, wann er für Softwareupdates verwendet werden soll. Konfigurieren Sie die folgenden Einstellungen:  

    -   Konfigurieren Sie die Proxyservereinstellungen im Assistenten auf der Seite **Proxy** oder in Eigenschaften des Standortsystems auf der Registerkarte **Proxy** . Die Proxyservereinstellungen sind standortsystemspezifisch. Dies bedeutet, dass die von Ihnen angegebenen Proxyservereinstellungen von allen Standortsystemrollen verwendet werden.  

    -   Geben Sie an, ob der Proxyserver bei der Synchronisierung der Softwareupdates sowie beim Herunterladen des Inhalts mithilfe einer automatischen Bereitstellungsregel von Configuration Manager verwendet werden soll. Konfigurieren Sie die Einstellungen für den Proxyserver für Softwareupdatepunkte auf der Seite **Proxy- und Kontoeinstellungen** des Assistenten oder auf der Registerkarte **Proxy- und Kontoeinstellungen** in den Eigenschaften für den Softwareupdatepunkt.  

        > [!NOTE]  
        >  Die Einstellung **Proxyserver beim Herunterladen von Inhalt mithilfe der Regeln zur automatischen Bereitstellung verwenden** ist zwar verfügbar, wird aber für einen Softwareupdatepunkt an einem sekundären Standort nicht verwendet. Inhalt wird nur vom Softwareupdatepunkt am Standort der zentralen Verwaltung und an einem eigenständigen primären Standort von Microsoft Update heruntergeladen.  

> [!IMPORTANT]  
>  Das Konto **Lokales System** für den Server, auf dem die automatische Bereitstellungsregel erstellt wurde, wird bei der Ausführung der automatischen Bereitstellungsregeln standardmäßig zum Herstellen der Verbindung mit dem Internet und zum Herunterladen von Softwareupdates verwendet. Wenn dieses Konto nicht auf das Internet zugreifen kann, können keine Softwareupdates heruntergeladen werden. In diesem Fall wird der Datei „ruleengine.log“ der folgende Eintrag hinzugefügt: **Fehler beim Herunterladen des Updates aus dem Internet. Fehler = 12007**. Konfigurieren Sie Anmeldeinformationen für die Verbindung mit dem Proxyserver, wenn der Internetzugriff über das Konto Lokales System nicht möglich ist.  


## <a name="wsus-settings"></a>WSUS-Einstellungen  
 Sie müssen die WSUS-Einstellungen je nach verwendeter Configuration Manager-Version auf verschiedenen Seiten des **Assistenten zum Erstellen von Standortsystemservern** oder des **Assistenten zum Hinzufügen von Standortsystemrollen** konfigurieren. In manchen Fällen kann die Konfiguration auch nur in den Eigenschaften des Softwareupdatepunkts vorgenommen werden, die auch als Eigenschaften der Softwareupdatepunkt-Komponente bezeichnet werden. In den folgenden Abschnitten wird erläutert, wie Sie die WSUS-Einstellungen konfigurieren.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a> WSUS-Porteinstellungen  
 Sie müssen die WSUS-Porteinstellungen im Assistenten auf der Seite Softwareupdatepunkt oder in den Eigenschaften des Softwareupdatepunkts konfigurieren. Führen Sie die folgende Prozedur durch, um die von WSUS verwendeten Porteinstellungen zu bestimmen.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>So bestimmen Sie die Porteinstellungen in IIS  

 1.  Öffnen Sie auf dem WSUS-Server den Internetinformationsdienste-Manager.  

 2.  Erweitern Sie **Sites**, klicken Sie mit der rechten Maustaste auf die Website für den WSUS-Server, und klicken Sie dann auf **Bindungen bearbeiten**. Im Dialogfeld "Sitebindungen" werden die HTTP- und HTTPS-Portwerte in der Spalte **Port** angezeigt.


### <a name="configure-ssl-communications-to-wsus"></a>Konfigurieren der SSL-Kommunikation mit WSUS  
 Sie können die SSL-Kommunikation im Assistenten auf der Seite **Allgemein** oder in den Eigenschaften des Softwareupdatepunkts auf der Registerkarte **Allgemein** konfigurieren.  

 Weitere Informationen zur Verwendung von SSL finden Sie unter [Entscheiden, ob WSUS zur Verwendung von SSL konfiguriert werden soll](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL) und [Konfigurieren eines Softwareupdatepunkts für die Verwendung von TLS/SSL mit einem PKI-Zertifikat](../get-started/software-update-point-ssl.md).  

### <a name="wsus-server-connection-account"></a>Verbindungskonto für WSUS-Server  
 Sie können ein Konto konfigurieren, das beim Herstellen einer Verbindung mit WSUS auf dem Softwareupdatepunkt vom Standortserver verwendet wird. Wenn Sie dieses Konto nicht konfigurieren, wird die Verbindung mit WSUS von Configuration Manager über das Computerkonto für den Standortserver hergestellt. Konfigurieren Sie das Verbindungskonto für WSUS-Server auf der Seite **Proxy- und Kontoeinstellungen** des Assistenten oder auf der Registerkarte **Proxy- und Kontoeinstellungen** in den Eigenschaften für den Softwareupdatepunkt.  Je nachdem, welche Version von Configuration Manager Sie verwenden, können Sie das Konto an unterschiedlichen Stellen im Assistenten konfigurieren.  

 Weitere Informationen über Configuration Manager-Konten finden Sie unter [In Configuration Manager verwendete Konten](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Synchronisierungsquelle  
 Sie können die Upstreamsynchronisierungsquelle für die Synchronisierung von Softwareupdates im Assistenten auf der Seite **Synchronisierungsquelle** oder in „Eigenschaften der Softwareupdatepunktkomponente“ auf der Registerkarte **Synchronisierungseinstellungen** konfigurieren. Die Optionen für die Synchronisierungsquelle variieren je nach Standort.  

 In der folgenden Tabelle finden Sie eine Übersicht über die Optionen, die beim Konfigurieren des Softwareupdatepunkts an einem Standort verfügbar sind.  

|Standort|Verfügbare Optionen für die Synchronisierungsquelle|  
|----------|----------------------------------------------|  
|-   Standort der zentralen Verwaltung<br />-   Eigenständiger primärer Standort|-   Über die Microsoft Update-Website synchronisieren<br />-   Über eine Upstreamdatenquelle synchronisieren<br />-   Nicht über Microsoft Update oder eine Upstreamdatenquelle synchronisieren|  
|-   Zusätzliche Softwareupdatepunkte an einem Standort<br />-   Untergeordneter primärer Standort<br />-   Sekundärer Standort|-   Über eine Upstreamdatenquelle synchronisieren|  

 Die folgende Liste enthält weitere Informationen zu den einzelnen Optionen, die Sie als Synchronisierungsquelle verwenden können:  

-   **Über Microsoft Update synchronisieren**: Verwenden Sie diese Einstellung, um Metadaten für Softwareupdates über Microsoft Update zu synchronisieren. Der Standort der zentralen Verwaltung muss mit dem Internet verbunden sein. Andernfalls kann die Synchronisierung nicht ausgeführt werden. Diese Einstellung ist nur verfügbar, wenn Sie den Softwareupdatepunkt am Standort der obersten Ebene konfigurieren.  

    > [!NOTE]  
    >  Wenn es zwischen dem Softwareupdatepunkt und dem Internet eine Firewall gibt, muss die Firewall möglicherweise zum Akzeptieren der für die WSUS-Website verwendeten HTTP- und HTTPS-Ports konfiguriert werden. Nach Wunsch können Sie den Zugriff auf der Firewall auf bestimmte Domänen einschränken. Weitere Informationen zum Planen einer Firewall, von der Softwareupdates unterstützt werden, finden Sie unter [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **<a name="BKMK_wsussync"></a>Über eine Upstreamdatenquelle synchronisieren**: Verwenden Sie diese Einstellung, um Metadaten für Softwareupdates über die Upstreamsynchronisierungsquelle zu synchronisieren. Die untergeordneten primären und sekundären Standorte werden automatisch zur Verwendung der übergeordneten Standort-URL für diese Einstellung konfiguriert. Sie haben die Möglichkeit, Softwareupdates über einen vorhandenen WSUS-Server zu synchronisieren. Geben Sie eine URL wie `https://WSUSServer:8531` an, wobei 8531 der Port ist, über den die Verbindung mit dem WSUS-Server hergestellt wird.  

-   **Nicht über Microsoft Update oder eine Upstreamdatenquelle synchronisieren**: Verwenden Sie diese Einstellung, um Softwareupdates manuell zu synchronisieren, wenn der Softwareupdatepunkt am Standort der obersten Ebene nicht mit dem Internet verbunden ist. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Wenn es zwischen dem Softwareupdatepunkt und dem Internet eine Firewall gibt, muss die Firewall möglicherweise zum Akzeptieren der für die WSUS-Website verwendeten HTTP- und HTTPS-Ports konfiguriert werden. Nach Wunsch können Sie den Zugriff auf der Firewall auf bestimmte Domänen einschränken. Weitere Informationen zum Planen einer Firewall, von der Softwareupdates unterstützt werden, finden Sie unter [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Sie können im Assistenten auf der Seite **Synchronisierungsquelle** oder in „Eigenschaften der Softwareupdatepunktkomponente“ auf der Registerkarte **Synchronisierungseinstellungen** auch festlegen, ob WSUS-Berichterstattungsereignisse erstellt werden sollen. Da Configuration Manager diese Ereignisse nicht verwendet, wählen Sie in der Regel die Standardeinstellung **Keine WSUS-Berichterstattungsereignisse erstellen**.  

## <a name="synchronization-schedule"></a>Synchronisierungszeitplan  
 Konfigurieren Sie den Synchronisierungszeitplan im Assistenten auf der Seite **Synchronisierungszeitplan** oder in "Eigenschaften der Softwareupdatepunktkomponente". Diese Einstellung wird nur auf dem Softwareupdatepunkt am Standort der obersten Ebene konfiguriert.  

 Wenn Sie den Zeitplan aktivieren, können Sie für die Synchronisierung einen einfachen oder benutzerdefinierten Wiederholungszeitplan konfigurieren. Wenn Sie einen einfachen Zeitplan konfigurieren, basiert die Startzeit auf der zum Zeitpunkt der Zeitplanerstellung geltenden lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird. Die für einen benutzerdefinierten Zeitplan konfigurierte Startzeit basiert auf der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird.  

> [!TIP]  
>  Planen Sie die Ausführung der Softwareupdatesynchronisierung in einem für Ihre Umgebung geeigneten Zeitrahmen. Eine Möglichkeit besteht darin, den Zeitplan so zu konfigurieren, dass die Softwareupdatesynchronisierung kurz nach der Veröffentlichung der Microsoft-Sicherheitsupdates jeweils am zweiten Dienstag eines Monats („Patch-Dienstag“) ausgeführt wird. Eine andere Möglichkeit besteht darin, den Zeitplan so zu konfigurieren, dass die Softwareupdatesynchronisierung täglich ausgeführt wird, wenn Sie mithilfe von Softwareupdates Endpoint Protection-Definitions- und Engine-Updates bereitstellen.  

> [!NOTE]  
>  Wenn Sie die Softwareupdatesynchronisierung nicht nach einem Zeitplan aktivieren, können Sie Softwareupdates im Arbeitsbereich "Softwarebibliothek" über den Knoten **Alle Softwareupdates** oder S **oftwareupdategruppen** manuell synchronisieren. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Ablösungsregeln  
 Konfigurieren Sie die Ablösungseinstellungen im Assistenten auf der Seite **Ablösungsregeln** oder in "Eigenschaften der Softwareupdatepunktkomponente" auf der Registerkarte **Ablösungsregeln** . Sie können die Ablösungsregeln nur am Standort der obersten Ebene konfigurieren. Ab Version 1810 von Configuration Manager können Sie das Verhalten der Ablösungsregeln für **Featureupdates** separat von **anderen Updates** festlegen. <!--3098809, 2977644-->

 Auf dieser Seite können Sie angeben, dass abgelöste Softwareupdates sofort ablaufen sollen. Hierdurch verhindern Sie, dass diese Softwareupdates in neue Bereitstellungen eingeschlossen werden. Zudem wird bei vorhandenen Bereitstellungen durch eine Kennzeichnung darauf hingewiesen, dass die abgelösten Softwareupdates mindestens ein abgelaufenes Softwareupdate enthalten. Sie können auch angeben, dass die abgelösten Softwareupdates erst nach einem bestimmten Zeitraum ablaufen. In diesem Fall können Sie diese Updates weiterhin bereitstellen. Weitere Informationen finden Sie unter [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  Die Seite **Ablösungsregeln** ist im Assistenten nur verfügbar, wenn Sie den ersten Softwareupdatepunkt am Standort konfigurieren. Bei der Installation weiterer Softwareupdatepunkte wird diese Seite nicht angezeigt.  

## <a name="classifications"></a>Klassifizierungen  
 Konfigurieren Sie die Klassifizierungseinstellungen im Assistenten auf der Seite **Klassifizierungen** oder in den „Eigenschaften der Softwareupdatepunktkomponente“ auf der Registerkarte **Klassifizierungen** . Weitere Informationen zu Softwareupdateklassifizierungen finden Sie unter [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  Die Seite **Klassifizierungen** ist im Assistenten nur verfügbar, wenn Sie den ersten Softwareupdatepunkt am Standort konfigurieren. Bei der Installation weiterer Softwareupdatepunkte wird diese Seite nicht angezeigt.  

> [!TIP]  
>  Deaktivieren Sie bei der Erstinstallation des Softwareupdatepunkts am Standort der obersten Ebene alle Klassifizierungen für Softwareupdates. Nach der Erstsynchronisierung der Softwareupdates konfigurieren Sie die Klassifizierungen anhand einer aktualisierten Liste, und initiieren Sie dann die Synchronisierung erneut. Diese Einstellung wird nur auf dem Softwareupdatepunkt am Standort der obersten Ebene konfiguriert.  

## <a name="products"></a>Produkte  
 Konfigurieren Sie die Produkteinstellungen im Assistenten auf der Seite **Produkte** oder in den „Eigenschaften der Softwareupdatepunktkomponente“ auf der Registerkarte **Produkte** .  

> [!NOTE]  
>  Die Seite **Produkte** ist im Assistenten nur verfügbar, wenn Sie den ersten Softwareupdatepunkt am Standort konfigurieren. Bei der Installation weiterer Softwareupdatepunkte wird diese Seite nicht angezeigt.  

> [!TIP]  
>  Deaktivieren Sie bei der Erstinstallation des Softwareupdatepunkts am Standort der obersten Ebene alle Produkte. Nach der Erstsynchronisierung der Softwareupdates konfigurieren Sie die Produkte anhand einer aktualisierten Liste, und initiieren Sie dann die Synchronisierung erneut. Diese Einstellung wird nur auf dem Softwareupdatepunkt am Standort der obersten Ebene konfiguriert.  

## <a name="languages"></a>Sprachen  
 Konfigurieren Sie die Spracheinstellungen im Assistenten auf der Seite **Sprachen** oder in den „Eigenschaften der Softwareupdatepunktkomponente“ auf der Registerkarte **Sprachen** . Geben Sie die Sprachen an, für die Sie Softwareupdatedateien und Übersichtsdetails synchronisieren möchten. Die Einstellung **Softwareupdatedatei** wird auf jedem Softwareupdatepunkt in der Configuration Manager-Hierarchie konfiguriert. Die Einstellung **Übersichtsdetails** wird nur auf dem Softwareupdatepunkt am Standort der obersten Ebene konfiguriert. Weitere Informationen finden Sie unter [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  Die Seite **Sprachen** ist im Assistenten nur verfügbar, wenn Sie den ersten Softwareupdatepunkt am Standort der zentralen Verwaltung installieren. Sie können die Sprachen für die Softwareupdatedatei an untergeordneten Standorten über die Registerkarte **Sprachen** in "Eigenschaften der Softwareupdatepunktkomponente" konfigurieren.  

## <a name="third-party-updates"></a>Updates von Drittanbietern
Ab Configuration Manager Version 1802 können Sie Updates von Drittanbietern für Konfigurations-Manager-Clients aktivieren. Wenn Sie Softwareupdates von Drittanbietern für die SUP-Komponenteneigenschaften aktivieren, wird der SUP das Signaturzertifikat herunterladen, das von WSUS für Updates von Drittanbietern verwendet wird. Diese Option ist während der Installation der Softwareupdatepunkte nicht verfügbar und muss nach der SUP-Installation konfiguriert werden. Informationen zur Aktivierung der Clienteinstellungen für Updates von Drittanbietern finden Sie im Artikel [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates).

## <a name="next-steps"></a>Nächste Schritte
Sie haben den Softwareupdatepunkt ausgehend vom obersten Standort in der Configuration Manager-Hierarchie installiert. Wiederholen Sie die Verfahren in diesem Artikel zum Installieren des Softwareupdatepunkts an untergeordneten Standorten.

Nachdem Sie die Softwareupdatepunkte installiert haben, wechseln Sie zu [Synchronisieren von Softwareupdates](synchronize-software-updates.md).
