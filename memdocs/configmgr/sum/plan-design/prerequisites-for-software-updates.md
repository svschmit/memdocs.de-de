---
title: Voraussetzungen für Softwareupdates
titleSuffix: Configuration Manager
description: Lernen Sie die Voraussetzungen für Softwareupdates in Configuration Manager kennen.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: a870d2bf18b9e7f064e914f450aee0f5e3e2e545
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906716"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Voraussetzungen für Softwareupdates in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden die Voraussetzungen für Softwareupdates in Configuration Manager beschrieben. Die externen und internen Voraussetzungen sind jeweils in separaten Tabellen aufgeführt.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Externe Softwareupdateabhängigkeiten von Configuration Manager  
 In den folgenden Abschnitten sind die externen Abhängigkeiten für Softwareupdates aufgeführt.  

### <a name="internet-information-services"></a>Internetinformationsdienste  
 Die Internetinformationsdienste (Internet Information Services, IIS) müssen zum Ausführen des Softwareupdate-, Verwaltungs- und Verteilungspunkts auf den Standortsystemservern installiert sein. Weitere Informationen finden Sie unter [Prerequisites for site system roles (Voraussetzungen für Standortsystemrollen)](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) ist zur Synchronisierung von Softwareupdates und für die Anwendbarkeit von Softwareupdates auf Clients erforderlich. Der WSUS-Server muss installiert werden, bevor Sie die Rolle „Softwareupdatepunkt“ erstellen können. Für einen Softwareupdatepunkt werden die folgenden Versionen von WSUS unterstützt:  

