---
title: Anmerkungen zu dieser Version
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu dringenden Problemen, die im Produkt noch nicht behoben oder bisher in keinem Knowledge Base-Artikel des Microsoft-Supports beschrieben wurden.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9c1152b14da7c0a473e266b1ac1e6da2778aa105
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126290"
---
# <a name="release-notes-for-configuration-manager"></a>Anmerkungen zu dieser Version für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei Configuration Manager sind die Versionsanmerkungen auf dringende Probleme beschränkt. Diese Probleme sind im Produkt noch nicht behoben oder wurden bisher in keinem Knowledge Base-Artikel des Microsoft-Supports beschrieben.  

Die Dokumentation zu den einzelnen Features enthält Informationen zu bekannten Problemen, die sich auf wichtige Szenarien auswirken.  

Dieser Artikel enthält Versionshinweise zum aktuellen Configuration Manager-Branch. Informationen über den Technical Preview-Branch finden Sie unter [Technical Preview](../../../get-started/technical-preview.md).  

Informationen zu den neuen, in den verschiedenen Versionen eingeführten Features finden Sie in den folgenden Artikeln:

- [Neuerungen in Version 2006](../../../plan-design/changes/whats-new-in-version-2006.md)
- [Neuerungen in Version 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Neuerungen in Version 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Neuerungen in Version 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  

Informationen zu den neuen Features in Desktop Analytics finden Sie unter [Neues in Desktop Analytics](../../../../desktop-analytics/whats-new.md).

> [!Tip]  
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Einrichtung und Upgrade  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>Automatische Clientupgrades werden automatisch für alle Clients ausgeführt

<!-- 6040412 -->

*Gilt für Version 1910*

Wenn an Ihrem Standort das [automatische Clientupgrade](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade) verwendet wird und Sie den Standort auf Version 1910 aktualisieren, wird nach der Aktualisierung des Standorts automatisch ein Upgrade aller Clients ausgeführt. Lediglich der Empfang der Richtlinie durch die Clients erfolgt zufallsbasiert, per Voreinstellung jede Stunde. In einem großen Standort mit vielen Clients kann dieses Verhalten eine erhebliche Menge an Netzwerkdatenverkehr beanspruchen und eine Belastung für Verteilungspunkte darstellen.

Weitere Informationen zu betroffenen Versionen finden Sie unter [Updaterollup für den aktuellen Branch von Configuration Manager, Version 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Der Standortserver im passiven Modus aktualisiert „configuration.mof“ nicht

<!-- 5787848 -->

*Gilt für Version 1910*

Wenn Ihr Standort einen [Standortserver im passiven Modus](../configure/site-server-high-availability.md) enthält, gehen möglicherweise beim Aktualisieren Ihres Standorts Inventuranpassungen verloren. Der Standort synchronisiert aktuell die Datei „configuration.mof“ nicht, wenn Sie ein Failover des Serverstandorts ausführen.

Sichern Sie manuell die Datei „configuration.mof“ des Standorts wieder her und sichern Sie sie, um dieses Problem zu umgehen.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Warnung zu Setupvoraussetzungen für Domänenfunktionsebene unter Server 2019

<!-- 4904376 -->

*Gilt für Version 1906*

Beim Installieren des Updates für Version 1906 in einer Umgebung mit Domänencontrollern unter Windows Server 2019 wird bei der Prüfung der Voraussetzungen für die Domänenfunktionsebene die folgende Warnmeldung zurückgegeben:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Sie können dieses Problem umgehen, indem Sie die Warnung ignorieren.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>Synchronisierung von Azure AD-Benutzerermittlung und -Sammlungsgruppen funktioniert nicht nach der Standorterweiterung

<!-- 4797313 -->
*Gilt für Version 1906*

Nach dem Konfigurieren eines der folgenden Features:

- Azure Active Directory-Benutzergruppenermittlung
- Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen

Wenn Sie dann einen eigenständigen primären Standort auf eine Hierarchie mit einem zentralen Verwaltungsstandort erweitern, wird in SMS_AZUREAD_DISCOVERY_AGENT.log die folgende Fehlermeldung angezeigt:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Um dieses Problem zu umgehen, erneuern Sie den Schlüssel, der mit der App-Registrierung in Azure AD verknüpft ist. Weitere Informationen finden Sie unter [Geheimen Schlüssel erneuern](../configure/azure-services-wizard.md#bkmk_renew).

## <a name="role-based-administration"></a>Rollenbasierte Verwaltung

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Sicherheitsbereiche für bestimmte Ordner werden von CAS nicht an primäre Standorte repliziert
<!--6306759-->
*Gilt für Version 1910*

Nach dem Upgrade auf Version 1910 werden [Sicherheitsbereiche für Ordner](../configure/configure-role-based-administration.md#bkmk_config-folder) in Benutzer- und Gerätesammlungen von CAS nicht an primäre Standorte repliziert.

## <a name="application-management"></a>Anwendungsverwaltung

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Fehlermeldung „Unable to get certifcate for PowerShell“ (Es konnte kein Zertifikat für PowerShell abgerufen werden) beim Bereitstellen von Microsoft Edge (Version 77 und höher)
<!--5769384-->
*Gilt für: Configuration Manager Version 1910*

Wenn Sie die Configuration Manager-Konsole auf einem Betriebssystem ausführen, auf dem die Sprache Schwedisch, Ungarisch oder Japanisch ist, erhalten Sie beim Bereitstellen von Microsoft Edge (Version 77 und höher) die folgende Fehlermeldung:

`Unable to get certificate for Powershell`

Dieser Fehler tritt auf, weil ein `scripts`-Ordner nicht unter dem `AdminConsole\bin`-Verzeichnis für die Sprachen Schwedisch, Ungarisch oder Japanisch vorhanden ist. Der Ordner der Skripts ist in diesen Betriebssystemsprachen lokalisiert.

Erstellen Sie zum Umgehen dieses Problem einen Ordner namens `scripts` im Verzeichnis `AdminConsole\bin`. Kopieren Sie die Dateien aus Ihrem lokalisierten Ordner in den neu erstellten `scripts`-Ordner. Stellen Sie Microsoft Edge (Version 77 und höher) bereit, nachdem die Dateien kopiert wurden.

## <a name="os-deployment"></a>Bereitstellung des Betriebssystems

### <a name="task-sequences-cant-run-over-cmg"></a>Tasksequenzen können nicht über CMG ausgeführt werden

*Gilt für: Configuration Manager, Version 2002*

Es gibt zwei Fälle, in denen Tasksequenzen nicht auf einem Gerät ausgeführt werden können, das über ein Cloudverwaltungsgateway (Cloud Management Gateway, CMG) kommuniziert:

- Sie konfigurieren den Standort für Erweitertes HTTP, und der Verwaltungspunkt ist HTTP.<!-- 6358851 -->

    Um dieses Problem zu umgehen, aktualisieren Sie auf Version 2006. Alternativ dazu können Sie auch den Verwaltungspunkt für HTTPS konfigurieren.

- Sie haben den Client mit einem Massenregistrierungstoken für die Authentifizierung installiert und registriert.<!-- 6377921 -->

    Um dieses Problem zu umgehen, aktualisieren Sie auf Version 2006. Alternativ dazu können Sie auch eine der folgenden Authentifizierungsmethoden verwenden:

  - Vorabregistrierung des Geräts im internen Netzwerk
  - Konfigurieren des Geräts mit einem Clientauthentifizierungszertifikat
  - Verknüpfen des Geräts mit Azure AD

## <a name="software-updates"></a>Softwareupdates

### <a name="security-roles-are-missing-for-phased-deployments"></a>Sicherheitsrollen fehlen für stufenweise Bereitstellungen.

<!--3479337, SCCMDocs-pr issue 3095-->
*Gilt für: Configuration Manager, Version 1810, 1902*

Die integrierte Sicherheitsrolle **Betriebssystembereitstellungs-Manager** besitzt Berechtigungen für [stufenweise Bereitstellungen](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). Den folgenden Rollen fehlen diese Berechtigungen:  

- **Anwendungsadministrator**  
- **Anwendungsbereitstellungs-Manager**  
- **Softwareupdate-Manager**  

Die Rolle **App-Autor** scheint möglicherweise Berechtigungen für stufenweise Bereitstellungen zu besitzen, sollte aber nicht in der Lage sein, Bereitstellungen zu erstellen.

Ein Benutzer mit einer dieser Rollen kann den Assistenten zum Erstellen stufenweiser Bereitstellungen starten sowie stufenweise Bereitstellungen für eine Anwendung oder ein Softwareupdate anzeigen. Sie können weder den Assistenten abschließen noch Änderungen an einer vorhandenen Bereitstellung vornehmen.

Erstellen Sie zum Umgehen dieses Problems eine benutzerdefinierte Sicherheitsrolle. Kopieren Sie eine vorhandene Sicherheitsrolle, und fügen Sie die folgenden Berechtigungen für die Objektklasse **Stufenweise Bereitstellung** hinzu:

- Erstellen  
- Löschen  
- Ändern  
- Überwachungsdaten  

Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Sicherheitsrollen](../configure/configure-role-based-administration.md#BKMK_CreateSecRole).

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a> Ein erweitertes Sicherheitsupdate für Windows 7 bewirkt, dass für sie **Registrierung nicht möglich** angezeigt wird.

<!-- 7283186 -->
_Gilt für: Configuration Manager, Version 2002 und früher_

Im erweiterten Sicherheitsupdate (Extended Security Update, ESU) für Windows 7 vom April 2020 wurde die mindestens erforderliche Version von „diagtrack.dll“ von 10586 in 10240 geändert. Diese Änderung bewirkt, dass für Windows 7-Geräte **Registrierung nicht möglich** auf dem Desktop Analytics-Dashboard **Verbindungsintegrität** angezeigt wird. Wenn Sie einen Drilldown zur Geräteansicht für diesen Status ausführen, wird in der Eigenschaft **DiagTrack-Dienstkonfiguration** der folgende Status angezeigt: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

Für dieses Problem ist keine Problemumgehung erforderlich. Deinstallieren Sie das ESU von April nicht. Bei ansonsten ordnungsgemäßer Konfiguration melden die Windows 7-Geräte weiterhin Diagnosedaten an den Desktop Analytics-Dienst und werden weiterhin im Portal angezeigt.

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Wenn Sie die Hardwareinventur für verteilte Ansichten verwenden, ist eine Integration in Desktop Analytics nicht möglich

<!-- 4950335 -->
*Gilt für: Configuration Manager, Version 1902 mit Updaterollup, sowie Version 1906*

Wenn Sie über eine Hierarchie verfügen und **Hardwareinventur**-Standortdaten für [verteilte Ansichten](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) für Standortreplikationslinks aktivieren, wird nach dem Konfigurieren der Desktop Analytics-Verbindung in Configuration Manager in M365UploadWorker.log die folgende Fehlermeldung angezeigt:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Deaktivieren Sie die **Hardwareinventur**-Standortdaten für verteilte Ansichten für jeden Standortreplikationslink, um dieses Problem zu umgehen.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>Konsole wird beim Entfernen von Sammlungen unerwartet geschlossen

<!-- 4749443 -->
*Gilt für: Configuration Manager Version 1902 mit Updaterollup*

Nach dem Herstellen einer Verbindung zwischen dem Standort und [Desktop Analytics](../../../../desktop-analytics/connect-configmgr.md) können Sie **bestimmte Sammlungen für die Synchronisierung mit Desktop Analytics auswählen**. Wenn Sie eine Sammlung entfernen und Änderungen anwenden, führt das sofortige Hinzufügen einer neuen Sammlung zu einem Ausnahmefehler. Die Konsole wird unerwartet geschlossen.

Um dieses Problem zu umgehen, klicken Sie beim Entfernen einer Sammlung auf **OK**, um das Eigenschaftenfenster zu schließen. Öffnen Sie dann die Eigenschaften erneut, um auf der Registerkarte **Desktop Analytics-Verbindung** eine neue Sammlung hinzuzufügen.

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>Kachel „Pilot status“ (Pilotstatus) zeigt mehrere Geräte als „undefined“ (nicht definiert) an

<!-- 4547783 -->
*Gilt für: Configuration Manager Version 1902 mit Updaterollup*

Wenn Sie die Configuration Manager-Konsole zum Überwachen des Pilotbereitstellungsstatus verwenden, werden Pilotgeräte, die in der Windows-Zielversion für diesen Bereitstellungsplan aktuell sind, auf der Kachel „Pilot status“ (Pilotstatus) als **undefined** (nicht definiert) angezeigt.  

Diese **nicht definierten** Geräte sind mit der Zielversion des Betriebssystems für diesen Bereitstellungsplan **auf dem neuesten Stand**. Es sind keine weiteren Aktionen erforderlich.

## <a name="cloud-services"></a>Clouddienste

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>Der Azure-Dienst für die US Government-Cloud wird als öffentliche Cloud angezeigt.

<!-- 6036748 -->

*Gilt für Version 1910*

Wenn Sie eine Verbindung mit einem Azure-Dienst herstellen und die **Azure-Umgebung** auf die Government-Cloud festlegen, wird in den Eigenschaften der Verbindung die Umgebung als öffentliche Azure-Cloud angezeigt. Dieses Problem ist nur ein Anzeigeproblem in der Konsole. Der Dienst befindet sich in der Government-Cloud. Führen Sie die folgende SQL-Abfrage für die Standortdatenbank aus, um die Konfiguration zu bestätigen:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

Für die Government-Cloud ist das Ergebnis dieser Abfrage für den jeweiligen Mandanten `2`.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Inhalt aus einem für TLS 1.2 aktivierten Cloud Management Gateway-Diensts kann nicht heruntergeladen werden

<!-- 5771680 -->

*Gilt für  1906, 1910 Early Update Ring*

Wenn Sie ein Cloud Management Gateway-Dienst (CMG) aktivieren, um **als ein Cloudverteilungspunkt zu fungieren und Inhalt aus Azure Storage zu verarbeiten** und **TLS 1.2** zu erzwingen, werden Sie möglicherweise sehen, dass die Downloads des Inhalts fehlschlagen.

Die folgenden Fehler werden in der Datei „DataTransferService.log“ auf dem Client angezeigt:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Die folgenden Fehler werden in der Datei „CMGContentService.log“ auf dem Client angezeigt:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

So umgehen Sie dieses Problem:

- Aktualisieren Sie den Standort auf die global verfügbare Version 1910, die am 20. Dezember 2019 veröffentlicht wurde. (Wenn Sie zuvor auf Early Update Ring 1910 aktualisiert haben, müssen Sie auf diesen Build aktualisieren, wenn er verfügbar ist.)

- Alternativ können Sie einen herkömmlichen [Cloudverteilungspunkt](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) verwenden. Diese Rolle erzwingt TLS 1.2 nicht, ist aber mit den Clients, die TLS 1.2 erfordern, kompatibel.

## <a name="protection"></a>Schutz

### <a name="bitlocker-management-appears-in-version-1906"></a>Die BitLocker-Verwaltung wird in Version 1906 angezeigt.

*Gilt für Version 1906*

<!-- 5984688 -->

Wenn Sie nach dem 21. November 2019 ein Update von Version 1902 oder früher auf Version 1906 durchführen, wird die BitLocker-Verwaltungsfunktion aktiviert und verfügbar. Diese Funktion ist ein optionales Feature ab Version 1910. Sie wird in Version 1906 nicht unterstützt. Wenn Sie versuchen, sie in Version 1906 zu verwenden, kann dies zu unerwarteten Ergebnissen führen. Wenn Sie die Funktion nicht verwenden, hat dies keine Auswirkungen.

Um die [BitLocker-Verwaltungsfunktion](../../../../protect/plan-design/bitlocker-management.md) zu verwenden, aktualisieren Sie auf Version 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
