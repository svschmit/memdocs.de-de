---
title: Hotfixinstallationsprogramm
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wann und wie Updates über das Hotfixinstallationsprogramm für Configuration Manager installiert werden.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8eed671b723091f2a43350f42ca82d90e0d9da3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906132"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Verwenden des Hotfixinstallationsprogramms zum Installieren von Updates für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Einige Updates für Configuration Manager sind nicht beim Microsoft-Clouddienst, sondern nur über den Out-of-Band-Zugriff verfügbar. Ein Beispiel ist ein Hotfix, dass mit Einschränkungen herausgegeben wird, um ein bestimmtes Problem zu beheben.   
Wenn Sie ein Update (oder einen Hotfix) installieren müssen, das/den Sie von Microsoft erhalten haben, und dieses Update hat einen Dateinamen mit der Erweiterung **.exe** (nicht **update.exe**), verwenden Sie das in diesem Hotfixdownload enthaltene Hotfixinstallationsprogramm, um das Update direkt auf dem Configuration Manager-Standortserver zu installieren.  

Informationen für den Fall, dass die Hotfixdatei über die Dateierweiterung **.update.exe** verfügt, finden Sie unter [Verwenden des Tools zur Updateregistrierung, um Hotfixes in Configuration Manager zu importieren](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
> Dieses Thema enthält allgemeine Informationen zum Installieren von Hotfixes, die Configuration Manager aktualisieren. Einzelheiten zu einem bestimmten Update finden Sie im entsprechenden Knowledge Base-Artikel (KB) auf der Microsoft Support-Website.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a> Übersicht über die Hotfixes für Configuration Manager  
Hotfixes für Configuration Manager ähneln denen für andere Microsoft-Produkte, wie z.B. SQL Server, enthalten entweder eine einzelne Lösung oder ein Paket (ein Updaterollup von Fehlerbehebungen) und werden in einem Microsoft Knowledge Base-Artikel beschrieben.  

Einzelne Updates umfassen ein einzelnes fokussiertes Update für eine bestimmte Version von Configuration Manager aktualisiert wird.  
Updatepakete enthalten mehrere Updates für eine bestimmte Version von Configuration Manager.  
Wenn ein Update als Paket vorliegt, können Sie keine einzelnen Updates aus diesem Paket installieren.  

Wenn Sie beabsichtigen, Bereitstellungen zur Installation von Updates auf weiteren Computern zu erstellen, müssen Sie das Updatepaket auf einem Standortserver der zentralen Verwaltung oder auf einem primären Standortserver installieren.  

Wenn Sie das Updatepaket ausführen, geschieht Folgendes:  

- Die Updatedateien jeder betreffenden Komponente werden aus dem Updatepaket extrahiert.  

- Es wird ein Assistent gestartet, der Sie durch die Schritte zur Konfiguration der Updates und Bereitstellungsoptionen für die Updates führt.  

- Nachdem Sie den Assistenten abgeschlossen haben, werden die im Paket enthaltenen Updates, die für den Standortserver relevant sind, auf dem Standortserver installiert.  

Vom Assistenten werden auch Bereitstellungen erstellt, mit denen Sie die Updates auf weiteren Computern installieren können. Zum Bereitstellen der Updates auf weiteren Computern bedienen Sie sich einer unterstützten Bereitstellungsmethode. Dazu gehören beispielsweise Softwarebereitstellungspakete oder Microsoft System Center Updates Publisher 2011.  

Bei der Ausführung des Assistenten wird auf dem Standortserver eine **.cab** -Datei erstellt, die für Updates Publisher 2011 vorgesehen ist. Optional können Sie den Assistenten so konfigurieren, dass zusätzlich mindestens ein Paket für die Softwarebereitstellung erstellt wird. Mit diesen Bereitstellungen können Sie Updates auf Komponenten installieren, z.B. auf Clients oder der Configuration Manager-Konsole. Auf Computern, auf denen der Configuration Manager-Client nicht ausgeführt wird, können Sie Updates auch manuell installieren.  

Die folgenden drei Gruppen in Configuration Manager können aktualisiert werden:  

- Folgende Configuration Manager-Serverrollen:  

  - Standort der zentralen Verwaltung  

  - Primärer Standort  

  - Sekundärer Standort  

  - SMS-Remoteanbieter  

- Configuration Manager-Konsole  

- Configuration Manager-Client  

> [!NOTE]  
> **Updates für Standortsystemrollen** (einschließlich Updates für die Standortdatenbank und cloudbasierte Verteilungspunkte) werden als Teil des Updates für Standortserver und Dienste vom Standortkomponenten-Manager installiert.  
>   
> Updates-Pullverteilungspunkte werden jedoch vom Verteilungs-Manager anstelle des Standortkomponenten-Managers abgewickelt.  

Jedes Updatepaket für Configuration Manager ist eine selbstextrahierende EXE-Datei (SFX). Diese Datei enthält alle Dateien, die zur Installation des Updates auf den entsprechenden Komponenten von Configuration Manager erforderlich sind. Die SFX-Datei kann in der Regel die folgenden Dateien enthalten:  

|Datei|Details|  
|----------|-------------|  
|&lt;Produktversion\>-QFE-KB&lt;KB-Artikel-ID\>-&lt;Plattform\>-&lt;Sprache\>.exe|Dies ist die Updatedatei. Die Befehlszeile für diese Datei wird von Updatesetup.exe verwaltet.<br /><br /> Beispiel:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Dieser MSI-Wrapper dient dazu, die Installation des Updatepakets zu verwalten.<br /><br /> Bei der Ausführung des Updates wird die Anzeigesprache des jeweiligen Computers von Updatesetup.exe erkannt. Die Benutzeroberfläche für das Update ist standardmäßig englisch. Wenn aber die Anzeigesprache unterstützt wird, wird die Benutzeroberfläche in der lokalen Sprache des Computers angezeigt.|  
|License_&lt;Sprache\>.rtf|Jedes Update enthält mindestens eine Lizenzdatei für unterstützte Sprachen, sofern zutreffend.|  
|&lt;Produkt&Updatetyp>-&lt;Produktversion\>-&lt;KB-Artikel-ID\>-&lt;Plattform\>.msp|Wenn das Update für die Configuration Manager-Konsole oder Clients gilt, enthält das Updatepaket separate Windows Installer-Patchdateien (MSP).<br /><br /> Beispiel:<br /><br /> **Configuration Manager-Konsolenupdate:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Clientupdate:** ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

Die Aktionen des Updatepakets werden standardmäßig in einer LOG-Datei auf dem Standortserver erfasst. Die Protokolldatei trägt den gleichen Namen wie das Updatepaket und wird im Ordner **%SystemRoot%/Temp** abgelegt.  

Bei der Ausführung des Updatepakets wird eine Datei unter dem gleichen Namen wie das Updatepaket in einem temporären Ordner auf dem Computer gespeichert. Anschließend wird Updatesetup.exe ausgeführt. „Updatesetup.exe“ startet das Softwareupdate für den Configuration Manager &lt;Produktversion\> &lt;KB-Nummer\>-Assistenten.  

Dem Umfang des Updates entsprechend erstellt der Assistent auf dem Standortserver eine Reihe von Ordnern im Installationsordner von Configuration Manager. Die Ordnerstruktur sieht etwa folgendermaßen aus:   
**\\\\&lt;Servername\>\SMS_&lt;Standortcode\>\Hotfix\\&lt;KB-Nummer\>\\&lt;Updatetyp\>\\&lt;Plattform\>** .  

Die folgende Tabelle enthält Einzelheiten zu den Ordnern in der Ordnerstruktur:  

|Ordnername|Weitere Informationen|  
|-----------------|----------------------|  
|&lt;Servername\>|Dies ist der Name des Standortservers, auf dem Sie das Updatepaket ausführen.|  
|SMS_&lt;Standortcode\>|Dies ist der Freigabename des Configuration Manager-Installationsordners.|  
|&lt;KB-Nummer\>|Dies ist die Nummer des Knowledge Base-Artikels für dieses Updatepaket.|  
|&lt;Updatetyp\>|Dies sind die Updatetypen für Configuration Manager. Für jeden Updatetyp, der sich im Updatepaket befindet, wird vom Assistenten ein separater Ordner angelegt. Welchen Updatetyp ein Ordner enthält, ist am Ordnernamen erkennbar. Dazu gehören:<br /><br /> **Server:** Dieser Ordner enthält Updates für Standortserver, Standortdatenbankserver und Computer, auf denen der SMS-Anbieter ausgeführt wird.<br /><br /> **Client:** Dieser Ordner enthält Updates für den Konfigurations-Manager-Client.<br /><br /> **AdminConsole:** Dieser Ordner enthält Updates für die Configuration Manager-Konsole.<br /><br /> Zusätzlich zu den bereits genannten Updatetypen wird vom Assistenten ein Ordner namens **SCUP**erstellt. Dieser Ordner stellt keinen Updatetyp dar, sondern enthält die CAB-Datei für Updates Publisher.|  
|&lt;Plattform\>|Dies ist ein plattformspezifischer Ordner. Er enthält Updatedateien für einen bestimmten Prozessortyp.  Dazu gehören:<br /><br />- x64<br /><br /> - I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Installieren von Updates  
Zum Installieren von Updates müssen Sie zuerst das Updatepaket auf einem Standortserver installieren. Beim Installieren eines Updatepakets wird ein Installationsassistent für dieses Update gestartet. Dieser Assistent dient zu Folgendem:  

- Extrahieren der Updatedateien  

- Leichteres Konfigurieren von Bereitstellungen  

- Installieren der anwendbaren Updates auf den Serverkomponenten des lokalen Computers  

Nach der Installation des Updatepakets auf einem Standortserver können Sie weitere Komponenten für Configuration Manager aktualisiert wird. Die folgende Tabelle enthält eine Übersicht über die Updateaktionen für die verschiedenen Komponenten:  

|Komponente|Anweisungen|  
|---------------|------------------|  
|Standortserver|Stellen Sie Updates für einen Remotestandortserver bereit, wenn Sie sich dazu entscheiden, das Updatepaket nicht direkt auf diesem Remotestandortserver zu installieren.|  
|Standortdatenbank|Stellen Sie für Remotestandortserver Serverupdates bereit, die ein Update der Standortdatenbank umfassen, wenn Sie das Updatepaket nicht direkt auf diesem Remotestandortserver installieren.|  
|Configuration Manager-Konsole|Nach der Erstinstallation der Configuration Manager-Konsole können Sie auf jedem Computer, auf dem die Konsole ausgeführt wird, Updates für die Configuration Manager-Konsole installieren. Sie können die Installationsdateien für die Configuration Manager-Konsole nicht dahingehend ändern, dass die Updates bei der Erstinstallation der Konsole angewendet werden.|  
|SMS-Remoteanbieter|Installieren Sie Updates für jede Instanz des SMS-Anbieters, der auf einem anderen Computer als dem Standortserver, auf dem Sie das Updatepaket installiert haben, ausgeführt wird.|  
|Configuration Manager-Clients|Nach der Erstinstallation des Configuration Manager-Clients können Sie auf jedem Computer, auf dem der Client ausgeführt wird, Updates für den Configuration Manager-Client installieren.|  

> [!NOTE]  
> Sie können Updates nur auf Computern bereitstellen, auf denen der Configuration Manager-Client nicht ausgeführt wird, können Sie Updates auch manuell installieren.  

Wenn Sie einen Client, die Configuration Manager-Konsole oder den SMS-Anbieter erneut installieren, müssen Sie auch die Updates für diese Komponenten erneut installieren.  

Verwenden Sie die Informationen in den folgenden Abschnitten, um für jede der Komponenten von Configuration Manager Updates zu installieren.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Aktualisieren von Servern  
Updates für Server können Updates für **Standorte**, die **site database**und Computer, auf denen eine Instanz des **SMS-Anbieters**ausgeführt wird, umfassen.  

####  <a name="update-a-site"></a><a name="bkmk_site"></a> Aktualisieren eines Standorts  
Zum Aktualisieren eines Configuration Manager-Standorts können Sie das Updatepaket direkt auf dem Standortserver installieren. Alternativ können Sie das Updatepaket an einem anderen Standort installieren und die Updates anschließend auf einem Standortserver bereitstellen.  

Wenn Sie ein Update auf einem Standortserver installieren, werden bei der Updateinstallation zusätzliche Aktionen verwaltet, die zur Anwendung des Updates erforderlich sind. Dazu gehört unter anderem die Aktualisierung der Standortsystemrollen. Die Ausnahme bildet die Standortdatenbank. Im folgenden Abschnitt wird erläutert, wie Sie die Standortdatenbank aktualisieren.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a> Aktualisieren einer Standortdatenbank  
Zur Aktualisierung der Standortdatenbank wird bei der Installation die Datei **update.sql** für die Standortdatenbank ausgeführt. Sie können den Updatevorgang dahingehend konfigurieren, dass die Standortdatenbank automatisch aktualisiert wird. Alternativ können Sie die Standortdatenbank zu einem späteren Zeitpunkt manuell aktualisieren.  

**Automatisches Aktualisieren der Standortdatenbank**  

Wenn Sie das Updatepaket auf einem Standortserver installieren, können Sie bestimmen, dass die Standortdatenbank beim Installieren des Serverupdates automatisch aktualisiert werden soll. Diese Entscheidung gilt nur für den Standortserver, auf dem Sie das Updatepaket installieren. Sie gilt nicht für Bereitstellungen, die zum Installieren der Updates auf Remotestandortservern erstellt werden.  

> [!NOTE]  
> Wenn Sie sich für die automatische Aktualisierung der Standortdatenbank entscheiden, wird eine Datenbank unabhängig davon aktualisiert, ob die Datenbank sich auf dem Standortserver oder auf einem Remotecomputer befindet.  

> [!IMPORTANT]  
> Erstellen Sie eine Sicherung der Standortdatenbank, bevor Sie die Standortdatenbank aktualisieren. Ein Update für die Standortdatenbank kann nicht deinstalliert werden. Informationen zum Erstellen einer Sicherung für Configuration Manager finden Sie unter [Sicherung und Wiederherstellung in Configuration Manager](backup-and-recovery.md).  

**Manuelles Aktualisieren der Standortdatenbank**  

Wenn Sie sich dafür entscheiden, die Standortdatenbank beim Installieren des Updatepakets auf dem Standortserver nicht automatisch zu aktualisieren, wird die Datenbank auf dem Standortserver, auf dem das Updatepaket ausgeführt wird, durch das Serverupdate nicht verändert. Die Standortdatenbank wird jedoch immer von Bereitstellungen aktualisiert, bei denen das Paket verwendet wird, das für die Softwarebereitstellung erstellt bzw. installiert wird.  

> [!WARNING]  
> Wenn das Update sowohl für den Standortserver als auch für die Standortdatenbank Updates enthält, ist das Update erst verfügbar, wenn die Updates für den Standortserver und die Standortdatenbank abgeschlossen sind. Der Standort befindet sich bis zur Anwendung des Updates auf die Standortdatenbank in einem nicht unterstützten Zustand.  

**So aktualisieren Sie eine Standortdatenbank manuell:**  

1.  Beenden Sie auf dem Standortserver den Dienst SMS_SITE_COMPONENT_MANAGER und dann den Dienst SMS_EXECUTIVE.  

2.  Schließen Sie die Configuration Manager-Konsole.  

3.  Führen Sie das Updateskript **update.sql** für die Datenbank dieses Standorts aus. Informationen zur Aktualisierung einer SQL Server-Datenbank mit einem Skript finden Sie in der Dokumentation für die SQL Server-Version, die Sie für den Standortdatenbankserver verwenden.  

4.  Starten Sie die in den vorherigen Schritten beendeten Dienste neu.  

5.  Bei der Installation des Updatepakets wird die Datei **update.sql** in das folgende Verzeichnis auf dem Standortserver extrahiert:  **\\\\&lt;Servername\>\SMS_&lt;Standortcode\>\Hotfix\\&lt;KB-Nummer\>\update.sql**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a> Aktualisieren eines Computers, auf dem der SMS-Anbieter ausgeführt wird  
Nach der Installation eines Updatepakets mit Updates für den SMS-Anbieter müssen Sie das Update auf jedem Computer bereitstellen, auf dem der SMS-Anbieter ausgeführt wird. Die einzige Ausnahme hierbei bildet die Instanz des SMS-Anbieters, die vorher auf dem Standortserver installiert war, auf dem Sie nun das Updatepaket installieren. Die lokale Instanz des SMS-Anbieters auf dem Standortserver wird aktualisiert, wenn Sie das Updatepaket installieren.  

Wenn Sie den SMS-Anbieter auf einem Computer entfernen und erneut installieren, dann müssen Sie das Update für den SMS-Anbieter auf diesem Computer erneut installieren.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a> Aktualisieren von Clients  
Bei der Installation eines Updates, das Updates für den Configuration Manager-Client enthält, können Sie Clients optional automatisch mit der Updateinstallation oder zu einem späteren Zeitpunkt manuell aktualisieren. Weitere Informationen zum automatischen Upgrade von Clients finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)aktualisiert wird.  

