---
title: UUP-Vorschau
titleSuffix: Configuration Manager
description: Anweisungen für die Vorschau der UUP-Integration
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702938"
---
# <a name="uup-private-preview-instructions"></a>Anweisungen für die private UUP-Vorschau

> [!Note]  
> Diese Informationen beziehen sich auf eine Previewfunktion, die sich vor ihrer kommerziellen Freigabe noch grundlegend ändern kann. Microsoft übernimmt bezüglich der hier bereitgestellten Informationen keine Gewährleistungen, weder ausdrücklich noch konkludent.  

## <a name="introduction"></a>Einführung

Die Unified Update Platform (UUP) ist die Verpackungs- und Veröffentlichungsplattform, die Consumer- und Unternehmensgeräte verwenden, um Updates von Windows Update for Business zu erhalten. Das private UUP-Vorschauprogramm ist für Kunden, die zugestimmt haben, Microsoft bei der Überprüfung der Verwendung von UUP-Updates in Configuration Manager zu helfen, um Probleme zu beheben, die Kunden heute bei der Wartung von Windows melden. Diese Updates sind zurzeit nicht öffentlich verfügbar.

Weitere Informationen zu UUP finden Sie im folgenden Windows-Blogbeitrag: [Update zu unserer Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Vorteile

Das UUP-Feature von Windows 10 und die kumulativen Updates tragen dazu bei, mehrere Probleme zu beheben, die Kunden heute bei der Wartung von Windows melden.

### <a name="feature-updates"></a>Featureupdates

- Bei einem Update des UUP-Features bewahrt der Windows Update-Prozess FOD- (Features on Demand) und Sprachpakete.

- Aktualisieren Sie direkt auf die neueste Ebene der Sicherheitskonformität. Sie müssen Sicherheitsupdates nicht sofort nach einem Featureupdate installieren. Microsoft veröffentlicht jeden Monat ein neues Featureupdate mit dem neuesten kumulativen Sicherheitsupdate. Sie müssen nicht jeden Monat den Großteil des Inhalts des Featureupdates herunterladen oder verteilen. Sie laden nur das Sicherheitsupdate herunter, das UUP mit dem kumulativen Update teilt.

### <a name="cumulative-updates"></a>Kumulative Updates

- Kumulative Updates mit UUP enthalten Updates für den Wartungsstapel (Servicing Stack Updates, SSUs) mit monatlichen kumulativen Sicherheitsupdates. Mit diesem Verhalten werden Probleme beim Orchestrieren dieser beiden Updates gelöst. Dabei wird sichergestellt, dass die Wartungsstapelupdates vorhanden sind, um kumulative Updates zu installieren. Sie brauchen diese Beziehungen nicht zu verwalten und zu orchestrieren.

- Kumulative Updates mit UUP ermöglichen es Ihnen, FOD- und Sprachpaketinhalte offline zu verteilen. Dieses Verhalten ermöglicht es Benutzern, sie bei Bedarf hinzuzufügen. Die Benutzer müssen nicht aus dem Internet herunterladen, und Sie müssen sich nicht überlegen, wie Sie diesen Inhalt vorab bereitstellen können.

## <a name="set-up"></a>Einrichtung

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. Ihre WSUS-ID an Microsoft senden

Teilen Sie Ihrem UUP-Vorschaukontakt Ihre WSUS-ID mit, um an der privaten UUP-Vorschau teilzunehmen. Microsoft nimmt Ihre WSUS-Umgebung in das UUP-Vorschauprogramm auf. Ohne diese ID werden Ihnen keine UUP-Updates angezeigt, bis die Vorschau in die öffentliche Phase eintritt.

Führen Sie das folgende PowerShell-Skript aus, um Ihre WSUS-ID zu erhalten:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

Die **MUUrl**-Eigenschaft muss `https://sws.update.microsoft.com` lauten. Informationen zum Ändern dieser Einstellung finden Sie im folgenden Supportartikel: [WSUS synchronization fails with SoapException (Fehler bei WSUS-Synchronisierung mit SoapException)](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. Configuration Manager aktualisieren

Nehmen Sie die folgenden Änderungen an Ihrem Configuration Manager-Standort vor, um diese UUP-Vorschau zu unterstützen:

#### <a name="diagnostics-and-usage-data-level"></a>Diagnose- und Nutzungsdatenebene

Während dieser Vorschau sollten Sie die Diagnose- und Datennutzungsebene für Configuration Manager erhöhen. Mit der Ebene **Full** (Vollständig) kann Microsoft mithilfe dieses neuen Features Probleme besser analysieren und behandeln. Weitere Informationen finden Sie unter [Sammlungsebenen von Nutzungsdaten zu Diagnosezwecken für Version 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>Installieren des neuesten Updates

1. Aktualisieren Sie die Website mit einem der folgenden Updates:

    - Version 1902 mit dem [Updaterollup](https://support.microsoft.com/help/4500571)
    - [Version 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Weitere Informationen finden Sie unter [Installieren konsoleninterner Updates](../../core/servers/manage/install-in-console-updates.md).

2. Aktualisieren der Clients  

    - Um diesen Prozess zu vereinfachen, sollten Sie automatische Clientupgrades in Betracht ziehen. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - Aktualisieren Sie alle Clients, für die Sie UUP-Updates ausführen möchten, um ein *unnötiges Herunterladen von ca. 6 GB* ungenutzter Inhalte auf den Client zu verhindern.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Windows-Clients auf eine unterstützte Version aktualisieren

Damit UUP-Updates erfolgreich installiert werden können, installieren Sie die beiden folgenden Updates:

1. Eine bestimmte kumulative monatliche Mindestkonformitätsebene.

2. Ein bestimmtes nicht kumulatives, Nicht-Sicherheitsupdate aus dem Microsoft Update-Katalog. Informationen zum Importieren des Updates in Configuration Manager für die Bereitstellung finden Sie unter [Importieren von Updates aus dem Microsoft Update-Katalog](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Unterstützte Versionen von Windows 10 und erforderliche Updates

| Windows 10-Version | Mindestkonformitätsebene | Zusätzliches Katalogupdate |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, Version 1903** | RTM | 7\. November 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, Version 1809** | August 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7\. November 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, Version 1803** | April 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7\. November 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, Version 1709** | April 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7\. November 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Wenn Sie die Updates vom 12. November 2019 auf den Client anwenden, bevor Sie das zusätzliche Katalogupdate vom 7. November 2019 anwenden, werden die zur Unterstützung von UUP erforderlichen Änderungen am Windows Update-Agent überschrieben. Wenden Sie das zusätzliche Katalogupdate an, nachdem die Updates vom 12. November 2019 installiert wurden, um Clients in diesem Szenario zu korrigieren.
> - Wenn Sie ein Featureupdate auf den Client anwenden, müssen Sie das zusätzliche Katalogupdate nach Abschluss des Upgrades erneut installieren.
> - Importieren Sie die Updates in Configuration Manager, um das Testen von Featureupdates zu erleichtern. Weitere Informationen finden Sie unter [Importieren von Updates aus dem Microsoft Update-Katalog](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). Nachdem das Featureupdate abgeschlossen ist, wird das zusätzliche Katalogupdate als **erforderlich** angezeigt, was die automatische Bereitstellung für die übergeordnete Betriebssystemversion ermöglicht.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)

Damit UUP-Updates ordnungsgemäß heruntergeladen werden können, aktivieren Sie die Clienteinstellung **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** . Diese Einstellung ermöglicht es Configuration Manager, den Windows Update-Agent (WUA) den erforderlichen Inhalt zum Herunterladen auf Clients bestimmen zu lassen. Dieses Verhalten ist nicht das Standardverhalten, bei dem der Configuration Manager-Client alle mit dem UUP-Update verbundenen Inhalte herunterlädt. Wenn Sie diese Einstellung aktivieren, ermittelt der WUA bei jedem UUP-Update den zusätzlich erforderlichen Inhalt. Beispielsweise nur die erforderlichen FOD- und Sprachpakete.

Wenn Sie diese Einstellung aktivieren, hat dies keine Auswirkungen auf Downloads von Serverinhalten aus dem Internet. Dies gilt nur für Clientdownloads. Bevor Sie UUP-Updates auf Clients bereitstellen, wenden Sie diese Einstellung auf Clients an, die den unterstützten Versionen für UUP entsprechen. Die erforderlichen Clientupdates beheben Kompatibilitätsprobleme für UUP-Updates in WSUS und Configuration Manager.

Weitere Informationen zu dieser Clienteinstellung finden Sie unter [Informationen zu Clienteinstellungen – Softwareupdates](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available).

### <a name="5-review-your-software-update-infrastructure"></a>5. Softwareupdateinfrastruktur überprüfen

Bevor Sie UUP-Updates synchronisieren, überprüfen Sie Ihre Regeln für die automatische Bereitstellung (ADR) und Wartungspläne. Wenn Sie nicht möchten, dass diese Updates automatisch bereitgestellt werden, überarbeiten Sie Ihre ADRs, um sie herauszufiltern. Weitere Informationen finden Sie unter [Auffinden von synchronisierten UUP-Updates](#how-to-find-synced-uup-updates). Standardmäßig werden bei bestehenden Wartungsplänen nur Nicht-UUP-Updates bereitgestellt. Sie können die Wartungspläne modifizieren, um dieses Verhalten zu ändern.

Überprüfen Sie Ihre Konformitätsberichte, und überarbeiten Sie sie bei Bedarf. Wenn Sie z. B. die produktübergreifende Konformität messen, werden jetzt sowohl kumulative UUP- als auch Nicht-UUP-Updates angezeigt. Die Geräte melden die Konformität mit beiden Arten von Updates. Stellen Sie sicher, dass Ihre Konformitätsberichte diese Änderung berücksichtigen.

## <a name="enable-uup-and-start-testing"></a>Aktivieren von UUP und Beginnen mit Tests

### <a name="select-products-and-classifications-to-sync"></a>Wählen Sie Produkte und Klassifikationen zur Synchronisierung aus.

Sobald Sie bereit sind, mit der Synchronisierung von UUP-Updates zu beginnen, und Microsoft Ihre WSUS-ID genehmigt hat, aktivieren Sie die neuen Produkte:

1. [Synchronisieren Sie Softwareupdates](../get-started/synchronize-software-updates.md), um die neuen Produkte aufzufüllen.  

2. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.

3. Wählen Sie den Standort auf oberster Ebene aus. Dabei handelt es sich entweder um einen zentralen Verwaltungsstandort (Central Administration Site, CAS) oder um einen eigenständigen primären Standort.

4. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.

5. Wechseln Sie zur Registerkarte **Produkte**, und wählen Sie eines oder mehrere der folgenden Produkte aus: 

    - **Windows 10 UUP Preview**
    - **Windows Server UUP Preview**

6. Wechseln Sie zur Registerkarte **Klassifizierungen**, und wählen Sie die folgenden Optionen aus:  

    - **Sicherheitsupdates**: So zeigen Sie die kumulativen UUP-Updates an  
    - **Upgrades**: zum Anzeigen der UUP-Featureupdates.  

7. Synchronisieren Sie die Softwareupdates erneut, um die neuen UUP-Updates anzuzeigen.

### <a name="how-to-find-synced-uup-updates"></a>Auffinden von synchronisierten UUP-Updates

Nachdem Sie UUP-Updates in Ihre Umgebung synchronisiert haben, finden Sie diese in der Configuration Manager-Konsole zum Testen. Es gibt zwei Möglichkeiten, die Vorschauupdates zu finden:

- Da diese Vorschauupdates in einem separaten Produkt enthalten sind, verwenden Sie das Produkt zum Filtern, um diese Updates zu finden. Verwenden Sie den Produktfilter des Wartungsplans, um entweder UUP- oder Nicht-UUP-Featureupdates bereitzustellen.  

- In den Knoten **Alle Softwareupdates** und **Alle Windows 10-Updates** der **Softwarebibliothek** befindet sich eine neue optionale Spalte namens **Tag**. Diese Eigenschaft steht auch als Filter in ADRs zur Verfügung. Suchen Sie für UUP-Updates in diesem Feld nach `UUP`. Für Nicht-UUP-Updates ist es leer.  

### <a name="updates-available-during-preview"></a>Während der Vorschauphase verfügbare Updates

Weitere Informationen zu allen von Microsoft veröffentlichten Windows 10-Updates finden Sie unter [Versionsinformationen zu Windows 10](https://docs.microsoft.com/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Zu testende kumulative Updates

Obwohl möglicherweise mehrere mit UUP-gekennzeichnete Updates verfügbar sind, beginnen Sie mit dem Update **September 2019** (2019-09) oder einer späteren Version. Beispiel:

- 2019-09 Kumulatives Update für Windows 10, Version 1809, für x64-basierte Systeme (KB4512578)
- 2019-09 Kumulatives Update für Windows 10, Version 1803, für x64-basierte Systeme (KB4516058)
- 2019-09 Kumulatives Update für Windows 10, Version 1709, für x64-basierte Systeme (KB4516066)

#### <a name="feature-updates-to-test"></a>Zu testende Featureupdates

Obwohl möglicherweise mehrere mit UUP-gekennzeichnete Updates verfügbar sind, beginnen Sie mit dem Update **September 2019** (2019-09B) oder einer späteren Version. Beispiel:

- Featureupdate für Windows 10, Version 1809, x64 2019-09B
- Featureupdate für Windows 10, Version 1803, x64 2019-09B

## <a name="scenarios-to-test"></a>Zu testende Szenarien

### <a name="test-feature-updates"></a>Testen von Featureupdates

- Aktualisieren Sie direkt auf die gewählte Ebene der Sicherheitskonformität.  

- Installieren Sie vor dem Update FOD- und Sprachpakete. Stellen Sie sicher, dass diese Komponenten beim Update erhalten bleiben.  

### <a name="test-cumulative-updates"></a>Testen von kumulativen Updates

Halten Sie während der Vorschauphase Clients konform, indem Sie den UUP-Typ von Updates für mehrere aufeinander folgende Updates verwenden. Dieser Test hilft Ihnen, das anhaltende Verhalten zu verstehen.

### <a name="test-content"></a>Testinhalt

Das erste Update für die einzelnen Hauptversionen (1809, 1803, 1709), die Architektur und die Sprachkombination wird umfangreich erscheinen. Diese Größe bezieht sich sowohl auf die Anzahl der Dateien als auch auf den Speicherplatz im Vergleich zu dem, was Sie zuvor bei Nicht-UUP-Updates gesehen haben. Dieser zusätzliche Inhalt ist in erster Linie für alle FOD- und Sprachpakete für kumulative Updates gedacht. Für Featureupdates gibt es weitere umfangreiche Inhalte für dieses erste Update.

Für zukünftige kumulative und Featureupdates ist der Umfang der neuen Inhalte, die von der Website heruntergeladen und verteilt werden, viel geringer. UUP teilt auf intelligente Weise alle FOD- und Sprachpaketinhalte zwischen den Updates. Es ist nicht erforderlich, diesen freigegebenen Inhalt neu herunterzuladen oder weiterzuverteilen. Während der Vorschau, in Windows 10 Versionen 1709 und 1803, entspricht dieser monatliche Download ungefähr der Größe der kumulativen Updates in Nicht-UUP-Szenarien. In Windows 10 Version 1809 und höher ist der inkrementelle Download für das kumulative Update jeden Monat viel geringer.

Wenn Sie sich den gesamten Inhalt ansehen, der heruntergeladen und über einen Zeitraum von 12 Monaten für *Nicht-Expressinhalte* verteilt wurde, sollte die Version 1803 von Windows 10 ohne UUP etwa gleich groß sein wie die Version 1809 mit UUP. Der gesamte heruntergeladene und über die gesamte Lebensdauer der Version verteilte Inhalt ist in der Version 1809 mit UUP kleiner.

### <a name="supported-content-channels"></a>Unterstützte Inhaltskanäle

Testen Sie für die Vorschau Ihre typischen realen Szenarien. UUP unterstützt alle Inhaltskanäle, einschließlich:

- Windows-Übermittlungsoptimierung (Delivery Optimization, DO)
  - Wenn Sie die Übermittlungsoptimierung verwenden, stellen Sie sicher, dass sie ordnungsgemäß konfiguriert ist. Weitere Informationen finden Sie unter [Optimieren der Bereitstellung von Updates für Windows 10](optimize-windows-10-update-delivery.md).
- Configuration Manager-Peercache
- Windows BranchCache
- Verwenden Sie die Option **Kein Bereitstellungspaket**, damit die Clients direkt von Microsoft Update herunterladen. Verwenden Sie diese Option mit der Übermittlungsoptimierung.
- Alternative Drittanbieter von Inhalten

Weitere Informationen zu Inhaltskanälen finden Sie unter [Optimieren der Bereitstellung von Updates für Windows 10](optimize-windows-10-update-delivery.md).

<!-- TODO: Addlink to WSUS Perf documentation-->
