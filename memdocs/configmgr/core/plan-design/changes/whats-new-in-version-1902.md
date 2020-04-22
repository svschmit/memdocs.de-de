---
title: Neuigkeiten in Version 1902
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1902 des Current Branchs von Configuration Manager eingeführt wurden.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4972f6e8689ad44dbd1a19adcde104cd5f59038c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702398"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Neuerungen in Version 1902 von Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1902 für den Current Branch von Configuration Manager ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen eine der Versionen 1802, 1806 oder 1810 ausgeführt wird. <!-- baseline only statement:-->Beim Installieren eines neuen Standorts steht das Update auch als Baselineversion zur Verfügung. In diesem Artikel werden die Änderungen und neuen Features in Configuration Manager, Version 1902, zusammengefasst.  

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Weitere Informationen finden Sie in der [Checkliste für die Installation von Update 1902](../../servers/manage/checklist-for-installing-update-1902.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).

Wenn Sie die neuen Configuration Manager-Features nach der Aktualisierung des Standorts vollständig nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Veraltete Features und Betriebssysteme

Erfahren Sie mehr zu Änderungen bei der Unterstützung, bevor sie in [entfernte und veraltete Elemente](deprecated/removed-and-deprecated.md) aufgenommen werden.

- Die Implementierung für die Freigabe von Inhalten aus Azure hat sich geändert. Verwenden Sie ein inhaltsfähiges Cloud-Management-Gateway, indem Sie die Option **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen** aktivieren. Zukünftig können Sie keinen herkömmlichen Cloudverteilungspunkt mehr erstellen.

Version 1902 löscht die Unterstützung für die folgenden Produkte:  

- Linux und UNIX als Client. Die Einstellung wurde mit [Version 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support) angekündigt. Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Standortinfrastruktur

### <a name="client-health-dashboard"></a>Dashboard „Clientintegrität“

<!--3599209-->
Softwareupdates und andere Apps werden zum Schutz der Umgebung bereitgestellt. Diese Bereitstellungen erreichen jedoch nur fehlerfreie Clients. Fehlerhafte Configuration Manager-Clients beeinträchtigen die Konformität insgesamt. Je nach Nenner – Anzahl der Geräte, die insgesamt verwaltet werden sollen – kann die Ermittlung der Clientintegrität eine gewisse Herausforderung darstellen. Der Nenner ist umso größer, wenn Sie alle Systeme aus Active Directory ermitteln, auch wenn einige dieser Datensätze zu ausgemusterten Computern gehören.

Ab sofort können Sie ein Dashboard mit Informationen zur Integrität von Configuration Manager-Clients in Ihrer Umgebung anzeigen. Zeigen Sie die Clientintegrität, Szenariointegrität und allgemeine Fehler an. Filtern Sie die Ansicht nach verschiedenen Attributen, um alle potenziellen Probleme nach Betriebssystem- und Clientversion anzuzeigen.

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Clientstatus**, und wählen Sie den Knoten **Dashboard „Clientintegrität“** aus.

![Screenshot des Dashboards „Clientintegrität“](media/3599209-client-health-dashboard.png)

Weitere Informationen finden Sie unter [Überwachen von Clients in Configuration Manager](../../clients/manage/monitor-clients.md#bkmk_health).

### <a name="new-management-insight-rules"></a>Neue Regeln für Verwaltungserkenntnisse

Beim Feature „Verwaltungserkenntnisse“ gibt es die folgenden neuen Regeln:

- Mehrere Regeln mit Empfehlungen für die Verwaltung von Sammlungen. Nutzen Sie die daraus gewonnenen Erkenntnisse, um die Verwaltung zu vereinfachen und die Leistung zu verbessern. Überprüfen Sie diese neuen Regeln in der Gruppe **Sammlungen**.<!--3555752-->  

- Regel **Clients auf eine unterstützte Windows 10-Version aktualisieren** in der Gruppe **Vereinfachte Verwaltung**. Diese Regel meldet Clients, auf denen eine nicht mehr unterstützte Windows 10-Version ausgeführt wird. Sie schließt auch Clients mit einer Windows 10-Version ein, bei denen das Serviceende bald erreicht sein wird (drei Monate).<!--3897268-->  

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md).

### <a name="improvement-to-enhanced-http"></a>Verbesserung von erweitertem HTTP

<!--3798957-->

Sie können jetzt erweitertes HTTP pro primärem Standort oder für den Standort der zentralen Verwaltung aktivieren.