Sie können Updates mit Updates Publisher oder einem Softwarebereitstellungspaket bereitstellen. Alternativ können Sie das Update manuell auf jedem Client installieren. Weitere Informationen zur Installation von Updates über Bereitstellungen finden Sie im Abschnitt [Bereitstellen von Updates für Configuration Manager](#BKMK_Deploy) dieses Themas.  

> [!IMPORTANT]  
> Wenn Sie Updates für Clients installieren und zu dem Updatepaket Updates für Server gehören, dann stellen Sie sicher, dass Sie auch die Serverupdates auf dem primären Standort installieren, dem die Clients zugeordnet sind.  

Für die manuelle Installation des Clientupdates müssen Sie auf jedem Configuration Manager-Client die Datei **Msiexec.exe** ausführen und einen Bezug zur plattformspezifischen Clientupdatedatei (MSP) herstellen.  

Beispiel: Sie können die folgende Befehlszeile für ein Clientupdate verwenden. Von dieser Befehlszeile wird MSIEXEC auf dem Computer ausgeführt. Diese bezieht sich auf die MSP-Datei, die vom Updatepaket auf dem Standortserver extrahiert wurde: **msiexec.exe /p \\\\&lt;Servername\>\SMS_&lt;Standortcode\>\Hotfix\\&lt;KB-Nummer\>\Client\\&lt;Plattform\>\\&lt;msp\> /L\*v &lt;Protokolldatei\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a> Aktualisieren von Configuration Manager-Konsolen  
Für die Aktualisierung einer Configuration Manager-Konsole müssen Sie nach Abschluss der Installation das Update auf dem Computer installieren, auf dem die Konsole ausgeführt wird.  

> [!IMPORTANT]  
> Wenn Sie Updates für die Configuration Manager-Konsole installieren und das Updatepaket Updates für Server enthält, müssen Sie auch die Serverupdates an dem Standort installieren, den Sie mit der Configuration Manager-Konsole verwenden.  

Wenn auf dem Computer, den Sie aktualisieren, der Configuration Manager-Client ausgeführt wird, gilt Folgendes:  

- Sie können für die Installation des Updates eine Bereitstellung verwenden. Weitere Informationen zur Installation von Updates über Bereitstellungen finden Sie im Abschnitt [Bereitstellen von Updates für Configuration Manager](#BKMK_Deploy) dieses Themas.  

- Wenn Sie direkt auf dem Clientcomputer angemeldet sind, können Sie die Installation interaktiv ausführen.  

- Sie können das Update manuell auf jedem Computer installieren. Für die manuelle Installation des Updates für die Configuration Manager-Konsole können Sie auf jedem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, die Datei „Msiexec.exe“ ausführen und einen Verweis auf die MSP-Datei für das Update der Configuration Manager-Konsole erstellen.  

Beispiel: Sie können die folgende Befehlszeile für ein Update der Configuration Manager-Konsole verwenden. Mit dieser Befehlszeile wird MSIEXEC auf dem Computer ausgeführt und auf die MSP-Datei verwiesen, die vom Updatepaket auf dem Standortserver extrahiert wurde: **msiexec.exe /p \\\\&lt;Servername\>\SMS_&lt;Standortcode\>\Hotfix\\&lt;KB-Nummer\>\AdminConsole\\&lt;Plattform\>\\&lt;msp\> /L\*v &lt;Protokolldatei\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Bereitstellen von Updates für Configuration Manager  
Nach der Installation des Updatepakets auf einem Standortserver können Sie mit einer der folgenden drei Methoden auf weiteren Computern Updates bereitstellen.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a> Installieren von Updates mit Updates Publisher 2011  
Wenn Sie das Updatepaket auf einem Standortserver installieren, erstellt der Assistent eine Katalogdatei für Updates Publisher, die Sie zur Bereitstellung der Updates auf den entsprechenden Computern verwenden können. Der Assistent erstellt diesen Katalog immer, auch wenn Sie die Option **Dieses Paket und Programm verwenden, um das Update bereitzustellen**aktualisiert wird.  

Der Katalog für System Center Updates Publisher heißt **SCUPCatalog.cab** und befindet sich an folgendem Speicherort auf dem Computer, auf dem das Updatepaket ausgeführt wird: **\\\\&lt;Servername\>\SMS_&lt;Standortcode\>\Hotfix\\&lt;KB-Nummer\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> Da die Datei SCUPCatalog.cab über die Pfade erstellt wird, die sich konkret auf den Standortserver beziehen, auf dem das Updatepaket installiert ist, kann diese nicht für andere Standortserver verwendet werden.  

Nachdem der Assistent beendet wurde, können Sie den Katalog in Updates Publisher importieren und dann Configuration Manager-Softwareupdates zur Bereitstellung der Updates verwenden. Informationen zu Updates Publisher finden Sie unter [Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

Gehen Sie wie folgt vor, um die Datei „SCUPCatalog.cab“ in Updates Publisher zu importieren und die Updates zu veröffentlichen.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>So importieren Sie Updates in Updates Publisher 2011  

1.  Starten Sie die Updates Publisher-Konsole, und klicken Sie auf **Importieren**.  

2.  Wählen Sie auf der Seite **Importtyp** des Assistenten für den Import des Softwareupdateskatalogs **Pfad zum Katalog für Import angeben**aus, und geben Sie dann die Datei "SCUPCatalog.cab" an.  

3.  Klicken Sie auf **Weiter**und dann erneut auf **Weiter** .  

4.  Klicken Sie im Dialogfeld **Sicherheitswarnung - Katalogüberprüfung** auf **Annehmen**. Schließen Sie den Assistenten, nachdem dieser abgeschlossen ist.  

5.  Wählen Sie in der Updates Publisher-Konsole das Update aus, das Sie bereitstellen möchten, und klicken Sie auf **Veröffentlichen**.  

6.  Wählen Sie auf der Seite **Veröffentlichungsoptionen** des Assistenten für das Veröffentlichen von Softwareupdates **Vollständiger Inhalt**aus, und klicken Sie dann auf **Weiter**.  

7.  Beenden Sie den Assistenten, um die Updates zu veröffentlichen.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a> Installieren von Updates mit der Softwarebereitstellung  
Wenn Sie das Updatepaket auf dem Standortserver eines primären Standorts oder des Standorts der zentralen Verwaltung installieren, können Sie den Installationsassistenten für das Erstellen von Updatepaketen für die Softwarebereitstellung konfigurieren. Dann können Sie jedes Paket auf einer Sammlung von Computern bereitstellen, die Sie aktualisieren möchten.  

Für die Erstellung eines Softwarebereitstellungspakets aktivieren Sie auf der Seite **Softwareupdatebereitstellung konfigurieren** des Assistenten das Kontrollkästchen für jeden Updatepakettyp, den Sie aktualisieren möchten. Die verfügbaren Typen können Server, Configuration Manager-Konsolen und Clients umfassen. Für jeden ausgewählten Updatetyp wird ein separates Paket erstellt.  

> [!NOTE]  
> Das Paket für Server enthält Updates für die folgenden Komponenten:  
>   
> - Standortserver  
> - SMS-Anbieter  
> - Standortdatenbank  

Wählen Sie als Nächstes auf der Seite **Methode der Softwareupdatebereitstellung konfigurieren** des Assistenten die Option **Ich verwende die Softwareverteilung**aus. Aufgrund dieser Auswahl erstellt der Assistent die Softwarebereitstellungspakete.  

Nachdem Sie den Assistenten abgeschlossen haben, können Sie sich die erstellten Pakete in der Configuration Manager-Konsole im Knoten **Pakete** im Arbeitsbereich **Softwarebibliothek** anzeigen lassen. Sie können anschließend Ihren Standardprozess verwenden, um Softwarepakete in Configuration Manager-Clients bereitzustellen. Wenn ein Paket auf einem Client ausgeführt wird, werden so die Updates in den entsprechenden Komponenten von Configuration Manager auf dem Clientcomputer installiert.  

Informationen zum Bereitstellen von Paketen auf Configuration Manager-Clients finden Sie unter [Pakete und Programme](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a> Erstellen von Sammlungen für die Bereitstellung von Updates für Configuration Manager  
Sie können spezifische Updates auf geeigneten Clients bereitstellen. Folgende Informationen können Ihnen bei der Erstellung von Gerätesammlungen für verschiedene Komponenten für Configuration Manager helfen.  

|Configuration Manager-Komponente|Anweisungen|  
|----------------------------------------|------------------|  
|Standortserver der zentralen Verwaltung|Erstellen Sie eine Abfrage für direkte Mitgliedschaft, und fügen Sie den Standortservercomputer der zentralen Verwaltung hinzu.|  
|Alle primären Standortserver|Erstellen Sie eine Abfrage für direkte Mitgliedschaft, und fügen Sie jeden Computer des primären Standortservers hinzu.|  
|Alle sekundären Standortserver|Erstellen Sie eine Abfrage für direkte Mitgliedschaft, und fügen Sie jeden Computer des sekundären Standortservers hinzu.|  
|Alle X86-Clients|Erstellen Sie eine Sammlung mit den folgenden Abfragekriterien:<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"**|  
|Alle X64-Clients|Erstellen Sie eine Sammlung mit den folgenden Abfragekriterien:<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"**|  
|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|Erstellen Sie eine Abfrage für direkte Mitgliedschaft, und fügen Sie jeden Computer hinzu.|  
|Remotecomputer, von denen eine Instanz des SMS-Anbieters ausgeführt wird|Erstellen Sie eine Abfrage für direkte Mitgliedschaft, und fügen Sie jeden Computer hinzu.|  

> [!NOTE]  
> Zur Aktualisierung einer Standortdatenbank stellen Sie das Update auf dem Standortserver für diesen Standort bereit.  

Informationen zum Erstellen von Sammlungen finden Sie unter [Erstellen von Sammlungen](../../../core/clients/manage/collections/create-collections.md).  
