---
title: Microsoft Connected Cache
titleSuffix: Configuration Manager
description: Verwenden eines Configuration Manager-Verteilungspunkts als lokalen Cacheserver für die Übermittlungsoptimierung
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e718e62f097a9fec20d7b29deb9f03453931188a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696208"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Microsoft Connected Cache in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--3555764-->

Ab Version 1906 können Sie einen Microsoft Connected Cache-Server auf Ihren Verteilungspunkten installieren. Wenn Sie diese Art von Inhalt lokal zwischenspeichern, können Ihre Clients von dem Feature zur Übermittlungsoptimierung profitieren, und Sie können dabei helfen, WAN-Links zu schützen.

> [!NOTE]
> Ab Version 1910 wird dieses Feature als **Microsoft Connected Cache** bezeichnet. Zuvor wurde es als Übermittlungsoptimierung durch netzwerkinternen Cache (Delivery Optimization In-Network Cache, DOINC) bezeichnet.

Dieser Cacheserver dient als bedarfsgesteuerter transparenter Cache für Inhalt, der von der Übermittlungsoptimierung heruntergeladen wird. Verwenden Sie Clienteinstellungen, um sicherzustellen, dass dieser Server nur Mitgliedern der lokalen Begrenzungsgruppe für Configuration Manager angeboten wird.

Dieser Cache ist unabhängig vom Inhalt des Verteilungspunkts für Configuration Manager. Wenn Sie denselben Datenträger auswählen wie die Rolle des Verteilungspunkts, wird der Inhalt separat gespeichert.

> [!Note]  
> Der Connected Cache-Server ist eine Anwendung, die unter Windows Server installiert ist. Diese Anwendung befindet sich noch in der Entwicklung.

## <a name="how-it-works"></a>Funktionsweise

Wenn Sie Clients für die Verwendung des Connected Cache-Servers konfigurieren, werden keine von der Microsoft Cloud verwalteten Inhalte mehr aus dem Internet angefordert. Clients fordern diese Inhalte vom Cache-Server an, der im Verteilungspunkt installiert ist. Vom lokalen Server werden diese Inhalte mit dem IIS-Feature für das Routing von Anwendungsanforderungen (ARR) zwischengespeichert. Anschließend kann der Cacheserver schnell auf künftige Anforderungen derselben Inhalte reagieren. Wenn der Connected Cache-Server nicht verfügbar ist oder die Inhalte noch nicht zwischengespeichert sind, laden Clients den Inhalt aus dem Internet herunter. Clients nutzen auch die Übermittlungsoptimierung. Laden Sie also Teile der Inhalte von Peers in Ihrem Netzwerk herunter.

![Diagramm der Funktionsweise von Connected Cache](media/3555764-microsoft-connected-cache.png)

1. Der Client sucht nach Updates und ruft die Adresse für das Content Delivery Network (CDN) ab.

2. Configuration Manager konfiguriert Einstellungen der Übermittlungsoptimierung auf dem Client, u. a. den Namen des Cacheservers.

3. Client A fordert Inhalte vom Cacheserver der Übermittlungsoptimierung an.

4. Wenn die Inhalte nicht im Cache enthalten sind, ruft der Cacheserver der Übermittlungsoptimierung sie aus dem CDN ab.

5. Wenn der Cacheserver nicht antwortet, lädt der Client die Inhalte aus dem CDN herunter.

6. Client rufen mit der Übermittlungsoptimierung Teile der Inhalte von Peers ab.

## <a name="prerequisites-and-limitations"></a>Voraussetzungen und Einschränkungen

- Ein *lokaler* Verteilungspunkt mit folgenden Konfigurationen:

  - Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 oder Windows Server 2019 wird ausgeführt.

  - Die Standardwebsite ist an Port 80 aktiviert.

  - Das ARR-Feature ([Routing von Anwendungsanforderungen](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview)) von IIS darf nicht vorinstalliert sein. Connected Cache installiert ARR und konfiguriert die zugehörigen Einstellungen. Microsoft kann nicht garantieren, dass die ARR-Konfiguration von Connected Cache nicht mit anderen Anwendungen auf dem Server in Konflikt steht, die dieses Feature ebenfalls verwenden.

  - Der Verteilungspunkt benötigt Zugriff auf die Microsoft-Cloud über das Internet. Die genauen URLs können je nach cloudfähigem Inhalt variieren. Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../network/internet-endpoints.md).

  - Ab Version 2002 kann die Connected Cache-Anwendung einen nicht authentifizierten Proxyserver für den Internetzugriff verwenden. Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server).<!-- 5856396 -->

- Clients unter Windows 10, Version 1709 oder höher

