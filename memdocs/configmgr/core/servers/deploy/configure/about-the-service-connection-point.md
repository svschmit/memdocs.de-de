---
title: Dienstverbindungspunkt
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über diese Standortsystemrolle von Configuration Manager, und verstehen und planen Sie den Verwendungsbereich.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704948"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Informationen zum Dienstverbindungspunkt in System Center Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Der Dienstverbindungspunkt ist eine Standortsystemrolle, die mehrere wichtige Funktionen für die Hierarchie bereitstellt. Bevor Sie den Dienstverbindungspunkt einrichten, sollten Sie dessen Anwendungsbereiche kennen und entsprechend planen. Die Planung der Verwendung kann sich auf das Einrichten dieser Standortsystemrolle auswirken:

- Laden Sie Updates für Ihre Configuration Manager-Infrastruktur herunter. Auf Grundlage der von Ihnen hochgeladenen Nutzungsdaten werden nur Updates verfügbar gemacht, die für Ihre Infrastruktur relevant sind.

- Laden Sie über Ihre Configuration Manager-Infrastruktur Nutzungsdaten hoch. Sie können die Ebene oder die Menge von Daten steuern, die Sie hochladen. Weitere Informationen finden Sie unter [Ebenen und Einstellungen für Nutzungsdaten](../install/setup-reference.md#bkmk_usage).

- Stellen Sie eine [Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md)-Instanz in Azure bereit.

- Synchronisieren Sie Apps aus dem [Microsoft Store für Unternehmen und Bildungseinrichtungen](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

- Entdecken Sie Benutzer und Gruppen in [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc)

- Verwenden Sie [Desktop Analytics](../../../../desktop-analytics/overview.md), um Erkenntnisse zur Updatebereitschaft und der App-Vorbereitung für Windows 10 zu erhalten.

Jede Hierarchie unterstützt eine einzelne Instanz dieser Rolle. Diese kann nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Dabei handelt es sich um einen Standort der zentralen Verwaltung oder einen eigenständigen primären Standort. Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, deinstallieren Sie diese Rolle am primären Standort, und installieren Sie sie anschließend am Standort der zentralen Verwaltung.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a> Betriebsmodi

Der Dienstverbindungspunkt unterstützt zwei Betriebsmodi:

- **Online:** Der Dienstverbindungspunkt sucht automatisch alle 24 Stunden nach Updates. Neue Updates, die für Ihre aktuelle Infrastruktur und Produktversion verfügbar sind, werden heruntergeladen und in der Configuration Manager-Konsole bereitgestellt.

- **Offline**: Der Dienstverbindungspunkt stellt keine Verbindung mit dem Microsoft-Clouddienst her. Verwenden Sie zum manuellen Importieren verfügbarer Updates das [Dienstverbindungstool](../../manage/use-the-service-connection-tool.md).

### <a name="change-mode"></a>Ändern des Modus

Falls Sie nach der Installation des Dienstverbindungspunkts zwischen dem Online- und Offlinemodus wechseln möchten, müssen Sie den Thread **SMS_DMP_DOWNLOADER** des SMS_Executive-Diensts erneut starten. Wenn Sie diesen Thread neu starten, wird die Änderung übernommen. Sie können diesen Thread mithilfe des Dienst-Managers für Configuration Manager neu starten.

> [!TIP]
> Sie können auch den SMS_Executive-Dienst für Configuration Manager neu starten, wodurch die meisten Standortkomponenten neu gestartet werden. Alternativ haben Sie die Möglichkeit, auf einen geplanten Task wie eine Standortsicherung zu warten, die den SMS_Executive-Dienst beendet und dann für Sie neu startet.

Gehen Sie wie folgt vor, um den Dienst-Manager für Configuration Manager für den Neustart des Threads SMS_DMP_DOWNLOADER zu verwenden:

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie den **Systemstatus**, und wählen Sie den Knoten **Komponentenstatus** aus. Klicken Sie im Menüband auf **Starten**, und wählen Sie anschließend **Dienst-Manager für Configuration Manager** aus.

1. Erweitern Sie im Navigationsbereich des Dienst-Managers erst den Standort und anschließend die Option **Komponenten**. Klicken Sie dann auf die Komponente, die neu gestartet werden soll: **SMS_DMP_DOWNLOADER**.

1. Wechseln Sie zum Menü **Komponente**, und klicken Sie auf **Abfrage**.

1. Überprüfen Sie den aktuellen Status der Komponente. Navigieren Sie dann zum Menü **Komponente**, und klicken Sie auf **Beenden**.  

1. Führen Sie erneut eine **Abfrage** der Komponente aus, um zu bestätigen, dass sie beendet wurde. Klicken Sie dann auf die Komponentenaktion **Starten**, um diese neu zu starten.

## <a name="remote-site-system-requirements"></a>Anforderungen an das Remotestandortsystem

Wenn Sie den Dienstverbindungspunkt auf einem Remoteserver des Standortsystems installieren, konfigurieren Sie die folgenden Anforderungen:

- Das Computerkonto des Standortservers muss ein lokaler Administrator auf dem Computer sein, der einen Remotedienstverbindungspunkt hostet.

- Richten Sie den Standortsystemserver, der diese Rolle hostet, mit einem [Standortsystem-Installationskonto](../../../plan-design/hierarchy/accounts.md#site-system-installation-account) ein. Der Verteilungs-Manager auf dem Standortserver verwendet das Standortsystem-Installationskonto zum Übertragen von Updates vom Dienstverbindungspunkt.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a> Erforderliche Berechtigungen für den Internetzugriff

Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, müssen Sie den Zugriff auf Internetendpunkte durch den Dienstverbindungspunkt zulassen.

Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../../plan-design/network/internet-endpoints.md#bkmk_scp).

## <a name="install"></a>Installation

Beim Ausführen von **Setup** zum Installieren des Standorts der obersten Ebene einer Hierarchie haben Sie die Möglichkeit, den Dienstverbindungspunkt zu installieren.

Nach der Ausführung von „Setup“ oder wenn Sie die Rolle neu installieren, sollten Sie den Assistenten zum **Hinzufügen von Standortsystemrollen** oder den Assistenten zum **Erstellen von Standortsystemservern** verwenden. Konfigurieren Sie den Dienstverbindungspunkt nur am Standort auf der obersten Ebene Ihrer Hierarchie. Weitere Informationen finden Sie unter [Installieren von Standortsystemrollen](install-site-system-roles.md).

## <a name="move-the-role"></a><a name="bkmk_move"></a> Verschieben der Rolle

<!-- SCCMDocs#922 -->
Es gibt mehrere Szenarios, in denen Sie möglicherweise den Dienstverbindungspunkt auf einen anderen Server verschieben müssen:

- [Wiederherstellung](../../manage/recover-sites.md)
- [Hochverfügbarkeit der Standortserver](site-server-high-availability.md)
- [Standorterweiterung](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Nachdem Sie den Dienstverbindungspunkt verschoben haben, überprüfen Sie die Standortfunktionen. Beispielsweise müssen Sie möglicherweise den geheimen Schlüssel für alle Verbindungen mit Azure Active Directory-Mandanten (Azure AD) erneuern. Weitere Informationen finden Sie unter [Geheimen Schlüssel erneuern](azure-services-wizard.md#bkmk_renew).

## <a name="log-files"></a>Protokolldateien

Rufen Sie **Dmpuploader.log** auf dem Server ab, auf dem der Dienstverbindungspunkt ausgeführt wird, um Informationen zu Uploads in Microsoft anzuzeigen. In der Datei **Dmpdownloader.log** finden Sie Informationen zu Downloads und zum Downloadfortschritt von Updates. Die vollständige Liste der mit dem Dienstverbindungspunkt verknüpften Protokolle finden Sie unter [Protokolldateireferenz](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog) im Abschnitt „Dienstverbindungspunkt“.

## <a name="next-steps"></a>Nächste Schritte

Die folgenden Flussdiagramme sollten Ihnen dabei helfen, den Prozessablauf und die wichtigsten Protokolleinträge nachzuvollziehen. Dieser Vorgang umfasst Updatedownloads und die Replikation von Updates auf andere Standorte.

- [Flussdiagramm: Herunterladen von Updates](../../manage/download-updates-flowchart.md)

- [Flussdiagramm: Aktualisieren von Replikationen](../../manage/update-replication-flowchart.md)