Wählen Sie unter den Eigenschaften für den Standort der zentralen Verwaltung die Option **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** aus. Diese Einstellung gilt nur für Standortsystemrollen am Standort der zentralen Verwaltung. Es ist keine globale Einstellung für die Hierarchie.

Weitere Informationen finden Sie unter [Erweitertes HTTP](../hierarchy/enhanced-http.md).

### <a name="improvement-to-setup-prerequisites"></a>Verbesserung der Setupvoraussetzungen

Wenn Sie Version 1902 installieren oder ein Upgrade darauf durchführen, umfasst das Configuration Manager-Setup jetzt die folgenden Voraussetzungsprüfungen:

- **Ausstehender Systemneustart auf dem SQL-Remoteserver**: Diese Voraussetzungsprüfung ähnelt der Regel **Ausstehender Systemneustart**, überprüft aber einen SQL-Remoteserver. Weitere Informationen finden Sie unter [Liste der Voraussetzungsprüfungen](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloudgestützte Verwaltung

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Clouddienst beim Überschreiten des Schwellenwerts beenden

<!--3735092-->
Ein Cloud Management Gateway-Dienst (CMG) kann nun von Configuration Manager beendet werden, wenn mit der Gesamtmenge der übertragenen Daten Ihr Limit überschritten wird. CMG enthielt schon immer Warnungen, um Benachrichtigungen auszulösen, wenn bei der Nutzung Warnstufen oder kritische Werte erreicht wurden. Wenn Sie unerwartete Azure-Kosten aufgrund einer übermäßigen Nutzung reduzieren möchten, können Sie den Clouddienst nun mithilfe dieser neuen Option deaktivieren lassen.

Weitere Informationen finden Sie unter [Beenden von CMG bei Überschreiten des Schwellenwerts](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop).

### <a name="use-azure-resource-manager-for-cloud-services"></a>Einsatz von Azure Resource Manager für Clouddienste

<!--3605704-->
Ab Version 1810 von Configuration Manager ist die Verwendung klassischer Dienstbereitstellungen in Azure veraltet. Diese Version ist die letzte, die das Erstellen dieser Azure-Bereitstellungen unterstützt.

Vorhandene Bereitstellungen funktionieren weiterhin. Ab dieser Version des Current Branch können neue Instanzen des Cloudverwaltungsgateways und Cloudverteilungspunkten nur noch über Azure Resource Manager bereitgestellt werden.

Weitere Informationen finden Sie im Artikel „Planen von Cloud Management Gateway in Configuration Manager“ unter [Azure Resource Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Hinzufügen des Cloudverwaltungsgateways zu Begrenzungsgruppen

<!--3640932-->
Sie können jetzt ein Cloudverwaltungsgateway (Cloud Management Gateway, CMG) einer Begrenzungsgruppe zuordnen. Mit dieser Konfiguration können Clients für die Clientkommunikation entsprechend der Begrenzungsgruppenbeziehungen den Standardwert für das CMG verwenden oder Fallbacks dafür zulassen. Dieses Verhalten ist besonders in Zweigstellen- und VPN-Szenarios nützlich. Sie können für Clientdatenverkehr anstelle von kostspieligen und langsamen WAN-Links die schnelleren Internetlinks zu Microsoft Azure verwenden.

Weitere Informationen finden Sie im Artikel „Planen von Cloud Management Gateway in Configuration Manager“ unter [Hierarchieentwurf](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) sowie unter [Einrichten des Cloudverwaltungsgateways für Configuration Manager](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Verwaltung in Echtzeit

### <a name="run-cmpivot-from-the-central-administration-site"></a>CMPivot über den zentralen Verwaltungsstandort ausführen

<!--3610960-->
Configuration Manager unterstützt ab sofort das Ausführen von CMPivot über den Standort der zentralen Verwaltung in einer Hierarchie. Die Kommunikation mit dem Client wird nach wie vor vom primären Standort abgewickelt. Beim Ausführen von CMPivot über den Standort der zentralen Verwaltung kommuniziert der Client mit dem primären Standort über den Hochgeschwindigkeitskanal des Nachrichtenabonnements. Diese Kommunikation ist nicht von der standardmäßigen SQL-Replikation zwischen Standorten abhängig.

Weitere Informationen finden Sie unter [CMPivot for real-time data (CMPivot für Echtzeitdaten)](../../servers/manage/cmpivot.md#bkmk_cmpivot1902).

### <a name="edit-or-copy-powershell-scripts"></a>Bearbeiten oder Kopieren von PowerShell-Skripts

<!--3705507-->
Sie können jetzt ein vorhandenes PowerShell-Skript **bearbeiten** oder **kopieren**, das mit dem Feature „Skripts ausführen“ verwendet wird. Sie können ein Skript, das Sie ändern müssen, nun direkt bearbeiten und müssen es nicht mehr neu erstellen. Für beide Aktionen wird der gleiche Assistent wie zum Erstellen eines neuen Skripts verwendet. Wenn Sie ein Skript bearbeiten oder kopieren, behält Configuration Manager den Genehmigungsstatus nicht bei.

Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit).


## <a name="content-management"></a><a name="bkmk_content"></a> Content Management

### <a name="distribution-point-maintenance-mode"></a>Wartungsmodus für Verteilungspunkte

<!--3555754-->

Ab sofort können Verteilungspunkte in den Wartungsmodus versetzt werden. Aktivieren Sie den Wartungsmodus, wenn Sie Softwareupdates installieren oder an der Serverhardware Änderungen vornehmen.

Ein Verteilungspunkt im Wartungsmodus weist folgende Verhaltensweisen auf:

- Vom Standort werden keine Inhalte an den Verteilungspunkt verteilt.  

- Der Standort dieses Verteilungspunkts wird von Verwaltungspunkten nicht an Clients zurückgegeben.

- Wenn Sie den Standort aktualisieren, wird ein Verteilungspunkt im Wartungsmodus ebenfalls aktualisiert.

- Die Verteilungspunkteigenschaften sind schreibgeschützt. So ist es beispielsweise nicht möglich, das Zertifikat zu ändern oder Begrenzungsgruppen hinzuzufügen.  

- Ein geplanter Task, wie etwa eine Inhaltsprüfung, wird dennoch nach Zeitplan ausgeführt.

Weitere Informationen zu diesem Feature finden Sie unter [Maintenance mode (Wartungsmodus)](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

Weitere Informationen zur Automatisierung dieses Prozesses mithilfe des Configuration Manager SDK finden Sie unter [SetDPMaintenanceMode method in class SMS_DistributionPointInfo (SetDPMaintenanceMode-Methode in der SMS_DistributionPointInfo-Klasse)](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Clientverwaltung

### <a name="client-provisioning-mode-timeout"></a>Timeout für den Clientbereitstellungsmodus

<!--3197824-->
Die Tasksequenz setzt einen Zeitstempel, sobald der Client in den Bereitstellungsmodus versetzt wird. Die Zeitdauer seit dem letzten Zeitstempel wird von einem Client im Bereitstellungsmodus alle 60 Minuten geprüft. Wenn sich der Client länger als 48 Stunden im Bereitstellungsmodus befindet, wird der Bereitstellungsmodus automatisch beendet und der Vorgang neu gestartet.

Weitere Informationen finden Sie unter [Provisioning mode (Bereitstellungsmodus)](../../../osd/understand/provisioning-mode.md).

### <a name="view-first-screen-only-during-remote-control"></a>Anzeige ausschließlich des ersten Bildschirms während der Remotesteuerung

<!--3231732-->
Wenn Sie eine Verbindung von einem Client zu zwei oder mehr Monitoren herstellen, kann es schwierig sein, diese im Remotesteuerungsviewer von Configuration Manager anzuzeigen. Ein Remotetoolsverantwortlicher kann nun auswählen, ob **alle Bildschirme** oder nur der **erste Bildschirm** angezeigt werden soll.

Weitere Informationen finden Sie unter [Remoteverwaltung eines Windows-Clientcomputers](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Benutzerdefinierten Port für Peeraktivierung angeben

<!--3605925-->
Sie können ab sofort eine benutzerdefinierte Portnummer für den Aktivierungsproxy angeben. Konfigurieren Sie unter den Clienteinstellungen in der Gruppe **Energieverwaltung** die Einstellung für **Wake-On-LAN-Portnummer (UDP)** .  

Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN](../../clients/deploy/configure-wake-on-lan.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Anwendungsverwaltung

### <a name="improvements-to-application-approvals-via-email"></a>Verbesserungen an der Genehmigung von Anwendungen per E-Mail

<!--3594063-->
Diese Version enthält Verbesserungen für die Funktion zum Empfangen von E-Mail-Benachrichtigungen für Anwendungsanforderungen. Benutzer konnten der Anforderung im Softwarecenter immer einen Kommentar hinzuzufügen. Dieser Kommentar wird in der Anwendungsanforderung in der Configuration Manager-Konsole angezeigt. Nun wird dieser Kommentar auch in der E-Mail angezeigt. Die Aufnahme dieses Kommentars unterstützt die genehmigenden Personen bei der Entscheidungsfindung, ob die Anforderung zu genehmigen oder abzulehnen ist.

Weitere Informationen finden Sie im Artikel zu [E-Mail-Benachrichtigungen](../../../apps/deploy-use/app-approval.md#bkmk_email-approve).

### <a name="improvements-to-package-conversion-manager"></a>Verbesserungen am Paketkonvertierungs-Manager

<!-- SCCMDocs-pr issue #3357 -->
Diese Version enthält die folgenden Verbesserungen am [Paketkonvertierungs-Manager](../../../apps/pcm/package-conversion-manager.md):

- Geplante Paketanalyse wird standardmäßig alle 7 Tage ausgeführt.
- PowerShell-Cmdlets zum Analysieren und Konvertieren von Paketen
- Allgemeine Fehlerbehebungen und Verbesserungen


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Bereitstellung des Betriebssystems

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Fortschrittsanzeige während der Tasksequenz für direktes Upgrade

<!--3747129-->
Während der Tasksequenz für das direkte Windows 10-Upgrade wird nun eine detailliertere Statusanzeige angezeigt. Auf dieser Leiste wird der Fortschritt des Windows-Setups angezeigt, das während der Tasksequenz im Hintergrund abläuft. Benutzer erhalten nun Einblicke in den zugrunde liegenden Prozess. Aufgrund der fehlenden Fortschrittsanzeige haben Benutzer vorher häufiger angenommen, dass der Prozess unterbrochen wurde, obwohl dies nicht der Fall war.  

![Beispiel einer Fortschrittsanzeige für eine Tasksequenz für den Windows-Upgradeprozess](media/3747129-installation-progress.png)

Dieses Feature funktioniert mit einer unterstützten Version von Windows 10 und nur mit der Tasksequenz für direktes Upgrade.

### <a name="improvements-to-task-sequence-media-creation"></a>Verbesserungen bei der Erstellung von Tasksequenzmedien

<!--3556027, fka 1359388-->
Diese Version enthält mehrere Verbesserungen, die Ihnen beim Erstellen und Verwalten von Tasksequenzmedien helfen sollen. Weitere Informationen finden Sie in den folgenden Artikeln zu bestimmten Medientypen:

- [Erstellen eigenständiger Medien](../../../osd/deploy-use/create-stand-alone-media.md)
- [Erstellen von vorab bereitgestellten Medien](../../../osd/deploy-use/create-prestaged-media.md)
- [Erstellen von startbaren Medien](../../../osd/deploy-use/create-bootable-media.md)
- [Erstellen von Erfassungsmedien](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Angeben des temporären Speichers

Wenn Sie Tasksequenzmedien erstellen, passen Sie nun den Ort an, an dem Daten an diesem Standort temporär gespeichert werden. Dieser Prozess kann viel Speicherplatz auf dem temporären Laufwerk erfordern. Dank dieser Änderung können Sie flexibler auswählen, wo diese temporären Dateien gespeichert werden sollen.

Geben Sie im **Assistenten zum Erstellen von Tasksequenzmedien** einen Speicherort für den **Stagingordner** an. Dieser ähnelt standardmäßig dem folgenden Pfad: `%UserProfile%\AppData\Local\Temp`.

#### <a name="add-a-label-to-the-media"></a>Hinzufügen einer Bezeichnung zu den Medien

Sie können Tasksequenzmedien jetzt eine Bezeichnung hinzufügen. Damit können Sie die Medien besser identifizieren, nachdem Sie sie erstellt haben. Geben Sie dazu im **Assistenten zum Erstellen von Tasksequenzmedien** eine Medienbezeichnung (**Media label**) ein.

### <a name="import-a-single-index-of-an-os-image"></a>Importieren eines einzelnen Indexes für ein Betriebssystemimage

<!--3719699-->
Beim Importieren einer Windows-Imagedatei (WIM) in Configuration Manager können Sie nun festlegen, dass automatisch ein einzelner Index und nicht alle Imageindexe in die Datei importiert werden. Diese Option bietet die folgenden Vorteile:

- Kleinere Imagedatei  
- Schnellere Offlinewartung  
- Optimierte Imagewartung – für eine kleinere Imagedatei nach der Offlinewartung

Wählen Sie beim Import eines Betriebssystemimages die Option **Index für ein bestimmtes Image aus der angegebenen WIM-Datei extrahieren** aus. Wählen Sie dann den Imageindex aus der Liste aus.  

Weitere Informationen finden Sie unter [Hinzufügen eines Betriebssystemimage](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages).

### <a name="optimized-image-servicing"></a>Optimierte Imagewartung

<!--3555951-->
Beim Anwenden eines Softwareupdates auf ein Betriebssystemimage gibt es eine neue Option zum Optimieren der Ausgabe durch Entfernen von ersetzten Updates. Die Optimierung der Offlinewartung betrifft nur Images mit einem einzelnen Index.

Wählen Sie beim Erstellen eines Zeitplans für die Aktualisierung eines Betriebssystemabbilds die Option **Abgelöste Updates nach der Imageaktualisierung entfernen** aus.

Weitere Informationen finden Sie unter [Anwenden von Softwareupdates auf ein Image](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase).

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Verbesserungen am Tasksequenzschritt „PowerShell-Skript ausführen“

<!--3556028, fka 1359389-->
Der Tasksequenzschritt **PowerShell-Skript ausführen** wurde folgendermaßen verbessert:  

- Sie können Windows PowerShell-Code in diesem Schritt nun direkt eingeben. Dank dieser Änderung können Sie PowerShell-Befehle während einer Tasksequenz ausführen, ohne zuerst ein Paket mit dem Skript zu erstellen und zu verteilen.

- Wenn Sie die Option **PowerShell-Skript eingeben** auswählen, wählen Sie **Skript bearbeiten** aus. Das neue PowerShell-Skriptfenster bietet die folgenden Aktionen:  

    - Direktes Bearbeiten des Skripts  

    - Öffnen eines vorhandenen Skripts aus einer Datei  

    - Wechseln zu einem vorhandenen Skript in Configuration Manager

- Speichern der Skriptausgabe in einer benutzerdefinierten Tasksequenzvariablen  

- Um die Skriptparameter in das Tasksequenzprotokoll aufzunehmen, legen Sie die Tasksequenzvariable **OSDLogPowerShellParameters** auf **TRUE** fest. Standardmäßig befinden sich die Parameter nicht im Protokoll.  

- Weitere Verbesserungen, die ähnliche Funktionen bieten wie der Schritt [Befehlszeile ausführen](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine). Geben Sie beispielsweise alternative Benutzeranmeldeinformationen oder ein Timeout an.

> [!Important]  
> Wenn Sie diese neuen Configuration Manager-Features nach der Aktualisierung des Standorts nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

Weitere Informationen finden Sie unter [PowerShell-Skript ausführen](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

### <a name="other-improvements-to-os-deployment"></a>Weitere Verbesserungen bei der Bereitstellung von Betriebssystemen

<!--3633146,3641475,3654172,3734270-->
Diese Version umfasst die folgenden Verbesserungen bei der Bereitstellung von Betriebssystemen:

- Es gibt bei Tasksequenzen eine neue Standardaktion **Ansicht**. <!--3633146-->  

- Das Dialogfeld mit dem Tasksequenzfehler enthält nun mehr Informationen. Es wird auch der Name des Tasksequenzschritts angezeigt, bei dem ein Fehler aufgetreten ist. <!--3641475-->  

- Wenn Sie die Tasksequenzvariable **OSDDoNotLogCommand** auf TRUE festlegen, wird ab sofort auch die Befehlszeile aus dem Schritt „Befehlszeile ausführen“ in der Protokolldatei ausgeblendet. Bisher wurde nur der Programmname aus dem Schritt „Paket installieren“ in der Datei „smsts.log“ maskiert.<!--3654172-->  

- Wenn Sie einen PXE-Antwortdienst auf einem Verteilungspunkt ohne Windows-Bereitstellungsdienst aktivieren, kann er sich nun auf demselben Server wie der DHCP-Dienst befinden. <!--3734270--> Weitere Informationen finden Sie unter [Configure at least one distribution point to accept PXE requests (Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager)](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


## <a name="software-center"></a><a name="bkmk_userxp"></a> Softwarecenter

### <a name="replace-toast-notifications-with-dialog-window"></a>Ersetzen von Popupbenachrichtigungen durch ein Dialogfeld

<!--3555947-->
In einigen Fällen werden Benutzern Windows-Popupbenachrichtigungen über einen Neustart oder eine erforderliche Bereitstellung nicht angezeigt. So haben sie nicht die Möglichkeit, eine erneute Erinnerung anzufordern. Dieses Verhalten kann zu Problemen für den Benutzer führen, wenn der Client einen Stichtag erreicht.

Wenn also für Bereitstellungen ein Neustart oder Softwareupdates erforderlich sind, haben Sie jetzt die Möglichkeit, ein nachdrücklicheres Dialogfeld zu verwenden.

Weitere Informationen finden Sie unter [Planen für Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

### <a name="configure-user-device-affinity-in-software-center"></a>Affinität zwischen Benutzer und Gerät im Softwarecenter konfigurieren

<!--3485366-->
Mit den [Verbesserungen an der Infrastruktur im Softwarecenter](whats-new-in-version-1806.md#software-center-infrastructure-improvements) ab Version 1806 werden die Standortserverrollen im Anwendungskatalog für die meisten Szenarios nicht mehr benötigt. Einige Kunden vertrauten immer noch auf den Anwendungskatalog, um den Benutzern zu ermöglichen, ihr primäres Gerät für die Affinität zwischen Benutzer und Gerät einzustellen.

Benutzer können jetzt ihr primäres Gerät im Softwarecenter einstellen. Dadurch werden sie in Configuration Manager zum primären Benutzer des Geräts.

Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="configure-default-views-in-software-center"></a>Konfigurieren von Standardansichten im Softwarecenter

<!--3612112-->
Von der Version von Configuration Manager hängt ab, wie Sie das Softwarecenter anpassen können:

- Festlegen des Standardlayouts von Anwendungen als Kacheln oder Liste  

    - Wenn ein Benutzer diese Einstellungen ändert, werden die Benutzereinstellung zukünftig im Softwarecenter beibehalten.  

- Konfigurieren des Standardfilters für Anwendungen für alle Apps oder erforderliche Apps  

    - Im Softwarecenter werden immer Ihre Standardeinstellungen verwendet. Benutzer können diesen Filter ändern, im Softwarecenter werden deren Einstellungen jedoch nicht beibehalten.

Geben Sie diese Einstellungen in der Gruppe **Softwarecenter** der Clienteinstellungen an.

Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults).


## <a name="software-updates"></a><a name="bkmk_sum"></a> Softwareupdates

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Festlegen der Priorität für Featureupdates bei der Windows 10-Wartung

<!--3734525-->
Passen Sie die Priorität an, mit der Clients ein Featureupdate über die [Windows 10-Wartung](../../../osd/deploy-use/manage-windows-as-a-service.md) installieren. Featureupdates werden auf Clients ab sofort standardmäßig mit einer höheren Verarbeitungspriorität installiert.

Verwenden Sie Clienteinstellungen zum Konfigurieren dieser Option. Konfigurieren Sie in der Gruppe **Softwareupdates** die folgende Einstellung: **Threadpriorität für Featureupdates angeben**.

Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../clients/deploy/about-client-settings.md#software-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a> Office-Verwaltung

### <a name="redirect-windows-known-folders-to-onedrive"></a>Umleiten von bekannten Windows-Ordnern zu OneDrive

<!--3556021-->
Verwenden Sie Configuration Manager, um bekannte Windows-Ordner in OneDrive for Business zu verschieben. Zu diesen Ordnern gehören Desktop, Dokumente und Bilder. Stellen Sie diese Einstellungen für Windows 7-Clients bereit, bevor Sie eine Tasksequenz bereitstellen, um so Ihre Windows 10-Upgrades zu vereinfachen.

Weitere Informationen zu diesem Feature von OneDrive for Business finden Sie unter [Umleiten und Verschieben von bekannten Windows-Ordnern in OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders).

Zuerst müssen Sie die [ID Ihres Office 365-Mandanten ermitteln](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id). Stellen Sie dann die Clientversion 18.111.0603.0004 oder höher für die OneDrive-Synchronisierung bereit. Weitere Informationen finden Sie unter [Bereitstellen von OneDrive-Apps mit Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

Wenn Sie ein OneDrive for Business-Profil erstellen und bereitstellen möchten, wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie die **Konformitätseinstellungen**, und wählen Sie den Knoten **OneDrive for Business-Profile** aus.  

Weitere Informationen finden Sie im Abschnitt „Umleiten von bekannten Windows-Ordnern zu OneDrive“ des Artikels [OneDrive for Business-Profile](../../../compliance/deploy-use/onedrive-profile.md).

### <a name="integration-for-office-365-proplus-readiness"></a>Integration für Office 365 ProPlus-Bereitschaft

<!--3735402-->
Verwenden Sie Configuration Manager zum Identifizieren von Geräten mit hoher Zuverlässigkeit, die für ein Upgrade auf Office 365 ProPlus bereit sind. Die Integration bietet Erkenntnisse zu möglichen Kompatibilitätsproblemen mit Office-Add-Ins und -Makros, die in Ihrer Umgebung verwendet werden. Verwenden Sie den Configuration Manager anschließend zum Bereitstellen von Office auf Geräten, die dafür bereit sind.

Das vorhandene Office 365-Clientverwaltungsdashboard enthält jetzt die neue Kachel **Office 365 ProPlus-Upgradebereitschaft**.

Weitere Informationen finden Sie unter [Office 365-Clientverwaltungsdashboard](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness).

### <a name="additional-languages-for-office-365-updates"></a>Weitere Sprachen für Office 365-Updates

<!--3555955-->
Configuration Manager unterstützt jetzt alle unterstützten Sprachen für Office 365-Clientupdates. Der Updateworkflow trennt jetzt die 38 Sprachen für **Windows Update** von den zahlreichen Sprachen für das **Office 365-Clientupdate**.

Weitere Informationen finden Sie unter [Verwalten von Office 365-Updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang).

### <a name="office-products-on-lifecycle-dashboard"></a>Office-Produkte auf dem Dashboard für den Produktlebenszyklus

<!--3556026-->
Das Dashboard für den Produktlebenszyklus umfasst jetzt Informationen zu installierten Versionen von Office 2003 bis 2016. Die Daten werden immer dann angezeigt, wenn die Site den Zusammenfassungstask für den Produktlebenszyklus ausgeführt hat, also alle 24 Stunden.

Weitere Informationen finden Sie unter [Verwenden des Dashboards für den Produktlebenszyklus](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> Stufenweise Bereitstellungen

### <a name="dedicated-monitoring-for-phased-deployments"></a>Dedizierte Überwachung für stufenweise Bereitstellungen

<!--3555949-->
Für stufenweise Bereitstellungen gibt es jetzt einen eigenen dedizierten Überwachungsknoten. Er erleichtert das Identifizieren von stufenweisen Bereitstellungen, die sie erstellt haben, und navigiert dann zur Ansicht „Überwachung“ für stufenweise Bereitstellung. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Stufenweise Bereitstellungen** aus. Dann wird eine Liste mit stufenweisen Bereitstellungen angezeigt.

Weitere Informationen finden Sie unter [Verwalten und Überwachen von stufenweisen Bereitstellungen](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor).

### <a name="improvement-to-phased-deployment-success-criteria"></a>Verbesserung bei den Erfolgskriterien für stufenweise Bereitstellungen

<!--3555946-->
Geben Sie zusätzliche Kriterien für den Erfolg einer Phase in einer Bereitstellung in Phasen an. Anstelle eines bestimmten Prozentsatzes können Sie jetzt auch die Anzahl der erfolgreich bereitgestellten Geräte als Kriterium angeben. Diese Option ist nützlich, wenn die Größe der Sammlung variabel ist und Sie eine bestimmte Anzahl von Geräten haben, die Erfolg zeigen müssen, bevor mit der nächsten Phase fortgefahren wird.

Erstellen Sie eine stufenweise Bereitstellung für eine Tasksequenz, ein Softwareupdate oder eine Anwendung. Wählen Sie auf der Seite „Einstellungen“ des Assistenten die folgende Option als Kriterium für den Erfolg der ersten Phase aus: **Anzahl erfolgreich bereitgestellter Geräte**.

Weitere Informationen finden Sie unter [Erstellen von stufenweisen Bereitstellungen mit Configuration Manager](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-Konsole

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Verbesserungen der Configuration Manager-Konsole

<!--3594151-->
Basierend auf Kundenfeedback von der Midwest Management Summit (MMS) Desert Edition 2018 umfasst diese Version folgende Verbesserungen an der Configuration Manager-Konsole:

- Maximieren des Fensters zum Durchsuchen der Registrierung für Methoden zur Anwendungserkennung
- Wechseln von einer Anwendungsbereitstellung zu der Sammlung
- Entfernen von Inhalten aus der Überwachung des Status
- Sortierung von Ansichten nach ganzzahligen Werten im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung**
- Verschieben der Warnung wegen einer großen Anzahl von Ergebnissen

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md#tips).

### <a name="configuration-manager-console-notifications"></a>Configuration Manager-Konsolenbenachrichtigungen

<!--3556016, fka 1318035-->
Damit Sie besser informiert bleiben und die entsprechenden Maßnahmen ergreifen können, benachrichtigt Sie die Configuration Manager-Konsole jetzt über die folgenden Ereignisse:

- Ein Update ist für Configuration Manager selbst verfügbar.
- Lebenszyklus- und Verwaltungsereignisse treten in der Umgebung auf.

Diese Benachrichtigung wird als Leiste am oberen Rand des Konsolenfensters unter dem Menüband dargestellt. Es ersetzt die vorherige Oberfläche, wenn Configuration Manager-Updates verfügbar sind. Diese Benachrichtigungen in der Konsole enthalten wichtige Informationen, beeinträchtigen aber nicht Ihre Arbeit in der Konsole. Sie können kritische Benachrichtigungen nicht verwerfen. Die Konsole zeigt alle Benachrichtigungen in einem neuen Benachrichtigungsbereich der Titelleiste an.

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md).

### <a name="confirmation-of-console-feedback"></a>Bestätigung des Konsolenfeedbacks

<!--3556010-->
Wenn Sie [Feedback](../../understand/find-help.md#product-feedback) über die Configuration Manager-Konsole übermitteln, wird nun eine Bestätigung angezeigt. Diese enthält eine **Feedback-ID**, die Sie zur Nachverfolgung an Microsoft übermitteln können.

Weitere Informationen finden Sie unter [Produktfeedback](../../understand/find-help.md#bkmk_feedbackid).

### <a name="view-recently-connected-consoles"></a>Anzeigen kürzlich verbundener Konsolen

<!--3699367-->
Sie können jetzt die neuesten Verbindungen für die Configuration Manager-Konsole anzeigen. In der Ansicht finden Sie aktive Verbindungen und die Konsolen, die kürzlich verbunden wurden. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Sicherheit**, und wählen Sie den Knoten **Konsolenverbindungen** aus.

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md#bkmk_viewconnected).

### <a name="in-console-documentation-dashboard"></a>Dashboard für die konsoleninterne Dokumentation

<!--3556019, fka 1357546-->
Es gibt im neuen Arbeitsbereich der **Community** einen neuen Knoten für **Dokumentation**. Dieser Knoten enthält aktuelle Informationen zur Configuration Manager-Dokumentation und Supportartikel.

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md#bkmk_doc-dashboard).

### <a name="search-device-views-using-mac-address"></a>Geräteansichten mithilfe der MAC-Adresse durchsuchen

<!--3600878-->
Sie können jetzt in einer Geräteansicht der Configuration Manager-Konsole nach einer MAC-Adresse suchen. Diese Eigenschaft ist für Administratoren bei der Betriebssystembereitstellung hilfreich, wenn sie Probleme mit PXE-basierten Bereitstellungen beheben. Fügen Sie zur Ansicht einer Liste von Geräten die Spalte **MAC-Adresse** hinzu. Verwenden Sie das Suchfeld, um die Suchkriterien für die **MAC-Adresse** hinzuzufügen.

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md#tips).

### <a name="use-net-47-for-improved-console-accessibility"></a>Verwenden von .NET 4.7 für verbesserte Barrierefreiheit der Konsole

<!-- SCCMDocs-pr issue #3228 -->
Um die Barrierefreiheitsfunktionen der Configuration Manager-Konsole zu verbessern, aktualisieren Sie .NET auf dem Computer, auf dem die Konsole ausgeführt wird, auf Version 4.7 oder höher.

Weitere Informationen finden Sie unter [Barrierefreiheitsfunktionen in System Center Configuration Manager](../../understand/accessibility-features.md).

### <a name="changes-to-console-setup-process"></a>Änderungen am Konsolen-Setupprozess

<!-- 3612513 -->
Beim Installieren der Configuration Manager-Konsole werden neue Komponenten benötigt. Wenn Sie ein Paket zum Installieren der Konsole auf anderen Computern erstellen, sorgen Sie dafür, dass das Paket die folgenden Dateien enthält:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Bei der Installation oder dem Update eines Standortservers werden diese Installationsdateien und unterstützten Sprachpakete für den Standort in den Unterordner **Tools\ConsoleSetup** kopiert. Weitere Informationen finden Sie unter [Installieren der Configuration Manager-Konsole](../../servers/deploy/install/install-consoles.md).


## <a name="other-updates"></a>Weitere Updates

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im Current Branch von Configuration Manager, Version 1902](https://support.microsoft.com/help/4498910).

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie in den [Versionshinweisen zu PowerShell 1902](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps).

Folgender Updaterollup (4500571) ist ab dem 17. Juni 2019 in der Konsole verfügbar: [Updaterollup für den aktuellen Branch von Configuration Manager Version 1902](https://support.microsoft.com/help/4500571).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Nächste Schritte

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie weitere Informationen dazu unter [Installieren von Updates für Configuration Manager](../../servers/manage/updates.md) und [Checkliste für die Installation von Update 1902](../../servers/manage/checklist-for-installing-update-1902.md).

> [!TIP]  
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:    
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)  

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).