- WSUS 10.0.14393 (Rolle in Windows Server 2016)
- WSUS 10.0.17763 (Rolle in Windows Server 2019) (erfordert Configuration Manager 1810 oder höher)
- WSUS 6.2 und 6.3 (Rolle in Windows Server 2012 und Windows Server 2012 R2)
  - Für WSUS 6.2 und 6.3 werden [KB 3095113 und KB 3159706 (oder ein entsprechendes Update)](#BKMK_wsus2012) benötigt, wenn Sie Windows 10-Upgrades bereitstellen.

> [!NOTE]
> - Stellen Sie bei Verwendung mehrerer Softwareupdatepunkte an einem Standort sicher, dass jeweils die gleiche WSUS-Version ausgeführt wird.

### <a name="wsus-administration-console"></a>WSUS-Verwaltungskonsole  
Die WSUS-Verwaltungskonsole wird auf dem Configuration Manager-Standortserver benötigt, wenn sich der Softwareupdatepunkt auf einem Remote-Standortsystemserver befindet und auf dem Standortserver noch keine WSUS-Installation vorhanden ist.  

> [!IMPORTANT]  
> - Die WSUS-Version auf dem Standortserver muss der WSUS-Version entsprechen, die auf den Softwareupdatepunkten ausgeführt wird.
> - Verwenden Sie nicht die WSUS-Verwaltungskonsole zum Konfigurieren der WSUS-Einstellungen. Configuration Manager stellt eine Verbindung mit der WSUS-Instanz auf dem Softwareupdatepunkt her, und die entsprechenden Einstellungen werden konfiguriert.  


### <a name="windows-update-agent"></a>Windows Update-Agent  
 Der Client vom Windows Update-Agent (WUA) ist auf Clients erforderlich, damit sie eine Verbindung mit dem WSUS-Server herstellen können. WUA ruft die Liste der Softwareupdates ab, die auf Konformität überprüft werden müssen.  

 Während der Installation von Configuration Manager wird die aktuelle WUA-Version heruntergeladen. Bei Bedarf wird für WUA ein Upgrade ausgeführt, wenn Sie den Configuration Manager-Client installieren. Wenn bei der Installation Fehler auftreten, müssen Sie ein anderes Verfahren zum Ausführen des WUA-Upgrades verwenden.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Interne Softwareupdateabhängigkeiten von Configuration Manager  
 In der folgenden Abschnitten sind die internen Abhängigkeiten für Softwareupdates in Configuration Manager aufgeführt.  

### <a name="management-points"></a>Verwaltungspunkte  
 Informationen zwischen Clientcomputern und dem Configuration Manager-Standort werden über Verwaltungspunkte übertragen. Diese Verwaltungspunkte sind für Softwareupdates erforderlich.  

### <a name="software-update-points"></a>Softwareupdatepunkte  
 Sie müssen einen Softwareupdatepunkt auf dem WSUS-Server installieren, um Softwareupdates in Configuration Manager bereitstellen zu können. Weitere Informationen finden Sie unter [Install and configure a software update point (Installieren und Konfigurieren eines Softwareupdatepunkts)](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Verteilungspunkte  
 Verteilungspunkte sind erforderlich, um den Inhalt für Softwareupdates zu speichern. Weitere Informationen zum Installieren von Verteilungspunkten und Verwalten von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Clienteinstellungen für Softwareupdates  
Softwareupdates sind standardmäßig für Clients aktiviert. Es stehen außerdem noch weitere Einstellungen zur Verfügung, mit denen gesteuert wird, wie und wann von Clients die Kompatibilität für die Softwareupdates überprüft wird und wie die Softwareupdates installiert werden.  

 Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Clienteinstellungen für Softwareupdates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Softwareupdates-Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services-Punkte  
 Mithilfe der Standortsystemrolle Reporting Services-Punkt können Berichte für Softwareupdates angezeigt werden. Diese Rolle ist optional. Ihre Verwendung wird jedoch empfohlen. Weitere Informationen zum Erstellen eines Reporting Services-Punkts finden Sie unter [Konfigurieren der Berichterstellung](../../core/servers/manage/configuring-reporting.md).  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a> Welche Updates sind in WSUS 6.2 und 6.3 erforderlich?

Für die Synchronisierung der Klassifizierung **Aktualisierungen** in WSUS 6.2 und 6.3 sind zwei Updates erforderlich. Gelegentlich wird möglicherweise ein Fehler beim Herunterladen oder Bereitstellen von Upgrades angezeigt, wenn sie vor der Installation von KB3095113 und KB3159706 synchronisiert wurden. Informationen zu möglichen Problemen finden Sie im nächsten Abschnitt.  

- Sie müssen [KB 3095113](https://support.microsoft.com/kb/3095113) (im Oktober 2015 veröffentlicht) auf Ihren Softwareupdatepunkten und Standortservern installieren, bevor Sie die Klassifikation **Upgrades** synchronisieren.
  - Dieses Update aktiviert die Klassifizierung **Aktualisierungen**.
- Für Windows 10, Version 1607 und höher müssen Sie [KB 3159706](https://support.microsoft.com/help/3159706) installieren und konfigurieren. KB 3159706 wurde im Mai 2016 veröffentlicht.
  - Mit diesem Update kann WSUS die Dateien, mit denen Windows 10 ab Version 1607 aktualisiert wird, nativ entschlüsseln.

>[!IMPORTANT]
> Sowohl KB 3095113 als auch KB 3159706 sind ab Juli 2017 im **monatlichen Sicherheits- und Qualitätsrollup** enthalten. Dies bedeutet, dass KB 3095113 und KB 3159706 möglicherweise nicht als installierte Updates angezeigt werden, da sie unter Umständen mit einem Rollup installiert wurden. Wenn Sie jedoch eines dieser beiden Updates benötigen, empfiehlt es sich, ein **monatliches Sicherheits- und Qualitätsrollup** zu installieren, das nach Oktober 2017 veröffentlicht wurde, da diese Updates ein zusätzliches WSUS-Update enthalten, das die Arbeitsspeicherverwendung des ClientWebService von WSUS verringert.

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a> Das Herunterladen von Windows 10-Upgrades schlägt mit "Fehler: Ungültige Zertifikatsignatur“ oder 0xc1800118 fehl.

Die in diesem Abschnitt beschriebenen Updates und Probleme betreffen nur WSUS-Versionen, die auf Windows Server 2012- oder Windows Server 2012 R2-Computern (WSUS 6.2 und 6.3) ausgeführt werden. Üblicherweise treten die in diesem Abschnitt beschriebenen Probleme nur auf, wenn Sie WSUS vor Juli 2017 installiert und kürzlich die Klassifizierung **Aktualisierungen** aktiviert haben. Es ist jedoch möglich, dass diese Probleme auch in anderen Situationen auftreten.

### <a name="historical-information-about-kb-3095113"></a>Verlaufsinformationen zu KB 3095113

 [KB 3095113](https://support.microsoft.com/kb/3095113) wurde im Oktober 2015 [als Hotfix veröffentlicht](https://docs.microsoft.com/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113), um auch Windows 10-Upgrades für WSUS zu unterstützen. Mit diesem Update kann WSUS Updates in der Klassifizierung **Aktualisierungen** für Windows 10 synchronisieren und verteilen.

Wenn Sie Upgrades synchronisieren, ohne zuerst [KB 3095113](https://support.microsoft.com/kb/3095113) installiert zu haben, füllen Sie die WSUS-Datenbank (SUSDB) mit unbrauchbaren Daten auf. Diese Daten müssen gelöscht werden, bevor Upgrades ordnungsgemäß bereitgestellt werden können. Windows 10-Upgrades in diesem Zustand können nicht mithilfe des Assistenten zum Herunterladen von Softwareupdates heruntergeladen werden.

Fehler, die dem folgenden ähneln, werden auf der Abschlussseite des Assistenten zum Herunterladen von Softwareupdates angezeigt:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Außerdem werden Fehler, die dem folgenden ähneln, in der Datei „PatchDownloader.log“ protokolliert:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Wenn diese Fehler in der Vergangenheit auftraten, wurden sie durch eine geänderte Version der [Lösungsschritte für WSUS](https://docs.microsoft.com/archive/blogs/wsus/how-to-delete-upgrades-in-wsus) behoben. Da diese Schritte denen ähneln, die nach der Installation von KB 3159706 zum Vermeiden der manuellen Lösungsschritte erforderlich sind, wurden beide Lösungen im folgenden Abschnitt kombiniert:

- [Wiederherstellen nach Synchronisierung der Upgrades vor der Installation von KB 3095113 oder KB 3159706](#bkmk_fix-upgrades)

### <a name="historical-information-about-kb-3159706"></a>Verlaufsinformationen zu KB 3159706

KB 3148812 wurde ursprünglich im April 2016 veröffentlicht, damit WSUS die für das Upgrade von Windows 10-Paketen erforderlichen ESD-Dateien nativ entschlüsseln kann. [KB 3148812 verursachte jedoch bei einigen Kunden Probleme](https://docs.microsoft.com/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues) und wurde durch [KB 3159706](https://support.microsoft.com/help/3159706) ersetzt. KB 3159706 muss auf allen Softwareupdatepunkten und Standortservern installiert sein, bevor Sie Geräte mit Windows 10, Version 1607 und höher bedienen können. Es können jedoch Probleme auftreten, wenn Sie nicht wissen, dass für das Update nach der Installation die folgenden manuellen Schritte anfallen:

1. Führen Sie `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` über eine Eingabeaufforderung mit erhöhten Rechten aus.
1. Starten Sie den WSUS-Dienst auf allen WSUS-Servern neu.

Wenn Sie nicht wissen, dass für KB 3159706 nach der Installation manuelle Schritte erforderlich waren, oder Sie das Upgrade für Windows 10, Version 1607 vor der Installation von KB 3159706 synchronisiert haben, treten jeweils beim Herstellen einer Verbindung mit der WSUS-Konsole und der Bereitstellung des Upgrades Probleme auf. Wenn ein Client die Upgradedatei heruntergeladen hat, würde er einen [Fehlercode **0xC1800118**](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus) erhalten.

Da die Lösungsschritte denen der Lösung für das Synchronisieren von Upgrades vor der Installation von KB 3095113 ähneln, wurden alle Schritte im nächsten Abschnitt zu einer einzigen Lösung zusammengeführt.
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>Wiederherstellen nach Synchronisierung der Upgrades vor der Installation von KB 3095113 oder KB 3159706

Führen Sie die folgenden Schritte zur Behebung von Fehlern des Typs „0xc1800118“ und „Fehler: Ungültige Zertifikatsignatur“ aus.

1. Deaktivieren Sie die Klassifizierung **Aktualisierungen** sowohl in WSUS als auch in Configuration Manager. Sie sollten keine Synchronisierung ausführen, bevor diese Anleitung Sie nicht dazu auffordert.  
   - Deaktivieren Sie die Klassifizierung **Upgrades** in den Eigenschaften der Softwareupdatepunktkomponente auf dem Standort oberster Ebene.
     - Weitere Informationen finden Sie unter [Konfigurieren von Klassifizierungen und Produkten](../get-started/configure-classifications-and-products.md).
   - Deaktivieren Sie auf der [Seite **Optionen**](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations) unter **Produkte und Klassifikationen** die WSUS-Klassifizierung **Aktualisierungen**, oder verwenden Sie die PowerShell ISE, die als Administrator ausgeführt werden muss.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - Wenn Sie die WSUS-Datenbank für mehrere WSUS-Server freigeben, müssen Sie die Klassifizierung **Aktualisierungen** für jede Datenbank einzeln deaktivieren.  
1. Führen Sie auf jedem WSUS-Server in einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`. Starten Sie dann den WSUS-Dienst auf allen WSUS-Servern neu.
   -  WSUS versetzt die Datenbank in den [Einzelbenutzermodus](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode), bevor überprüft wird, ob eine Wartung erforderlich ist. Die Wartung wird entweder auf Grundlage der Überprüfungsergebnisse oder unabhängig davon ausgeführt. Anschließend wird die Datenbank wieder in den Mehrbenutzermodus versetzt. 
   - Wenn Sie die WSUS-Datenbank für mehrere WSUS-Server freigeben, müssen Sie diese Wartung nur einmal für jede Datenbank durchführen.
1. Löschen Sie mithilfe der PowerShell ISE, die als Administrator ausgeführt wird, alle Windows 10-Upgrades aus den einzelnen WSUS-Datenbanken.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Löschen Sie Dateien aus der Tabelle „tbFile“ aus jeder der von Ihren Softwareupdatepunkten verwendeten WSUS-Datenbanken. Führen Sie in der WSUS-Datenbank die folgenden Befehle aus SQL Server Management Studio aus:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Starten Sie in Configuration Manager die Synchronisierung von Softwareupdates am Standort der obersten Ebene, und warten Sie, bis der Vorgang beendet ist. Eine vollständige Synchronisierung erfolgt, weil eine Änderung an den Klassifizierungen in Configuration Manager vorgenommen wurde, als **Upgrades** entfernt wurde. (Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates](../get-started/synchronize-software-updates.md).)
1. Wählen Sie die Klassifizierung **Upgrades** in den Eigenschaften der Softwareupdatepunktkomponente aus. Starten Sie anschließend eine weitere Softwareupdatesynchronisierung, um **Aktualisierungen** in WSUS und „Upgrades“ in Configuration Manager zurückzuholen. Sie müssen die Klassifizierung **Aktualisierungen** in WSUS nicht aktivieren, da Configuration Manager dies für Sie erledigt.
1. Wenn Ihre Clients beim Herunterladen eines Upgrades den Fehlercode **0xc1800118** erhalten haben, müssen Sie den Datenspeicher löschen, der vom Windows Update-Agent verwendet wird. Möglicherweise müssen Sie auch den ausgeblendeten Ordner „~BT“ auf dem Gerät löschen. Wenn der Client das nächste Mal eine Überprüfung ausführt, ist es eine vollständige anstelle einer Delta-Überprüfung des WSUS-Servers. Sie können ein PowerShell-Skript ähnlich dem folgenden Beispielskript verwenden:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Nächste Schritte
[Vorbereiten der Softwareupdateverwaltung](../get-started/prepare-for-software-updates-management.md)