## <a name="enable-connected-cache"></a>Aktivieren von Connected Cache

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie dann den Knoten **Verteilungspunkte** aus.

1. Wählen Sie einen *lokalen* Verteilungspunkt aus, und wählen Sie im Menüband die Option **Eigenschaften** aus.

1. Konfigurieren Sie auf der Registerkarte **Allgemein** in den Eigenschaften der Verteilungspunktrolle die folgenden Einstellungen:  

    1. Aktivieren Sie die Option **Diesen Verteilungspunkt für die Verwendung als verbundener Microsoft-Cacheserver aktivieren**.  

        Lesen Sie die Lizenzbedingungen durch, und akzeptieren Sie sie.

    2. **Zu verwendender lokaler Datenträger:** Wählen Sie den Datenträger aus, der für den Cache verwendet werden soll. **Automatisch** ist der Standardwert, der den Datenträger mit dem meisten freien Speicherplatz verwendet.<sup>[Hinweis 1](#bkmk_note1)</sup>  

        > [!Note]  
        > Sie können diesen Datenträger später ändern. Alle zwischengespeicherten Inhalte gehen verloren, es sei denn, Sie kopieren sie auf das neue Laufwerk.

    3. **Speicherplatz:** Legen Sie fest, wie viel Speicherplatz in GB oder in Prozent im Verhältnis zum Gesamtspeicherplatz auf dem Datenträger reserviert werden soll. Der Standardwert beträgt 100 GB.

        > [!Note]  
        > Die Standardcachegröße sollte für die meisten Kunden ausreichend sein. Sie können die Cachegröße später anpassen.
        >
        > Wenn die Cachegröße auf dem Datenträger den zugewiesenen Speicherplatz überschreitet, gibt ARR Speicherplatz frei, indem Inhalte auf Grundlage der integrierten Heuristik entfernt werden.<!-- SCCMDocs#2045 -->

    4. **Cache beim Deaktivieren des verbundenen Cacheservers beibehalten**: Wenn Sie den Cacheserver entfernen und diese Option aktivieren, behält der Server weiter den Inhalt des Caches auf dem Datenträger.  

1. Konfigurieren Sie unter „Clienteinstellungen“ in der Gruppe **Übermittlungsoptimierung** die entsprechende Einstellung **Enable devices managed by Configuration Manager to use Microsoft Connected Cache servers for content download** (Aktivieren von Geräten, die von Configuration Manager verwaltet werden, zur Verwendung des Microsoft Connected Cache-Servers für das Herunterladen von Inhalt).  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a> Hinweis 1: Informationen zur Laufwerkauswahl

Wenn Sie auf **Automatisch** klicken, wird die Datei **no_sms_on_drive.sms** berücksichtigt, während Configuration Manager die Connected Cache-Komponente installiert. Angenommen, der Verteilungspunkt verfügt über die Datei `C:\no_sms_on_drive.sms`. Dann konfiguriert Configuration Manager die Connected Cache-Komponente für die Verwendung eines anderen Laufwerks für den Cache, auch wenn auf dem Laufwerk C: am meisten Speicherplatz frei ist.

Wenn Sie ein Laufwerk auswählen, auf dem bereits die Datei **no_sms_on_drive** gespeichert ist, ignoriert Configuration Manager diese Datei. Die Konfiguration von Connected Cache für die Verwendung dieses Laufwerks ist eine explizite Absicht. Angenommen, der Verteilungspunkt verfügt über die Datei `F:\no_sms_on_drive.sms`. Wenn Sie die Verteilungspunkteigenschaften explizit für die Verwendung des Laufwerks **F:** konfigurieren, konfiguriert Configuration Manager Connected Cache für die Verwendung des Laufwerks F: für den Cache.

So ändern Sie das Laufwerk nach der Installation von Connected Cache:

- Konfigurieren Sie die Verteilungspunkteigenschaften manuell so, dass ein bestimmter Laufwerkbuchstabe verwendet wird.

- Wenn die Einstellung auf „Automatisch“ festgelegt ist, erstellen Sie zuerst die Datei **no_sms_on_drive.sms**. Nehmen Sie dann einige Änderungen an den Eigenschaften des Verteilungspunkts vor, um eine Änderung der Konfiguration auszulösen.

## <a name="verify"></a>Überprüfen

Wenn Clients von der Cloud verwalteten Inhalt herunterladen, verwenden sie die Übermittlungsoptimierung des Cacheservers, der auf Ihrem Verwaltungspunkt installiert ist. Es gibt die folgenden Arten von Inhalten, die von der Cloud verwaltet werden:

- Microsoft Store-Apps
- Bedarfsgesteuerte Windows-Features, z. B. Sprachen
- Wenn Sie die Option [Windows Update for Business-Richtlinien](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md) aktivieren: Windows 10-Feature und Qualitätsupdates
- Für [Workloads für die Co-Verwaltung:](../../../comanage/workloads.md)
  - Windows Update for Business: Windows 10-Feature und Qualitätsupdates
  - Office-Klick-und-Los-Apps: Office-Apps und Updates
  - Client-Apps: Microsoft Store-Apps und Updates
  - Endpoint Protection: Definitionsupdates für Windows Defender

Überprüfen Sie dieses Verhalten unter Windows 10, Version 1809 oder höher mithilfe des Windows PowerShell-Cmdlets **Get-DeliveryOptimizationStatus**. Überprüfen Sie anschließend in der Ausgabe des Cmdlets den Wert **BytesFromCacheServer**. Weitere Informationen finden Sie unter [Monitor Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization) (Überwachen der Übermittlungsoptimierung).

Wenn der Cacheserver einen HTTP-Fehler zurückgibt, greift der Übermittlungsoptimierungsclient auf die ursprüngliche Cloudquelle zurück.

Weitere Informationen finden Sie unter [Problembehandlung für Microsoft Connected Cache in Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a> Support für Intune Win32-Apps

<!--5032900-->

Wenn Sie ab Version 1910 Connected Cache auf Ihren Configuration Manager-Verteilungspunkten aktivieren, können sie Microsoft Intune Win32-Apps für gemeinsam verwaltete Clients verarbeiten.

### <a name="prerequisites"></a>Voraussetzungen

#### <a name="client"></a>Client

- Aktualisieren Sie den Client auf die neueste Version.

- Das Clientgerät muss über mindestens 4 GB Arbeitsspeicher verfügen.

    > [!TIP]
    > Verwenden Sie die folgende Gruppenrichtlinieneinstellung: Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Übermittlungsoptimierung > **Minimale RAM-Kapazität (einschließlich), die zur Verwendung des Peercachings erforderlich ist (in GB)** .

#### <a name="site"></a>Standort

- Aktivieren Sie Connected Cache auf einem Verteilungspunkt. Weitere Informationen finden Sie unter [Microsoft Connected Cache](microsoft-connected-cache.md).

- Der Client und der Connected Cache-fähige Verteilungspunkt müssen sich in derselben Begrenzungsgruppe befinden.

- Aktivieren Sie in der Gruppe [**Übermittlungsoptimierung**](../../clients/deploy/about-client-settings.md#delivery-optimization) die folgenden Clienteinstellungen:

  - **Verwenden Sie Configuration Manager-Begrenzungsgruppen für die Gruppen-ID der Übermittlungsoptimierung**
  - **Ermöglichen Sie Geräten, die von Configuration Manager verwaltet werden, die Verwendung verbundener Microsoft-Cacheserver für den Inhaltsdownload**

- Aktivieren Sie die Vorabversionsfunktion**Client-Apps für gemeinsam verwaltete Geräte**. Weitere Informationen finden Sie unter [Features der Vorabversion](../../servers/manage/pre-release-features.md).

- Aktivieren Sie die Co-Verwaltung, und schalten Sie die Workload **Client-Apps** auf die **Pilotversion von Intune** oder **Intune** um. Weitere Informationen finden Sie in den folgenden Artikeln:

  - [Workloads – Client-Apps](../../../comanage/workloads.md#client-apps)
  - [Aktivieren der Co-Verwaltung](../../../comanage/how-to-enable.md)
  - [Verschieben von Workloads zu Intune](../../../comanage/how-to-switch-workloads.md)

    Fügen Sie im Pilotversuch den Client der Pilotsammlung für Client-Apps hinzu.

#### <a name="intune"></a>Intune

- Diese Funktion unterstützt nur den Intune-Win32-App-Typ.

  - Zu diesem Zweck müssen Sie in Intune eine neue App erstellen und zuweisen (bereitstellen). (Apps, die vor der Intune-Version 1811 erstellt wurden, funktionieren nicht.) Weitere Informationen finden Sie unter [Intune Win32-App-Verwaltung](https://docs.microsoft.com/intune/apps/apps-win32-app-management).

  - Die App muss mindestens 100 MB groß sein.
  
    > [!TIP]
    > Verwenden Sie die folgende Gruppenrichtlinieneinstellung: Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Übermittlungsoptimierung > **Minimale Größe der Inhaltsdatei für das Peercaching (in MB)** .

## <a name="see-also"></a>Weitere Informationen:

[Optimieren der Bereitstellung von Updates für Windows 10 mit Configuration Manager](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Problembehandlung für Microsoft Connected Cache in Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
