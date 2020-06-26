---
title: Überwachen der Verbindungsintegrität
titleSuffix: Configuration Manager
description: Ausführliche Informationen zum Überwachen der Verbindungsintegrität und der Gerätezustände für Desktop Analytics in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: db70eab54f319197f267173fe857d0fb147a7eba
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746560"
---
# <a name="monitor-connection-health"></a>Überwachen der Verbindungsintegrität

Verwenden Sie das Dashboard **Verbindungsintegrität** in Configuration Manager, um die Geräteintegrität nach Kategorien aufzuschlüsseln. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie den Knoten **Desktop Analytics-Wartung**, und wählen Sie das Dashboard **Verbindungsintegrität** aus.  

[![Screenshot des Dashboards „Verbindungsintegrität“ in Configuration Manager](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

Beim erstmaligen Einrichten von Desktop Analytics werden in diesen Diagrammen möglicherweise keine vollständigen Daten angezeigt. Es kann zwei bis drei Tage dauern, bis aktive Geräte Diagnosedaten an den Desktop Analytics-Dienst – den Dienst zum Verarbeiten der Daten – senden und mit Ihrem Configuration Manager-Standort synchronisieren.<!-- 4098037 -->

## <a name="connection-details"></a>Verbindungsdetails

Auf dieser Kachel werden die folgenden grundlegenden Informationen über die Verbindung von Configuration Manager zu Desktop Analytics angezeigt:

- **Mandantenname**: Der Name der Desktop Analytics-Verbindung im Knoten **Azure-Dienste**

- **Zielsammlung**: Die *Zielsammlung*, die Sie auch beim Herstellen einer Verbindung von Configuration Manager mit Desktop Analytics angegeben haben. Diese Sammlung enthält alle Geräte, die von Configuration Manager mit den Einstellungen für kommerzielle ID und Diagnosedaten konfiguriert werden. Dabei handelt es sich um sämtliche Geräte, die Configuration Manager mit dem Desktop Analytics-Dienst verbindet.

- **Zielgeräte**: Alle Geräte in der Zielsammlung mit Ausnahme der folgenden Gerätetypen:

  - Außer Betrieb
  - Veraltet
  - Inaktiv
  - Nicht verwaltet
  - Geräte, auf denen eine LTSC-Version (Long-Term Servicing Channel) von Windows 10 ausgeführt wird
  - Geräte, auf denen Windows Server ausgeführt wird

    Weitere Informationen zu diesen Gerätezuständen finden Sie unter [Informationen zum Clientstatus](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager lädt alle Geräte aus der Zielsammlung mit Ausnahme von außer Betrieb gesetzten und veralteten Clients in Desktop Analytics hoch.

- **Für Desktop Analytics zugelassene Geräte**: Die Anzahl der Zielgeräte abzüglich der Geräte, die für Desktop Analytics nicht infrage kommen. Dies sind beispielsweise Geräte in der Zielsammlung, auf denen Windows Server oder Windows 10 LTSC (Long-Term Servicing Channel) ausgeführt wird.

## <a name="last-sync-details"></a>Details zur letzten Synchronisierung

Auf dieser Kachel wird angezeigt, ob Configuration Manager eine Synchronisierung mit dem Desktop Analytics-Clouddienst ausführt und wie viele Geräte synchronisiert werden.

- **Geräte synchronisiert**: Die Anzahl der berechtigten Geräte, die Configuration Manager an Desktop Analytics sendet. Der Dienst schließt diese Geräte in die derzeit angezeigte Momentaufnahme ein.

- **Letzte Dienstsynchronisierung**: Stimmt mit der Zeit unter **Zuletzt aktualisiert** im Desktop Analytics-Portal überein.

- **Nächste Dienstsynchronisierung**: Voraussichtlicher Zeitpunkt der nächsten täglichen Momentaufnahme in Desktop Analytics.

> [!Note]  
> Beim erstmaligen Registrieren von Geräten bei Desktop Analytics kann es mehrere Tage dauern, bis Daten hochgeladen und verarbeitet wurden. In der Zwischenzeit bleibt die Kachel **Details zur letzten Synchronisierung** möglicherweise leer.
> Außerdem wird keiner der Werte auf dieser Kachel automatisch aktualisiert, wenn Sie eine bedarfsgesteuerte Momentaufnahme anfordern. Weitere Informationen finden Sie unter [Datenlatenz](troubleshooting.md#data-latency).

Wenn Sie vermuten, dass einige Geräte in Desktop Analytics nicht angezeigt werden, vergewissern Sie sich, dass die Geräte von Desktop Analytics unterstützt werden. Weitere Informationen finden Sie unter [Voraussetzungen](overview.md#prerequisites).

## <a name="connection-health"></a>Verbindungsintegrität

Im Diagramm **Verbindungsintegrität** wird die Anzahl der Geräte mit den folgenden Integritätszuständen angezeigt:  

- [Ordnungsgemäß registriert](#properly-enrolled): Das Gerät wird in Desktop Analytics mit einem vollständigen Inventar angezeigt.
- [Registrierung nicht möglich](#unable-to-enroll): Es gibt ein Blockierproblem, das die Geräteregistrierung verhindert.
- [Konfigurationswarnung](#configuration-alert): Das Gerät wird in Desktop Analytics nicht oder mit einem unvollständigen Inventar angezeigt. In Configuration Manager wurde außerdem ein Problem mit der Geräteregistrierung festgestellt.
- [Auf Registrierung wird gewartet](#awaiting-enrollment): Configuration Manager hat das Gerät konfiguriert, es wird jedoch noch nicht in Desktop Analytics angezeigt.
- [Status ausstehend](#status-pending): Configuration Manager konfiguriert dieses Gerät noch, oder es sind nicht genügend Daten vom Gerät zum Ermitteln seines Zustands vorhanden.
- [Daten fehlen](#missing-data): Configuration Manager hat das Gerät konfiguriert, in Desktop Analytics sind jedoch nur ein Teil der Daten vorhanden.

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Die Gesamtanzahl der Geräte in diesem Diagramm sollte mit dem Wert **Für Desktop Analytics zugelassene Geräte** auf der Kachel „Verbindungsdetails“ übereinstimmen.

Wählen Sie den Slice im Diagramm aus, um einen Drilldown zu einer Liste der Geräte mit dem jeweiligen Zustand auszuführen. Weitere Informationen finden Sie unter [Geräteliste](#device-list).

Wählen Sie den Namen der Kategorie aus, die Sie entfernen möchten, oder fügen Sie sie aus dem Diagramm hinzu. Mit dieser Aktion können Sie das Diagramm vergrößern, sodass die relativen Größen kleinerer Segmente zu erkennen sind.

### <a name="properly-enrolled"></a>Ordnungsgemäß registriert

Das Gerät verfügt über folgende Attribute:

- Ein Configuration Manager-Client der Version 1902 oder höher  
- Keine Konfigurationsfehler vorhanden  
- Desktop Analytics hat in den letzten 28 Tagen die gesamten Diagnosedaten von diesem Gerät erhalten  
- Desktop Analytics verfügt über ein vollständiges Inventar der Gerätekonfiguration und der installierten Apps  

### <a name="unable-to-enroll"></a>Registrierung nicht möglich

Configuration Manager erkennt ein oder mehrere Blockierprobleme, die die Geräteregistrierung verhindern. Weitere Informationen finden Sie in der Liste der [Desktop Analytics-Geräteeigenschaften in Configuration Manager](#bkmk_config-issues).  

Beispielsweise hat der Configuration Manager-Client nicht mindestens die Versionsnummer 1902 (5.0.8790). Aktualisieren Sie den Client auf die neueste Version. Aktivieren Sie ggf. das automatische Clientupdate für den Configuration Manager-Standort. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

> [!TIP]
> In Verbindung mit dem erweiterten Sicherheitsupdate von April 2020 (ESU) für Windows 7 ist das Problem bekannt, dass Geräte diesen Fehler fälschlicherweise melden. Weitere Informationen finden Sie in den [Versionsanmerkungen](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

Ab Version 2002 können Sie Probleme mit der Clientproxykonfiguration in zwei Bereichen leichter erkennen:

- **Endpunktkonnektivitätsüberwachung:** Wenn Clients einen erforderlichen Endpunkt nicht erreichen können, wird auf dem Dashboard eine Konfigurationswarnung angezeigt. Führen Sie einen Drilldown bei Clients aus, die sich nicht registrieren können, um die Endpunkte anzuzeigen, auf die Clients aufgrund von Problemen mit der Proxykonfiguration nicht zugreifen können. Weitere Informationen finden Sie unter [Endpunktverbindungsüberwachungen](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Konnektivitätsstatus:** Wenn Ihre Clients einen Proxyserver für den Zugriff auf Desktop Analytics verwenden, werden in Configuration Manager Probleme bei der Proxyauthentifizierung von Clients angezeigt. Führen Sie einen Drilldown aus, um Clients anzuzeigen, die wegen Problemen bei der Proxyauthentifizierung nicht registriert werden können. Weitere Informationen finden Sie unter [Konnektivitätsstatus](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Konfigurationswarnung

Das Gerät wird in Desktop Analytics nicht oder mit einem unvollständigen Inventar angezeigt. In Configuration Manager wurde außerdem ein Problem mit der Geräteregistrierung festgestellt. Weitere Informationen finden Sie in der Liste der [Desktop Analytics-Geräteeigenschaften in Configuration Manager](#bkmk_config-issues).

Beispielsweise verfügt das Gerät über keine Verbindung mit dem Dienst. Weitere Informationen finden Sie unter [Konnektivität mit Windows-Diagnoseendpunkt](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Auf Registrierung wird gewartet

Desktop Analytics verfügt über keine Diagnosedaten für dieses Gerät. Ursache für dieses Problem kann es sein, dass Sie das Gerät der Zielsammlung erst kürzlich hinzugefügt haben und noch keine Daten gesendet wurden. Dies kann auch bedeuten, dass das Gerät nicht ordnungsgemäß mit dem Dienst kommuniziert und die neuesten Diagnosedaten älter als 28 Tage sind.

Stellen Sie sicher, dass das Gerät mit dem Dienst kommunizieren kann. Weitere Informationen finden Sie unter [Endpunkte](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Status ausstehend

Configuration Manager konfiguriert dieses Gerät noch, oder es sind nicht genügend Daten vom Gerät zum Ermitteln seines Zustands vorhanden.

### <a name="missing-data"></a>Daten fehlen

Das Gerät wurde von Configuration Manager erfolgreich konfiguriert, Desktop Analytics kann jedoch keine Bewertung der Kompatibilität erstellen. Es ist kein vollständiges Dataset für die Konfiguration des Geräts (Census) oder die installierten Apps (Inventar) vorhanden.

Dieses Problem wird häufig automatisch behoben, wenn das Gerät den Versuch wiederholt. Wenn das Problem weiterhin auftritt, stellen Sie sicher, dass das Gerät mit dem Dienst kommunizieren kann. Weitere Informationen finden Sie unter [Endpunkte](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Geräteliste

Wenn Sie eine bestimmte Liste von Geräten nach Status anzeigen möchten, verwenden Sie zunächst das Dashboard **Verbindungsintegrität**. Wählen Sie eines der Segmente der Kachel **Verbindungsintegrität** aus, und führen Sie einen Drilldown zur Liste der Geräte mit diesem Zustand aus. In dieser benutzerdefinierten Geräteansicht werden standardmäßig die folgenden Desktop Analytics-Spalten angezeigt:

- Konfiguration der kommerziellen ID
- Mindestens erforderliches Kompatibilitätsupdate
- Einwilligung für Windows-Diagnosedaten
- Einwilligung für kommerzielle Windows-Daten
- Konnektivität mit Windows-Diagnoseendpunkt
- Konnektivitätsstatus (ab Version 2002)
- Endpunktverbindungsüberwachungen (ab Version 2002)

Diese Spalten entsprechen den wichtigsten [Voraussetzungen](overview.md#prerequisites) für Geräte, damit diese mit Desktop Analytics kommunizieren können.

[![Screenshot: „Registrierung des Geräts unmöglich“](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Wählen Sie ein Gerät aus, um die vollständige Liste der verfügbaren Eigenschaften im Detailbereich anzuzeigen. Sie können auch jede dieser Eigenschaften als Spalten der Geräteliste hinzufügen.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> Geräteeigenschaften

Die folgenden Desktop Analytics-Geräteeigenschaften sind als Spalten in der Configuration Manager-Geräteliste verfügbar:

- [Endpunktverbindungsüberwachungen](#endpoint-connectivity-checks) (ab Version 2002)
- [Konnektivitätsstatus](#connectivity-status) (ab Version 2002)
- [Appraiser-Konfiguration](#appraiser-configuration)  
- [Mindestens erforderliches Kompatibilitätsupdate](#minimum-compatibility-update)  
- [Appraiser-Version](#appraiser-version)  
- [Letzte erfolgreiche vollständige Ausführung von Appraiser](#last-successful-full-run-of-appraiser)  
- [Appraiser-Datensammlung](#appraiser-data-collection)  
- [Letzte erfolgreiche vollständige Ausführung von Census](#last-successful-full-run-of-census)  
- [Census-Datensammlung](#census-data-collection)  
- [Konnektivität mit Windows-Diagnoseendpunkt](#windows-diagnostic-endpoint-connectivity)  
- [Diagnosedaten von Endbenutzern prüfen](#check-end-user-diagnostic-data)  
- [Benutzerproxy überprüfen](#check-user-proxy)  
- [Konfiguration der kommerziellen ID](#commercial-id-configuration)  
- [Einwilligung für kommerzielle Windows-Daten](#windows-commercial-data-opt-in)  
- [Gerätenamen in Diagnosedaten prüfen](#check-device-name-in-diagnostic-data)  
- [DiagTrack-Dienstkonfiguration](#diagtrack-service-configuration)  
- [DiagTrack-Version](#diagtrack-version)  
- [SQM-ID abrufen](#sqm-id-retrieval)  
- [Eindeutige Geräte-ID abrufen](#unique-device-identifier-retrieval)  
- [Einwilligung für Windows-Diagnosedaten](#windows-diagnostic-data-opt-in)  

Auf der Kachel **Häufigste Registrierungsblocker und Konfigurationswarnungen** des Dashboards „Verbindungsintegrität“ werden die Eigenschaften angezeigt, bei denen Geräte am häufigsten ein Problem melden.

### <a name="endpoint-connectivity-checks"></a>Endpunktverbindungsüberwachungen

Ab Version 2002 gilt Folgendes:<!-- 4963230 --> Um Probleme mit der Proxyauthentifizierung zu erkennen, führen Clients Verbindungsüberwachungen für erforderliche Endpunkte durch. Wenn ein Client einen erforderlichen Endpunkt nicht erreichen kann, zeigt diese Eigenschaft eine nummerierte Liste von Endpunkten an, mit denen keine Verbindung hergestellt werden kann, weil Probleme mit der Proxykonfiguration auftreten. Vergleichen Sie diese Liste mit der veröffentlichten Liste [erforderlicher Endpunkte](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Konnektivitätsstatus

Ab Version 2002 gilt Folgendes:<!-- 4963383 --> Wenn Ihre Clients einen Proxyserver für den Zugriff auf Desktop Analytics verwenden, zeigt diese Eigenschaft Probleme bei der Proxyauthentifizierung an. Sie enthält die folgenden Details im Zusammenhang mit der Proxyauthentifizierung:

- Statuscode
- Rückgabecode

In der Protokolldatei werden Fehler wie etwa der folgende angezeigt:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Dabei ist `%s` die URL eines erforderlichen Endpunkts.

Möglicherweise werden auch nicht deterministische Fehlermeldungen angezeigt, die erst beachtet werden müssen, wenn bei einem Gerät Registrierungsprobleme auftreten. Beispiel:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Weitere Informationen zum Konfigurieren von Proxyservern für die Verwendung mit Desktop Analytics finden Sie unter [Proxyserverauthentifizierung](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Appraiser-Konfiguration

<!--20,21-->
Bei Appraiser handelt es sich um die Windows-Komponente, die den [Kompatibilitätsupdates](enroll-devices.md#update-devices) entspricht. Er überprüft die Apps und Treiber auf dem Gerät auf Kompatibilität mit der aktuellen Windows-Version.

Wenn diese Überprüfung erfolgreich ist, wird die Appraiser-Komponente ordnungsgemäß auf dem Gerät konfiguriert.

Andernfalls wird möglicherweise einer der folgenden Fehler angezeigt:

- Die Datensammlung zur Geräte-App-Kompatibilität (SetRequestAllAppraiserVersions) kann nicht konfiguriert werden. Details zur Ausnahme finden Sie in den Protokollen.  

- Die Datensammlung zur Geräte-App-Kompatibilität (SetRequestAllAppraiserVersions) kann nicht konfiguriert werden. Details zur Ausnahme finden Sie in den Protokollen.  

- RequestAllAppraiserVersions kann nicht in den Registrierungsschlüssel `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Appraiser` geschrieben werden. Überprüfen Sie die Berechtigungen.  

Überprüfen Sie die Berechtigungen für diesen Registrierungsschlüssel. Vergewissern Sie sich, dass das lokale Systemkonto auf diesen Schlüssel zugreifen kann, der für den Configuration Manager-Client festgelegt werden soll.  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

### <a name="minimum-compatibility-update"></a>Mindestens erforderliches Kompatibilitätsupdate

<!--18,19,32-->
Das Kompatibilitätsupdate („appraiser.dll“) ist auf dem Gerät nicht installiert oder veraltet. Es ist älter als die für Desktop Analytics mindestens erforderliche Version 10.0.17763.

Installieren Sie das neueste Kompatibilitätsupdate. Weitere Informationen finden Sie unter [Kompatibilitätsupdates](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Appraiser-Version

Diese Eigenschaft zeigt die aktuelle Version der Appraiser-Komponente auf dem Gerät an. Die Dateiversion auf `%windir%\System32\appraiser.dll` wird ohne Dezimaltrennzeichen angezeigt. Beispielsweise wird die Dateiversion 10.0.17763 als 10017763 angezeigt.

### <a name="last-successful-full-run-of-appraiser"></a>Letzte erfolgreiche vollständige Ausführung von Appraiser

Diese Eigenschaft gibt das Datum und die Uhrzeit der letzten erfolgreichen Ausführung von Appraiser an.

### <a name="appraiser-data-collection"></a>Appraiser-Datensammlung

<!--Appraiser run status-->
<!--22,33-->
Diese Eigenschaft zeigt das letzte Ergebnis der Ausführung der Appraiser-Komponente durch Windows an.

Wenn diese nicht erfolgreich war, wird möglicherweise einer der folgenden Fehler angezeigt:

- Es können keine App-Kompatibilitätsdaten (RunAppraiser) gesammelt werden. Details finden Sie in den Protokollen.  

- Die Datensammlung zur App-Kompatibilität (CompatTelRunner.exe) wurde mit einem Fehlercode beendet.  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.

Überprüfen Sie die folgende Datei: `%windir%\System32\CompatTelRunner.exe`. Wenn diese nicht vorhanden ist, installieren Sie die erforderlichen [Kompatibilitätsupdates](enroll-devices.md#update-devices) erneut. Stellen Sie sicher, dass diese Datei von keiner anderen Systemkomponente entfernt wird, z. B. einer Gruppenrichtlinie oder einem Antischadsoftwaredienst.

Wenn die Datei „M365AHandler.log“ auf dem Client einen der folgenden Fehler enthält:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Um diese Fehler zu beheben, führen Sie die folgenden Befehle in einer Windows PowerShell-Konsole mit erhöhten Rechten auf dem betroffenen Client aus:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Letzte erfolgreiche vollständige Ausführung von Census

Diese Eigenschaft gibt das Datum und die Uhrzeit der letzten erfolgreichen Ausführung von Census an.

### <a name="census-data-collection"></a>Census-Datensammlung

<!-- Census run status -->
<!--51,52-->
Census ist die Windows-Komponente, die das Geräteinventar erfasst. Diese Inventardaten werden verwendet, um Informationen über das Gerät und seine Konfiguration zu erhalten.

Diese Eigenschaft zeigt das letzte Ergebnis der Ausführung der Census-Komponente durch Windows an.

Wenn diese nicht erfolgreich war, wird möglicherweise einer der folgenden Fehler angezeigt:

- Es können keine Daten über das Gerät und seine Konfiguration erfasst werden (RunCensus). Details zur Ausnahme finden Sie in den Protokollen.  

- Das Tool zur Geräte- und Konfigurationsdatensammlung (devicecensus.exe) wurde nicht gefunden.  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.

Überprüfen Sie die folgende Datei: `%windir%\System32\DeviceCensus.exe`. Wenn diese nicht vorhanden ist, installieren Sie die erforderlichen [Kompatibilitätsupdates](enroll-devices.md#update-devices) erneut. Stellen Sie sicher, dass diese Datei von keiner anderen Systemkomponente entfernt wird, z. B. einer Gruppenrichtlinie oder einem Antischadsoftwaredienst.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Konnektivität mit Windows-Diagnoseendpunkt

<!--12,15-->
Wenn diese Überprüfung erfolgreich ist, kann das Gerät eine Verbindung mit dem Endpunkt „Benutzererfahrung und Telemetrie im verbundenen Modus“ (Vortex) herstellen.

Andernfalls wird möglicherweise einer der folgenden Fehler angezeigt:  

- Mit dem Endpunkt "Benutzererfahrung und Telemetrie im verbundenen Modus" (Vortex) ist keine Verbindung möglich. Überprüfen Sie die Netzwerk-/Proxyeinstellungen.  

- Die Konnektivität mit dem Endpunkt "Benutzererfahrung und Telemetrie im verbundenen Modus" (CheckVortexConnectivity) kann nicht überprüft werden. Details zur Ausnahme finden Sie in den Protokollen.  

Geräte überprüfen die Verbindung je nach Betriebssystemversion anhand einer GET-Anforderung an den folgenden Endpunkt:

| BS-Version | Endpunkt |
|------------|----------|
| – Windows 10, Version 1809 oder höher<br/>– Windows 10, Version 1803 mit dem kumulativen Update 2018-09 oder höher | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, Version 1803 *ohne* das kumulative Update 2018-09 oder höher | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, Version 1709 oder früher | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 oder Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Stellen Sie sicher, dass das Gerät mit dem Dienst kommunizieren kann. Bei dieser Überprüfung werden nur einige und nicht alle erforderlichen Endpunkte überprüft. Weitere Informationen finden Sie unter [Endpunkte](enable-data-sharing.md#endpoints).  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

### <a name="check-end-user-diagnostic-data"></a>Diagnosedaten von Endbenutzern prüfen

<!--1004-->
Wenn diese Überprüfung nicht erfolgreich ist, hat ein Benutzer Windows-Diagnosedaten auf niedrigerer Ebene auf dem Gerät ausgewählt. Ursache kann auch ein Gruppenrichtlinienobjekt sein, das einen Konflikt verursacht. Weitere Informationen finden Sie unter [Windows-Einstellungen](enroll-devices.md#windows-settings).

Je nach Ihren Geschäftsanforderungen können Sie die Benutzerauswahl über Gruppenrichtlinien deaktivieren. Verwenden Sie die Einstellung, um die **Benutzeroberfläche für die Festlegung der Telemetrieaktivierung zu konfigurieren**. Weitere Informationen finden Sie unter [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Benutzerproxy überprüfen

<!--30,35-->
Unter Windows 7 ist die Einstellung „DisableEnterpriseAuthProxy“ standardmäßig aktiviert. Auf Windows 8.1-Computern wird die Einstellung „DisableEnterpriseAuthProxy“ von Configuration Manager auf 0 (nicht deaktiviert) festgelegt.

Diese Eigenschaft zeigt möglicherweise die folgenden Fehler an:

- Der Authentifizierungsproxy ist aktiviert. Legen Sie DisableEnterpriseAuthProxy in `HKLM:\Software\Policies\Microsoft\Windows\DataCollection` auf 0 fest.

- Die Prüfung auf den Status des Authentifizierungsproxys ist nicht möglich. Details zur Ausnahme finden Sie in den Protokollen.

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

Überprüfen Sie die Berechtigungen für diesen Registrierungsschlüssel. Vergewissern Sie sich, dass das lokale Systemkonto auf diesen Schlüssel zugreifen kann, der für den Configuration Manager-Client festgelegt werden soll. Ursache kann auch ein Gruppenrichtlinienobjekt sein, das einen Konflikt verursacht. Weitere Informationen finden Sie unter [Windows-Einstellungen](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Konfiguration der kommerziellen ID

<!--9, 11, 53-->
Microsoft verwendet eine eindeutige kommerzielle ID zum Zuordnen von Informationen von Geräten zu Ihrem Desktop Analytics-Arbeitsbereich. Wenn Sie Configuration Manager in Desktop Analytics integrieren, wird diese ID automatisch beim Dienst abgefragt. Configuration Manager sollte diese ID automatisch auf Clients anwenden, die als Ziel in den Desktop Analytics-Einstellungen festgelegt sind.

Wenn diese Überprüfung erfolgreich ist, wird das Gerät ordnungsgemäß mit einer kommerziellen ID konfiguriert.

Andernfalls wird möglicherweise einer der folgenden Fehler angezeigt:

- CommercialId kann nicht in den Registrierungsschlüssel `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` geschrieben werden. Überprüfen Sie die Berechtigungen.  

- Die CommercialId im Registrierungsschlüssel `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` kann nicht aktualisiert werden. Details zur Ausnahme finden Sie in den Protokollen.  

- Geben Sie unter `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` den richtigen CommercialId-Wert an.  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

Überprüfen Sie die Berechtigungen für diesen Registrierungsschlüssel. Vergewissern Sie sich, dass das lokale Systemkonto auf diesen Schlüssel zugreifen kann, der für den Configuration Manager-Client festgelegt werden soll. Ursache kann auch ein Gruppenrichtlinienobjekt sein, das einen Konflikt verursacht. Weitere Informationen finden Sie unter [Windows-Einstellungen](enroll-devices.md#windows-settings).  

Es gibt eine andere ID für das Gerät. Dieser Registrierungsschlüssel wird von der Gruppenrichtlinie verwendet. Er hat Vorrang vor der von Configuration Manager bereitgestellten ID.  

<a name="bkmk_ViewCommercialID"></a> Gehen Sie wie folgt vor, um die kommerzielle ID im Desktop Analytics-Portal anzuzeigen:

1. Wechseln Sie zum Desktop Analytics-Portal, und wählen Sie in der Gruppe „Globale Einstellungen“ **Verbundene Dienste** aus.  

2. Im Bereich **Verbundene Dienste** ist standardmäßig der Bereich **Geräte registrieren** ausgewählt. Im Bereich „Geräte registrieren“ wird im Bereich „Informationen“ der Schlüssel für Ihre kommerzielle ID angezeigt.  

[![Screenshot der kommerziellen ID im Desktop Analytics-Portal](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Verwenden Sie **Neuen ID-Schlüssel abrufen** nur, wenn Sie den aktuellen Schlüssel nicht verwenden können. Wenn Sie die kommerzielle ID neu generieren, [registrieren Sie Ihre Geräte erneut mit der neuen ID](enroll-devices.md#device-enrollment). Dieser Vorgang kann zum Verlust von Diagnosedaten während des Übergangs führen.  

### <a name="windows-commercial-data-opt-in"></a>Einwilligung für kommerzielle Windows-Daten

<!--64-->
Diese Eigenschaft bezieht sich nur auf Geräte, auf denen Windows 7 oder Windows 8.1 ausgeführt wird. Sie führt ähnliche Tests wie [Einwilligung für Windows-Diagnosedaten](#windows-diagnostic-data-opt-in) aus, jedoch ohne den Wert „CommercialDataOptIn“.

### <a name="check-device-name-in-diagnostic-data"></a>Gerätenamen in Diagnosedaten prüfen

<!--56,58-->
Wenn diese Überprüfung erfolgreich ist, wird das Gerät ordnungsgemäß für die Veröffentlichung des Gerätenamens konfiguriert.

Andernfalls wird möglicherweise einer der folgenden Fehler angezeigt:

- Die Prüfung auf den Gerätenamen, der im Rahmen der Windows-Diagnosedaten an Microsoft gesendet werden soll, ist nicht möglich. Details zur Ausnahme finden Sie in den Protokollen.  

- AllowDeviceNameInTelemetry kann nicht in den Registrierungsschlüssel `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` geschrieben werden. Überprüfen Sie die Berechtigungen.  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

Überprüfen Sie die Berechtigungen für diesen Registrierungsschlüssel. Vergewissern Sie sich, dass das lokale Systemkonto auf diesen Schlüssel zugreifen kann, der für den Configuration Manager-Client festgelegt werden soll. Ursache kann auch ein Gruppenrichtlinienobjekt sein, das einen Konflikt verursacht. Weitere Informationen finden Sie unter [Windows-Einstellungen](enroll-devices.md#windows-settings).  

Stellen Sie sicher, dass diese Einstellung nicht von einem anderen Richtlinienmechanismus, z. B. einer Gruppenrichtlinie, deaktiviert wird.

### <a name="diagtrack-service-configuration"></a>DiagTrack-Dienstkonfiguration

<!--44,45,50-->
Wenn diese Überprüfung erfolgreich ist, wird die DiagTrack-Komponente ordnungsgemäß auf dem Gerät konfiguriert. Die für Desktop Analytics erforderliche Mindestversion ist 10010586 (10.0.10586).

Andernfalls wird möglicherweise einer der folgenden Fehler angezeigt:

- Die Komponente "Benutzererfahrung und Telemetrie im verbundenen Modus" (diagtrack.dll) ist veraltet. Überprüfen Sie die Anforderungen.  

    > [!TIP]
    > In Verbindung mit dem erweiterten Sicherheitsupdate von April 2020 (ESU) für Windows 7 ist das Problem bekannt, dass Geräte diesen Fehler fälschlicherweise melden. Weitere Informationen finden Sie in den [Versionsanmerkungen](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

- Die Komponente "Benutzererfahrung und Telemetrie im verbundenen Modus" (diagtrack.dll) wurde nicht gefunden. Überprüfen Sie die Anforderungen.  

- Aktivieren und starten Sie den Dienst "Benutzererfahrung und Telemetrie im verbundenen Modus", um Daten an Microsoft zu senden.  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installieren Sie die neuesten Updates. Weitere Informationen finden Sie unter [Geräteupdates](enroll-devices.md#update-devices).

Stellen Sie sicher, dass der Dienst **Benutzererfahrung und Telemetrie im verbundenen Modus** auf dem Gerät ausgeführt wird.

### <a name="diagtrack-version"></a>DiagTrack-Version

Diese Eigenschaft zeigt die aktuelle Version der Komponente „Benutzererfahrung und Telemetrie im verbundenen Modus“ auf dem Gerät an. Die Dateiversion auf `%windir%\System32\diagtrack.dll` wird ohne Dezimaltrennzeichen angezeigt. Beispielsweise wird die Dateiversion 10.0.10586 als 10010586 angezeigt.

### <a name="sqm-id-retrieval"></a>SQM-ID abrufen

<!--38-->
Diese Eigenschaft ist in erster Linie für Windows 7-Geräte gedacht. Sie kann von höheren Betriebssystemversionen als Fallbackbezeichner für das Gerät verwendet werden.

Wenn die Überprüfung nicht erfolgreich ist, wird möglicherweise der folgende Fehler angezeigt:

- Die Legacy-Gerätetelemetrie-ID (SQM-ID) kann nicht abgerufen werden.

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

Stellen Sie sicher, dass in Ihrer Umgebung keine doppelten IDs vorhanden sind. Dies kann beispielsweise der Fall sein, wenn Geräte mit einem Betriebssystemimage bereitgestellt wurden, das nicht generalisiert wurden.

### <a name="unique-device-identifier-retrieval"></a>Eindeutige Geräte-ID abrufen

<!--54-->
Desktop Analytics verwendet den Microsoft-Konto-Dienst, um eine zuverlässigere Geräte-ID abzurufen.

Stellen Sie sicher, dass der Dienst **Anmelde-Assistent für Microsoft-Konten** nicht deaktiviert ist. Der Starttyp sollte **Manuell (Start durch Auslöser)** lauten.

Verwenden Sie Richtlinieneinstellungen, anstatt diesen Endpunkt zu blockieren, um den Zugriff auf Endbenutzer-Microsoft-Konten zu deaktivieren. Weitere Informationen finden Sie unter [Das Microsoft-Konto im Unternehmen](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Einwilligung für Windows-Diagnosedaten

<!--8,40,55,62-->
Diese Eigenschaft überprüft, ob Windows ordnungsgemäß für das Zulassen von Diagnosedaten konfiguriert ist. Der Wert „AllowTelemetry“ wird in den folgenden Registrierungsschlüsseln überprüft:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Überprüfen Sie die Berechtigungen für diese Registrierungsschlüssel. Vergewissern Sie sich, dass das lokale Systemkonto auf diese Schlüssel zugreifen kann, die für den Configuration Manager-Client festgelegt werden sollen. Ursache kann auch ein Gruppenrichtlinienobjekt sein, das einen Konflikt verursacht. Weitere Informationen finden Sie unter [Windows-Einstellungen](enroll-devices.md#windows-settings).  

Weitere Informationen finden Sie in der Datei „M365AHandler.log“ auf dem Client.  

## <a name="see-also"></a>Weitere Informationen:

[Problembehandlung bei Desktop Analytics](troubleshooting.md)
