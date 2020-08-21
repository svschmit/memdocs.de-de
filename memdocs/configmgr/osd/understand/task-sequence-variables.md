---
title: 'Tasksequenzvariablen: Referenz'
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Variablen zum Steuern und Anpassen einer Configuration Manager-Tasksequenz.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86a19970b58747d83ae8823eb8e2a85c40c03c4d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697346"
---
# <a name="task-sequence-variables"></a>Tasksequenzvariablen

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden alle verfügbaren Variablen in alphabetischer Reihenfolge aufgeführt. Verwenden Sie die **Suchfunktion** (i.d.R. **STRG** + **F**), um eine bestimmte Variable zu finden. Es wird angegeben, ob die Variable für einen bestimmten Schritt gilt. Der Artikel über [Tasksequenzschritte](task-sequence-steps.md) enthält die Liste der für jeden Schritt spezifischen Variablen.

Weitere Informationen finden Sie unter [Verwenden von Tasksequenzvariablen](using-task-sequence-variables.md).

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a> Tasksequenzvariablen: Referenz

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

Die Tasksequenz prüft beim Starten von Windows PE die Festplatten eines Computers auf vorherige Installationen eines Betriebssystems. Der Speicherort des Windows-Ordners wird in dieser Variable gespeichert. Sie können Ihre Tasksequenz so konfigurieren, dass sie diesen Wert aus der Umgebung abruft und mit diesem Wert festlegt, dass für die Installation des neuen Betriebssystems der gleiche Speicherort des Windows-Ordners verwendet werden soll.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

Die Tasksequenz prüft beim Starten von Windows PE die Festplatten eines Computers auf vorherige Installationen eines Betriebssystems. Der Speicherort auf der Festplatte, in dem das Betriebssystem installiert ist, wird in dieser Variable gespeichert. Sie können Ihre Tasksequenz so konfigurieren, dass sie diesen Wert aus der Umgebung abruft und mit diesem Wert festlegt, dass für das neue Betriebssystem der gleiche Speicherort auf der Festplatte verwendet werden soll.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Gilt für den Schritt [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).*

(Eingabe)

Gibt die Paket-ID des Configuration Manager-Pakets an, das die USMT-Dateien enthält. Diese Variable ist erforderlich.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Gilt für den Schritt [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState).*

(Eingabe)

Gibt die Paket-ID des Configuration Manager-Pakets an, das die USMT-Dateien enthält. Diese Variable ist erforderlich.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Hiermit wird die eindeutige ID der aktuell ausgeführten Tasksequenzbereitstellung gespeichert. Dabei wird das gleiche Format wie bei den IDs der Bereitstellung der Configuration Manager-Softwareverteilung verwendet. Wenn die Tasksequenz von einem eigenständigen Medium aus ausgeführt wird, ist diese Variable nicht definiert.

#### <a name="example"></a>Beispiel

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt das Bestandskennzeichen für den Computer an.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a> _SMSTSBootImageID

Wenn die aktuell ausgeführte Tasksequenz auf ein Startimagepaket verweist, ist in dieser Variablen die Startimagepaket-ID enthalten. Verweist die Tasksequenz auf kein Startimagepaket, ist diese Variable nicht festgelegt.

#### <a name="example"></a>Beispiel

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

Die Tasksequenz legt diese Variable fest, wenn ein Computer im UEFI-Modus erkannt wird.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
Die Tasksequenz legt diese Variable fest, wenn sie Inhalte auf dem lokalen Laufwerk zwischenspeichert. Die Variable enthält den Pfad zum Cache. Wenn diese Variable nicht vorhanden ist, gibt es keinen Cache.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Speichert den Wert der Configuration Manager-Client-GUID. Wenn die Tasksequenz von einem eigenständigen Medium aus ausgeführt wird, ist diese Variable nicht festgelegt.

#### <a name="example"></a>Beispiel

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Gibt den Namen des aktuell ausgeführten Tasksequenzschritts an. Diese Variable wird festgelegt, bevor die einzelnen Schritte vom Tasksequenz-Manager ausgeführt werden.

#### <a name="example"></a>Beispiel

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt die vom Computer verwendeten Standardgateways an.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

Wenn die aktuelle Tasksequenz im Modus für bedarfsorientierten Download ausgeführt wird, lautet diese Variable `true`. Im Modus für bedarfsorientierten Download lädt der Tasksequenz-Manager Inhalt nur dann lokal herunter, wenn er darauf zugreifen muss.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a> _SMSTSInWinPE

Wenn der aktuelle Tasksequenzschritt in Windows PE ausgeführt wird, lautet diese Variable `true`. Sie können diese Tasksequenzvariable testen, um die aktuelle Betriebssystemumgebung zu bestimmen.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt die vom Computer verwendeten IP-Adressen an.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a> _SMSTSLastActionName

Speichert den Namen der zuletzt ausgeführten Aktion. Diese Variable bezieht sich auf **_SMSTSLastActionRetCode**. Die Tasksequenz protokolliert diese Werte in der Datei „smsts.log“. Diese Variable ist bei der Problembehandlung einer Tasksequenz hilfreich. Wenn ein Schritt fehlschlägt, kann ein benutzerdefiniertes Skript den Namen des Schritts sowie den Rückgabecode enthalten.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Speichert den Rückgabecode der zuletzt ausgeführten Aktion. Diese Variable kann als Bedingung verwendet werden, um zu ermitteln, ob der nächste Schritt ausgeführt wird.

#### <a name="example"></a>Beispiel

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- Wenn der letzte Schritt erfolgreich ausgeführt wurde, lautet diese Variable `true`.  

- Wenn beim letzten Schritt ein Fehler auftritt, lautet sie `false`.  

- Wenn die Tasksequenz die letzte Aktion übersprungen hat, weil der Schritt deaktiviert oder die zugehörige Bedingung als **FALSE** ausgewertet wurde, wird diese Variable nicht zurückgesetzt. Sie enthält immer noch den Wert der vorherigen Aktion.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a> _SMSTSLastContentDownloadLocation

<!-- 2840337 -->
Ab Version 1906 enthält diese Variable den letzten Speicherort, von dem die Tasksequenz Inhalte heruntergeladen hat bzw. herunterzuladen versucht hat. Überprüfen Sie diese Variable, statt die Clientprotokolle für diesen Inhaltsspeicherort zu analysieren.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Gibt an, dass die Tasksequenz über eine der folgenden Methoden gestartet wurde:  

- **SMS:** der Configuration Manager-Client, z. B. wenn ein Benutzer ihn über das Softwarecenter startet
- **UFD:** ältere USB-Medien
- **UFD+FORMAT:** neuere USB-Medien
- **CD:** eine startbare CD
- **DVD:** eine startbare DVD
- **PXE:** Netzwerkstart mit PXE
- **HD:** vorab bereitgestellte Medien auf einer Festplatte

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a> _SMSTSLogPath

Speichert den vollständigen Pfad des Protokollverzeichnisses. Mit diesem Wert legen Sie fest, wo die Tasksequenzschritte ihre Aktionen protokollieren. Dieser Wert kann nur festgelegt werden, wenn eine Festplatte verfügbar ist.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt die vom Computer verwendeten MAC-Adressen an.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a> _SMSTSMachineName

Legt den Computernamen fest und speichert diesen. Speichert den Namen des Computers, den die Tasksequenz zum Protokollieren aller Statusmeldungen verwendet. Um den Computernamen im neuen Betriebssystem zu ändern, verwenden Sie die Variable [OSDComputerName](#OSDComputerName-input).

### <a name="_smstsmake"></a><a name="SMSTSMake"></a> _SMSTSMake

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt den Hersteller des Computers an.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Gibt den Pfad an, der von der Variablen [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) definiert wird. Dieser Pfad gibt an, wo die Tasksequenz während der Ausführung temporäre Cachedateien auf dem Zielcomputer speichert. Wenn Sie die Variable „SMSTSLocalDataDrive“ vor dem Starten der Tasksequenz definieren (z.B. durch Festlegen einer Sammlungsvariablen), definiert Configuration Manager die Variable „_SMSTSMDataPath“, sobald die Tasksequenz gestartet wird.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a> _SMSTSMediaType

Gibt den Medientyp an, mit dem die Installation initiiert wird. Beispiele für Medientypen sind Startmedien, vollständige Medien, PXE und vorab bereitgestellte Medien.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a> _SMSTSModel

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt das Modell des Computers an.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a> _SMSTSMP

Speichert die URL oder die IP-Adresse eines Configuration Manager-Verwaltungspunkts

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a> _SMSTSMPPort

Speichert die Portnummer eines Configuration Manager-Verwaltungspunkts.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a> _SMSTSOrgName

Speichert den Namen des Brandingtitels, den die Tasksequenz im Statusdialogfeld anzeigt.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Gilt für den Schritt [Betriebssystem aktualisieren](task-sequence-steps.md#BKMK_UpgradeOS).*

Speichert den Exitcodewert, der von Windows Setup zurückgegeben wird, um auf eine erfolgreiche oder fehlerhafte Ausführung hinzuweisen. Diese Variable ist bei der Befehlszeilenoption `/Compat` hilfreich.

#### <a name="example"></a>Beispiel

Ergreifen Sie nach Abschluss eines reinen Kompatibilitätsscans je nach Fehler- oder Erfolgsexitcode in späteren Schritten die entsprechenden Maßnahmen. Bei erfolgreicher Ausführung initiieren Sie das Upgrade. Sie können auch einen Marker in der Umgebung festlegen, um eine Erfassung mit Hardwareinventur auszuführen. Fügen Sie beispielsweise eine Datei hinzu, oder legen Sie einen Registrierungsschlüssel fest. Verwenden Sie diese Marker, um eine Sammlung von Computern zu erstellen, die zum Upgrade bereit sind oder die vor dem Upgrade eine Aktion erfordern.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a> _SMSTSPackageID

Speichert die ID der aktuell ausgeführten Tasksequenz. Diese ID hat das gleiche Format wie eine Configuration Manager-Softwarepaket-ID.

#### <a name="example"></a>Beispiel

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a> _SMSTSPackageName

Speichert den Namen der aktuell ausgeführten Tasksequenz. Ein Configuration Manager-Administrator gibt diesen Namen beim Erstellen der Tasksequenz an.

#### <a name="example"></a>Beispiel

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Die Variable ist auf `true` festgelegt, wenn die aktuelle Tasksequenz im Modus zur Ausführung über den Verteilungspunkt ausgeführt wird. Dieser Modus bedeutet, dass der Tasksequenz-Manager die erforderlichen Paketfreigaben vom Verteilungspunkt abruft.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt die Seriennummer des Computers an.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Gibt an, ob Windows Setup bei einem direkten Upgrade einen Rollback ausgeführt hat. Die Variablenwerte können `true` oder `false` sein.

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Speichert den Standortcode des Configuration Manager-Standorts

#### <a name="example"></a>Beispiel

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a> _SMSTSTimezone

Diese Variable speichert Zeitzoneninformationen im folgenden Format:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Beispiel

Für die Zeitzone **Eastern Time (USA und Kanada)** :

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a> _SMSTSType

Gibt den Typ der aktuell ausgeführten Tasksequenz an. Die Variable muss einen der folgenden Werte aufweisen:  

- **1:** eine allgemeine Tasksequenz
- **2:** eine Tasksequenz für eine Betriebssystembereitstellung

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a> _SMSTSUseCRL

Wenn die Tasksequenz über HTTPS mit dem Verwaltungspunkt kommuniziert, gibt diese Variable an, ob sie die Zertifikatssperrliste verwendet.

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Gibt an, ob ein Benutzer die Tasksequenz gestartet hat. Diese Variable wird nur festgelegt, wenn die Tasksequenz über das Softwarecenter gestartet wird. Dies ist beispielsweise der Fall, wenn [_SMSTSLaunchMode](#SMSTSLaunchMode) auf `SMS` festgelegt ist.

Diese Variable kann die folgenden Werte aufweisen:  

- `true`: Die Tasksequenz wird von einem Benutzer manuell über das Softwarecenter gestartet.  

- `false`: Die Tasksequenz wird automatisch vom Configuration Manager-Planer initiiert.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Gibt an, ob die Tasksequenz SSL zur Kommunikation mit dem Configuration Manager-Verwaltungspunkt verwendet. Wenn Sie Ihre Standortsysteme für HTTPS konfigurieren, wird der Wert auf `true` festgelegt.

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a> _SMSTSUUID

*Gilt für den Schritt [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Gibt die UUID des Computers an.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a> _SMSTSWTG

Gibt an, ob der Computer als Windows To Go-Gerät ausgeführt wird.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a> _TS_CRMEMORY

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Mindestens erforderlicher Arbeitsspeicher (MB)** TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a> _TS_CRSPEED

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Mindestens erforderliche Prozessorgeschwindigkeit (MHz)** TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a> _TS_CRDISK

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Mindestens erforderlicher freier Speicherplatz (MB)** TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a> _TS_CROSTYPE

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Aktuelles Betriebssystem, das aktualisiert wird** TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a> _TS_CRARCH

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Architecture of current OS** (Architektur des aktuellen Betriebssystems) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a> _TS_CRMINOSVER

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Minimum OS version** (Mindestversion des Betriebssystems) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a> _TS_CRMAXOSVER

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Maximum OS version** (Maximalversion des Betriebssystems) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a> _TS_CRCLIENTMINVER

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Minimum client version** (Mindestversion des Clients) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a> _TS_CROSLANGUAGE

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Language of current OS** (Sprache des aktuellen Betriebssystems) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a> _TS_CRACPOWER

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **AC power plugged in** (Netzteil angeschlossen) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a> _TS_CRNETWORK

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Network adapter connected** (Netzwerkadapter verbunden) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_cruefi"></a><a name="TSCRUEFI"></a> _TS_CRUEFI

*Ab Version 2006* <!--6452769-->
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Eine schreibgeschützte Variable, die angibt, ob **Computer befindet sich im UEFI-Modus** BIOS (`0`) oder UEFI (`1`) zurückgibt. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a> _TS_CRWIRED

*Ab Version 2002* <!--6005561-->  
*Gilt für den Schritt [Bereitschaft überprüfen](task-sequence-steps.md#BKMK_CheckReadiness)*

Dies ist eine schreibgeschützte Variable, mit der überprüft werden kann, ob die Überprüfung **Network adapter is not wireless** (Netzwerkadapter ist nicht drahtlos) TRUE (`1`) oder FALSE (`0`) zurückgegeben hat. Wenn Sie diese Überprüfung nicht aktivieren, ist der Wert dieser schreibgeschützten Variable leer.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a> _TSAppInstallStatus

Die Tasksequenz legt diese Variable mit dem Installationsstatus für die Anwendung beim Schritt [Anwendung installieren](task-sequence-steps.md#BKMK_InstallApplication) fest. Einer der folgenden Werte wird festgelegt:  

- **Nicht definiert:** Der Schritt „Anwendung installieren“ wurde nicht ausgeführt.  

- **Fehler**: Bei mindestens einer Anwendung ist aufgrund eines Fehlers beim Schritt „Anwendung installieren“ ein Fehler aufgetreten.  

- **Warnung:** Während des Schritts „Anwendung installieren“ sind keine Fehler aufgetreten. Mindestens eine Anwendung oder eine erforderliche Abhängigkeit konnte wegen einer nicht erfüllten Anforderung nicht installiert werden.  

- **Erfolg:** Während des Schritts „Anwendung installieren“ sind keine Fehler oder Warnungen aufgetreten.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a> _TSSecureBoot

*Ab Version 2002* <!--5842295-->  

Verwenden Sie diese Variable, um den Status des sicheren Starts auf einem UEFI-fähigen Gerät zu bestimmen. Für die Variable ist einer der folgenden Werte möglich:

- `NA`: Der zugehörige Registrierungswert ist nicht vorhanden, das heißt, dass das Gerät keinen sicheren Start unterstützt.
- `Enabled`: Für das Gerät ist der sichere Start aktiviert.
- `Disabled`: Für das Gerät ist der sichere Start deaktiviert.

### <a name="osdadapter"></a><a name="OSDAdapter"></a> OSDAdapter

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Diese Tasksequenzvariablen ist eine *Arrayvariable*. Die einzelnen Elemente im Array stellen die Einstellungen für eine einzelne Netzwerkkarte im Computer dar. Greifen Sie auf die Einstellungen für den jeweiligen Adapter zu, indem Sie den Namen der Arrayvariablen mit dem nullbasierten Netzwerkadapterindex und dem Eigenschaftennamen kombinieren.

Wenn in Schritt „Netzwerkeinstellungen anwenden“ mehrere Netzwerkadapter konfiguriert werden, werden die Eigenschaften für den *zweiten* Netzwerkadapter mithilfe des Indexes **1** im Variablennamen definiert. Beispiel: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList und OSDAdapter1DNSDomain.

Verwenden Sie die folgenden Variablennamen, um die Eigenschaften des *ersten* Netzwerkadapters für den zu konfigurierenden Schritt zu definieren:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Diese Einstellung ist erforderlich. Mögliche Werte sind `True` oder `False`. Beispiel:

`true` aktiviert das Dynamic Host Configuration Protokoll (DHCP) für den Adapter.

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Eine durch Kommas getrennte Liste der IP-Adressen für den Adapter. Diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf `false` festgelegt. Diese Einstellung ist erforderlich.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Eine durch Kommas getrennte Liste der Subnetzmasken. Diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf `false` festgelegt. Diese Einstellung ist erforderlich.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Eine durch Kommas getrennte Liste der IP-Gatewayadressen. Diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf `false` festgelegt. Diese Einstellung ist erforderlich.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Die DNS-Domäne (Domain Name System) für den Adapter.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Eine durch Kommas getrennte Liste der DNS-Server für den Adapter. Diese Einstellung ist erforderlich.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Der Wert `true` ist festgelegt, um die IP-Adresse für den Adapter in DNS zu registrieren.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Der Wert `true` ist festgelegt, um die IP-Adresse für den Adapter in DNS unter dem vollständigen DNS-Namen des Computers zu registrieren.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Der Wert `true` ist festgelegt, um IP-Protokollfilterung für den Adapter zu aktivieren.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Eine durch Kommas getrennte Liste der Protokolle, die über IP ausgeführt werden dürfen. Diese Eigenschaft wird ignoriert, wenn **EnableIPProtocolFiltering** auf `false` festgelegt ist.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Der Wert `true` ist festgelegt, um TCP-Portfilterung für den Adapter zu aktivieren.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Eine durch Kommas getrennte Liste der Ports, denen Zugriffsberechtigungen für TCP zu erteilen sind. Diese Eigenschaft wird ignoriert, wenn **EnableTCPFiltering** auf `false` festgelegt ist.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Optionen für NetBIOS über TCP/IP. Es sind folgende Werte möglich:  

- `0`: NetBIOS-Einstellungen von DHCP-Server verwenden  
- `1`: NetBIOS über TCP/IP aktivieren  
- `2`: NetBIOS über TCP/IP deaktivieren  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Der Wert `true` ist festgelegt, damit WINS für die Namensauflösung verwendet wird.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Eine durch Kommas getrennte Liste der WINS-Server-IP-Adressen. Diese Eigenschaft wird ignoriert, es sei denn, **EnableWINS** ist auf `true` festgelegt.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

Mit dieser MAC-Adresse werden die Einstellungen dem physischen Netzwerkadapter zugeordnet.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

Der Name der Netzwerkverbindung, der in der Systemsteuerung unter „Netzwerkverbindungen“ angezeigt wird. Der Name ist zwischen 0 und 255 Zeichen lang.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Der Index der Netzwerkadaptereinstellungen im Array der Einstellungen.

#### <a name="example"></a>Beispiel

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a> OSDAdapterCount

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Hiermit wird die Anzahl der Netzwerkkarten angegeben, die auf dem Zielcomputer installiert sind. Wenn Sie den **OSDAdapterCount**-Wert festlegen, müssen Sie auch alle Konfigurationsoptionen für die einzelnen Adapter bestimmen.

Wenn Sie z. B. den **OSDAdapter0TCPIPNetbiosOptions**-Wert für den ersten Adapter festlegen, müssen Sie auch alle anderen Werte für diesen Adapter konfigurieren.

Wenn Sie diesen Wert nicht angeben, ignoriert die Tasksequenz alle **OSDAdapter**-Werte.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*Gilt für den Schritt [Treiberpaket anwenden](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(Eingabe)

Hiermit wird die Inhalts-ID des Treibers für Massenspeichergeräte angegeben, der aus dem Treiberpaket installiert werden soll. Wenn diese Variable nicht angegeben ist, wird kein Massenspeichertreiber installiert.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Gilt für den Schritt [Treiberpaket anwenden](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(Eingabe)

Hiermit wird angegeben, ob ein Treiber für Massenspeichergeräte installiert wird. Diese Variable muss **SCSI** sein.

Wenn [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) festgelegt ist, ist diese Variable erforderlich.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Gilt für den Schritt [Treiberpaket anwenden](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(Eingabe)

Hiermit wird die für den Start erforderliche ID des Treibers für Massenspeichergeräte angegeben, der installiert werden soll. Diese ID wird im Abschnitt **SCSI** der Gerätetreiberdatei „txtsetup.oem“ aufgeführt.

Wenn [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) festgelegt ist, ist diese Variable erforderlich.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Gilt für den Schritt [Treiberpaket anwenden](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(Eingabe)

Hiermit wird die INF-Datei des zu installierenden Massenspeichertreibers angegeben.

Wenn [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) festgelegt ist, ist diese Variable erforderlich.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Gilt für den Schritt [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(Eingabe)

Wenn der Treiberkatalog mehrere mit einem Hardwaregerät kompatible Gerätetreiber enthält, legt diese Variable die im Schritt auszuführende Aktion fest.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard): Nur der am besten geeignete Gerätetreiber wird installiert  

- `false`: Alle kompatiblen Gerätetreiber werden installiert, und Windows wählt dann den am besten geeigneten Treiber aus  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Gilt für den Schritt [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(Eingabe)

Eine durch Kommas getrennte Liste der eindeutigen IDs der Treiberkatalogkategorie. Im Schritt **Treiber automatisch anwenden** werden nur die Treiber in mindestens einer der angegebenen Kategorien berücksichtigt. Dieser Wert ist optional und wird standardmäßig nicht festgelegt. Rufen Sie die verfügbaren Kategorie-IDs ab, indem Sie die Objekte **SMS_CategoryInstance** am Standort auflisten.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a> OSDBitLockerRebootCount

*Gilt für den Schritt [BitLocker deaktivieren](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
Ab Version 1906 können Sie über diese Variable die Anzahl von Neustarts festlegen, nach denen der Schutz fortgesetzt wird.

#### <a name="valid-values"></a>Gültige Werte

Ein ganzzahliger Wert zwischen `1` und `15`.

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a> OSDBitLockerRebootCountOverride

*Gilt für den Schritt [BitLocker deaktivieren](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
Ab Version 1906 können Sie diesen Wert festlegen, um die vom Schritt oder der [OSDBitLockerRebootCount](#OSDBitLockerRebootCount)-Variablen festgelegte Zahl außer Kraft zu setzen. Während die anderen Methoden nur Werte von 1 bis 15 akzeptieren, wenn Sie diese Variable auf 0 setzen, bleibt BitLocker auf unbestimmte Zeit deaktiviert. Diese Variable ist hilfreich, wenn die Tasksequenz einen Wert festlegt, Sie aber einen separaten Wert pro Gerät oder pro Sammlung festlegen möchten.

#### <a name="valid-values"></a>Gültige Werte

Ein ganzzahliger Wert zwischen `0` und `15`.

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*Gilt für den Schritt [BitLocker aktivieren](task-sequence-steps.md#BKMK_EnableBitLocker).*

(Eingabe)

Der Schritt **BitLocker aktivieren** generiert kein zufälliges Wiederherstellungskennwort, sondern verwendet den angegebenen Wert als Wiederherstellungskennwort. Dieser Wert muss ein gültiges numerisches BitLocker-Wiederherstellungskennwort sein.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*Gilt für den Schritt [BitLocker aktivieren](task-sequence-steps.md#BKMK_EnableBitLocker).*

(Eingabe)

Von dem Schritt **BitLocker aktivieren** wird kein zufälliger Systemstartschlüssel für die Schlüsselverwaltungsoption **Nur Schlüssel zum Systemstart auf USB** generiert, sondern das Trusted Platform Module (TPM) als Systemstartschlüssel verwendet. Bei dem Wert muss es sich um einen gültigen, 256-Bit Base64-codierten BitLocker-Systemstartschlüssel handeln.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(Eingabe)

Gibt einen Windows-Kontonamen mit der Berechtigung, das erfasste Image in einer Netzwerkfreigabe ([OSDCaptureDestination](#OSDCaptureDestination)) zu speichern, an. Außerdem wird [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) angegeben.

Weitere Informationen zu Konten für die Erfassung des Betriebssystemimages finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(Eingabe)

Gibt das Kennwort für das Windows-Konto ([OSDCaptureAccount](#OSDCaptureAccount)) an, das zum Speichern des erfassten Images auf einer Netzwerkfreigabe ([OSDCaptureDestination](#OSDCaptureDestination)) verwendet wird.

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(Eingabe)

Gibt den Speicherort an, an dem die Tasksequenz das erfasste Betriebssystemimage speichert. Die maximale Länge für den Verzeichnisnamen beträgt 255 Zeichen. Wenn die Netzwerkfreigabe eine Authentifizierung erfordert, geben Sie die Variablen [OSDCaptureAccount](#OSDCaptureAccount) und [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) an.

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a> OSDComputerName (Eingabe)

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Hiermit wird der Name des Zielcomputers angegeben.

#### <a name="example"></a>Beispiel

`%_SMSTSMachineName%` (Standard)

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a> OSDComputerName (Ausgabe)

*Gilt für den Schritt [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Auf den NetBIOS-Namen des Computers festlegen. Der Wert wird nur festgelegt, wenn die Variable [OSDMigrateComputerName](#OSDMigrateComputerName) auf `true` festgelegt ist.

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a> OSDConfigFileName

*Gilt für den Schritt [Betriebssystemimage anwenden](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(Eingabe)

Gibt den Dateinamen der Antwortdatei für die Betriebssystembereitstellung an, die zum Bereitstellungsimagepaket des Betriebssystems gehört.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Gilt für den Schritt [Datenimage anwenden](task-sequence-steps.md#BKMK_ApplyDataImage).*

(Eingabe)

Gibt den Indexwert des Images an, der auf den Zielcomputer angewendet wird.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a> OSDDiskIndex

*Gilt für den Schritt [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(Eingabe)

Gibt die Anzahl der zu partitionierenden physischen Datenträger an.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a> OSDDNSDomain

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Gibt den primären DNS-Server an, den der Zielcomputer verwendet.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Hiermit wird die DNS-Suchreihenfolge für den Zielcomputer angegeben.

### <a name="osddomainname"></a><a name="OSDDomainName"></a> OSDDomainName

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Gibt den Namen der Active Directory-Domäne an, der der Zielcomputer beitritt. Der angegebene Wert muss ein gültiger Active Directory-Domänendienste-Domänenname sein.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a> OSDDomainOUName

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Hiermit wird der Name der Organisationseinheit, der der Zielcomputers hinzugefügt wird, im RFC 1779-Format angegeben. Wenn dieser Parameter angegeben wird, muss die Zeichenfolge einen vollständigen Pfad enthalten.

#### <a name="example"></a>Beispiel

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
*Gilt für den Schritt [Paket installieren](task-sequence-steps.md#BKMK_InstallPackage).*

*Ab Version 1902*  
*Gilt für den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).*

(Eingabe)

Wenn Sie verhindern möchten, dass möglicherweise vertrauliche Daten angezeigt oder protokolliert werden, legen Sie diese Variable auf `TRUE` fest. Diese Variable verbirgt den Programmnamen in **smsts.log** während des Schritts **Paket installieren**.

Wenn Sie diese Variable auf `TRUE` festlegen, wird ab Version 1902 auch die Befehlszeile aus dem Schritt **Befehlszeile ausführen** in der Protokolldatei ausgeblendet.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Hiermit wird angegeben, ob der TCP/IP-Filter aktiviert wird.

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false` (Standard)  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Gilt für den Schritt [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(Eingabe)

Gibt an, ob eine EFI-Partition auf einer GPT-Festplatte erstellt werden soll. EFI-basierte Computer verwenden diese Partition als Startdatenträger.

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false` (Standard)

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a> OSDImageCreator

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(Eingabe)

Dies ist ein optionaler Name des Benutzers, der das Abbild erstellt hat. Dieser Name wird in der WIM-Datei gespeichert. Die maximale Länge des Benutzernamens beträgt 255 Zeichen.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a> OSDImageDescription

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(Eingabe)

Eine optionale benutzerdefinierte Beschreibung des erfassten Betriebssystemimages. Diese Beschreibung wird in der WIM-Datei gespeichert. Die maximale Länge der Beschreibung beträgt 255 Zeichen.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a> OSDImageIndex

*Gilt für den Schritt [Betriebssystemimage anwenden](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(Eingabe)

Gibt den Imageindexwert der WIM-Datei an, die auf den Zielcomputer angewendet wird.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a> OSDImageVersion

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(Eingabe)

Diese optionale benutzerdefinierte Versionsnummer wird dem erfassten Betriebssystemimage zugewiesen. Diese Versionsnummer wird in der WIM-Datei gespeichert. Dieser Wert kann eine beliebige Kombination aus alphanumerischen Zeichen und maximal 32 Zeichen lang sein.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Gilt für den Schritt [Treiberpaket anwenden](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(Eingabe)

Gibt zusätzliche Optionen an, die beim Anwenden eines Treiberpakets der DISM-Befehlszeile hinzugefügt werden. Die Tasksequenz überprüft nicht die Befehlszeilenoptionen.

Um diese Variable zu verwenden, aktivieren Sie in Schritt **Treiberpaket anwenden** die Einstellung **Treiberpaket über ausgeführten DISM mit rekursiver Option installieren**.

Weitere Informationen finden Sie unter [Windows 10-DISM-Befehlszeilenoptionen](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a> OSDJoinAccount

*Gilt für die folgenden Schritte:*  

- [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(Eingabe)

Gibt das Domänennutzerkonto an, mit dem der Zielcomputer der Domäne hinzugefügt wird. Diese Variable ist für den Beitritt zu einer Domäne erforderlich.

Weitere Informationen zum Tasksequenz-Domänenbeitrittskonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Gilt für den Schritt [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(Eingabe)

Gibt den Namen einer Active Directory-Domäne an, der der Zielcomputer hinzugefügt wird. Der Domänenname muss zwischen 1 und 255 Zeichen enthalten.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Gilt für den Schritt [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(Eingabe)

Hiermit wird der Name der Organisationseinheit, der der Zielcomputers hinzugefügt wird, im RFC 1779-Format angegeben. Wenn dieser Parameter angegeben wird, muss die Zeichenfolge einen vollständigen Pfad enthalten. Der Name der Organisationseinheit muss zwischen 0 und 32.767 Zeichen enthalten. Dieser Wert wird nicht festgelegt, wenn die Variable [OSDJoinType](#OSDJoinType) auf `1` (Arbeitsgruppe beitreten) festgelegt ist.

#### <a name="example"></a>Beispiel

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a> OSDJoinPassword

*Gilt für die folgenden Schritte:*  

- [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(Eingabe)

Gibt das Kennwort für [OSDJoinAccount](#OSDJoinAccount) an, mit dem der Zielcomputer der Active Directory-Domäne beitritt. Wenn diese Variable in der Tasksequenzumgebung nicht enthalten ist, versucht Windows Setup die Eingabe eines leeren Kennworts. Dieser Wert ist erforderlich, wenn die Variable [OSDJoinType](#OSDJoinType) den Wert `0` (Domäne beitreten) aufweist.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Gilt für den Schritt [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(Eingabe)

Hiermit wird angegeben, ob der Neustart des Zielcomputers nach dessen Beitritt zur Domäne oder Arbeitsgruppe übersprungen werden soll.

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a> OSDJoinType

*Gilt für den Schritt [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(Eingabe)

Hiermit wird angegeben, ob der Zielcomputer einer Windows-Domäne oder einer Arbeitsgruppe hinzugefügt wird.

#### <a name="valid-values"></a>Gültige Werte

- `0`: Der Zielcomputer wird einer Windows-Domäne hinzugefügt  
- `1`: Der Zielcomputer wird einer Arbeitsgruppe hinzugefügt  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Gilt für den Schritt [Einer Domäne oder Arbeitsgruppe beitreten](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(Eingabe)

Hiermit wird der Name einer Arbeitsgruppe angegeben, der der Zielcomputer hinzugefügt wird. Der Name der Arbeitsgruppe muss zwischen 1 und 32 Zeichen enthalten.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a> OSDKeepActivation

*Gilt für den Schritt [Windows für die Erfassung vorbereiten](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

(Eingabe)

Hiermit wird angegeben, ob das Produktaktivierungskennzeichen von Sysprep beibehalten oder zurückgesetzt wird.

#### <a name="valid-values"></a>Gültige Werte

- `true`: Aktivierungskennzeichen beibehalten
- `false` (Standardwert): Aktivierungskennzeichen zurücksetzen

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(Eingabe)

Gibt das Kennwort für das lokale Administratorkonto an. Wenn Sie die Option **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren** aktivieren, wird diese Variable in dem Schritt ignoriert. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
*Ab Version 1902*  
*Gilt für den Schritt [PowerShell-Skript ausführen](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(Eingabe)

Wenn Sie verhindern möchten, dass möglicherweise vertrauliche Daten protokolliert werden, werden im Schritt **PowerShell-Skript ausführen** keine Skriptparameter in der Datei **smsts.log** protokolliert. Legen Sie diese Variable auf **TRUE** fest, wenn Sie die Skriptparameter ins Tasksequenzprotokoll aufnehmen möchten.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Gilt für den Schritt [Netzwerkeinstellungen erfassen](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(Eingabe)

Gibt an, ob die Tasksequenz, die Netzwerkadapterinformationen erfasst. Diese Informationen umfassen die Konfigurationseinstellungen für TCP/IP, DNS und WINS.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard)
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*Gilt für den Schritt [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).*

(Eingabe)

Gibt zusätzliche Befehlszeilenoptionen für das Migrationstool für den Benutzerstatus (USMT) an, mit dem die Tasksequenz den Benutzerstatus erfasst. In dem Schritt werden diese Einstellungen im Tasksequenz-Editor nicht verfügbar gemacht. Geben Sie diese Optionen als Zeichenfolge an, die die Tasksequenz der automatisch generierten USMT-Befehlszeile für ScanState anhängt.

Die USMT-Optionen, die mit dieser Tasksequenzvariablen angegeben werden, werden vor dem Ausführen der Tasksequenz nicht auf Genauigkeit überprüft.

Weitere Informationen zu verfügbaren Optionen finden Sie unter [ScanState-Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*Gilt für den Schritt [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState).*

(Eingabe)

Gibt zusätzliche Befehlszeilenoptionen für das Migrationstool für den Benutzerstatus (USMT) an, mit dem die Tasksequenz den Benutzerstatus wiederherstellt. Geben Sie die zusätzlichen Optionen als Zeichenfolge an, die die Tasksequenz der automatisch generierten USMT-Befehlszeile für LoadState anhängt.

Die USMT-Optionen, die mit dieser Tasksequenzvariablen angegeben werden, werden vor dem Ausführen der Tasksequenz nicht auf Genauigkeit überprüft.

Weitere Informationen zu verfügbaren Optionen finden Sie unter [LoadState-Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Gilt für den Schritt [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(Eingabe)

Hiermit wird angegeben, ob der Computername migriert wird.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard). Die Variable [OSDComputerName (Ausgabe)](#OSDComputerName-output) wird auf den NetBIOS-Namen des Computers festgelegt.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Gilt für den Schritt [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).*

(Eingabe)

Gibt die Konfigurationsdateien an, mit denen die Erfassung von Benutzerprofilen gesteuert wird. Diese Variable wird nur verwendet, wenn [OSDMigrateMode](#OSDMigrateMode) auf `Advanced` festgelegt ist. Dieser durch Kommas getrennte Listenwert wird festgelegt, um die Migration benutzerdefinierter Benutzerprofile auszuführen.

#### <a name="example"></a>Beispiel

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Gilt für den Schritt [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).*

(Eingabe)

Wenn USMT einige Dateien nicht erfassen kann, lässt diese Variable zu, dass die Erfassung des Benutzerstatus fortgesetzt wird.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard)  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Gilt für den Schritt [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState).*

(Eingabe)

Der Prozess wird fortgesetzt, auch wenn USMT einige Dateien nicht wiederherstellen kann.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard)  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Gilt für die folgenden Schritte:*  

- [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState)  

(Eingabe)

Aktiviert die ausführliche Protokollierung für USMT. Der Schritt benötigt diesen Wert.

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false` (Standard)  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Gilt für den Schritt [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState).*

(Eingabe)

Hiermit wird angegeben, ob das lokale Computerkonto wiederhergestellt werden soll.

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false` (Standard)  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Gilt für den Schritt [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState).*

(Eingabe)

Wenn die Variable [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) auf `true` festgelegt ist, muss diese Variable das Kennwort enthalten, das *allen* migrierten lokalen Konten zugewiesen ist. USMT weist allen migrierten lokalen Konten das gleiche Kennwort zu. Betrachten Sie dieses als vorübergehendes Kennwort, und ändern Sie es später mit einer anderen Methode.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a> OSDMigrateMode

*Gilt für den Schritt [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).*

(Eingabe)

Ermöglicht das Anpassen der Dateien, die USMT erfasst.

#### <a name="valid-values"></a>Gültige Werte

- `Simple`: Die Tasksequenz verwendet nur die USMT-Standardkonfigurationsdateien  

- `Advanced`: Die Tasksequenzvariable [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) gibt die von USMT verwendeten Konfigurationsdateien an.  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Gilt für den Schritt [Netzwerkeinstellungen erfassen](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(Eingabe)

Gibt an, ob die Tasksequenz die Informationen zur Arbeitsgruppen- oder Domänenmitgliedschaft migriert.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard)
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Gilt für den Schritt [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(Eingabe)

Gibt an, ob in dem Schritt Benutzer- und Organisationsinformationen migriert werden.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard). Die Variable [OSDRegisteredOrgName (Ausgabe)](#OSDRegisteredOrgName-output) ist auf den registrierten Organisationsnamen des Computers festgelegt.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Gilt für den Schritt [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState).*

(Eingabe)

Hiermit wird angegeben, ob verschlüsselte Dateien erfasst werden.

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false` (Standard)  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Gilt für den Schritt [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(Eingabe)

Hiermit wird angegeben, ob die Zeitzone des Computers migriert wird.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard). Die Variable [OSDTimeZone (Ausgabe)](#OSDTimeZone-output) ist auf die Zeitzone des Computers festgelegt.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Gibt an, ob der Zielcomputer einer Active Directory-Domäne oder einer Arbeitsgruppe beitritt.

#### <a name="value-values"></a>Gültige Werte

- `0`: Beitritt zu einer Active Directory-Domäne  
- `1`: Einer Arbeitsgruppe beitreten

### <a name="osdpartitions"></a><a name="OSDPartitions"></a> OSDPartitions

*Gilt für den Schritt [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(Eingabe)

Diese Tasksequenzvariable ist eine Arrayvariable der Partitionseinstellungen. Die einzelnen Elemente im Array stellen die Einstellungen für eine einzelne Partition auf der Festplatte dar. Die Einstellungen, die für jede Partition definiert sind, können aufgerufen werden, indem der Name der Arrayvariablen mit der Null-basierten Nummer der Festplattenpartition und dem Eigenschaftennamen kombiniert wird.

Verwenden Sie die folgenden Variablennamen, um die Eigenschaften für die *erste* Partition zu definieren, die in diesem Schritt auf der Festplatte erstellt werden:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Gibt den Partitionstyp an. Diese Eigenschaft ist erforderlich. Gültige Werte sind `Primary`, `Extended`, `Logical` und `Hidden`.

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Gibt den Typ des Dateisystems an, das zum Formatieren der Partition verwendet wird. Diese Eigenschaft ist optional. Wenn Sie kein Dateisystem angeben, wird die Partition in diesem Schritt nicht formatiert. Gültige Werte sind `FAT32` und `NTFS`.

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Gibt an, ob die Partition startbar ist. Diese Eigenschaft ist erforderlich. Wenn der Wert für MBR-Datenträger auf `TRUE` festgelegt ist, wird diese Partition in dem Schritt als „aktiv“ gekennzeichnet.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Gibt den Typ des verwendeten Formats an. Diese Eigenschaft ist erforderlich. Wenn dieser Wert auf `TRUE` festgelegt ist, wird in dem Schritt eine Schnellformatierung ausgeführt. Andernfalls umfasst der Schritt eine vollständige Formatierung.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Gibt den Namen an, der dem Volume beim Formatieren zugewiesen wird. Diese Eigenschaft ist optional.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Gibt die Größe der Partition an. Diese Eigenschaft ist optional. Wenn diese Eigenschaft nicht angegeben wird, wird die Partition mit dem gesamten verbleibenden freien Speicherplatz erstellt. Einheiten werden von der Variablen **OSDPartitions0SizeUnits** angegeben.

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

Diese Einheiten werden in dem Schritt verwendet, um die Variable **OSDPartitions0Size** zu interpretieren. Diese Eigenschaft ist optional. Gültige Werte sind `MB` (Standard), `GB` und `Percent`.

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Wenn in diesem Schritt Partitionen erstellt werden, wird immer der nächste verfügbare Laufwerkbuchstabe in Windows PE verwendet. Verwenden Sie diese optionale Eigenschaft, um den Namen einer anderen Tasksequenzvariablen anzugeben. Mithilfe dieser Variablen wird in dem Schritt der neue Laufwerkbuchstabe zur späteren Referenz gespeichert.

Wenn Sie in diesem Tasksequenzschritt mehrere Partitionen definieren, werden die Eigenschaften für die *zweite* Partition über den Index **1** im Variablennamen definiert. Beispiel: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** und **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Gilt für den Schritt [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(Eingabe)

Gibt den bei der Partitionierung des Datenträgers zu verwendenden Partitionsstil an.

#### <a name="valid-values"></a>Gültige Werte

- `GPT`: Der Stil „GUID-Partitionstabelle“ wird verwendet
- `MBR`: Der Partitionsstil „Master Boot Record (MBR)“ wird verwendet

### <a name="osdproductkey"></a><a name="OSDProductKey"></a> OSDProductKey

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(Eingabe)

Gibt den Windows-Product Key an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(Eingabe)

Gibt ein zufällig generiertes Kennwort für das lokale Administratorkonto im neuen Betriebssystem an.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard): Windows Setup deaktiviert das lokale Administratorkonto auf dem Zielcomputer.  

- `false`: Windows Setup aktiviert das lokale Administratorkonto auf dem Zielcomputer und legt den Wert von [OSDLocalAdminPassword](#OSDLocalAdminPassword) als Kontokennwort fest.  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (Eingabe)

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Gibt den registrierten Standardorganisationsnamen im neuen Betriebssystem an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (Ausgabe)

*Gilt für den Schritt [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Auf den registrierten Organisationsnamen des Computers festlegen. Der Wert wird nur festgelegt, wenn die Variable [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) auf `true` festgelegt ist.

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(Eingabe)

Gibt den registrierten Standardbenutzernamen im neuen Betriebssystem an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(Eingabe)

Gibt die Anzahl der maximal zulässigen Verbindungen an. Die angegebene Zahl muss zwischen 5 und 9999 liegen.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(Eingabe)

Gibt den verwendeten Windows Server-Lizenzmodus an.

#### <a name="valid-values"></a>Gültige Werte

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Gilt für den Schritt [Betriebssystem aktualisieren](task-sequence-steps.md#BKMK_UpgradeOS).*

(Eingabe)

Gibt die zusätzlichen Befehlszeilenoptionen an, die während eines Windows 10-Upgrades zu Windows Setup hinzugefügt werden. Die Tasksequenz überprüft nicht die Befehlszeilenoptionen.

Weitere Informationen finden Sie unter [Windows Setup-Befehlszeilenoptionen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Gilt für den Schritt [Statusspeicher anfordern](task-sequence-steps.md#BKMK_RequestStateStore).*

(Eingabe)

Wenn das Computerkonto keine Verbindung mit dem Statusmigrationspunkt herstellen kann, gibt diese Variable an, ob die Tasksequenz das Netzwerkzugriffskonto als Ausweichmöglichkeit verwenden soll.

Weitere Informationen zum Netzwerkzugriffskonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Gültige Werte

- `true`  
- `false` (Standard)  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Gilt für den Schritt [Statusspeicher anfordern](task-sequence-steps.md#BKMK_RequestStateStore).*

(Eingabe)

Hiermit wird angegeben, wie viele Wiederholungsversuche des Tasksequenzschritts zum Suchen eines Zustandsmigrationspunkts ausgeführt werden, bevor der Schritt mit einem Fehler abgebrochen wird. Die angegebene Anzahl muss zwischen 0 und 600 liegen.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Gilt für den Schritt [Statusspeicher anfordern](task-sequence-steps.md#BKMK_RequestStateStore).*

(Eingabe)

Hiermit wird angegeben, wie viele Sekunden zwischen den einzelnen Versuchen des Tasksequenzschritts gewartet werden soll. Die Anzahl der Sekunden darf maximal 30 Zeichen umfassen.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a> OSDStateStorePath

*Gilt für die folgenden Schritte:*  

- [Benutzerstatus erfassen](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Statusspeicher freigeben](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Statusspeicher anfordern](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Benutzerstatus wiederherstellen](task-sequence-steps.md#BKMK_RestoreUserState)  

(Eingabe)

Der Name der Netzwerkfreigabe oder des lokale Pfads des Ordners, in dem die Tasksequenz den Benutzerstatus speichert oder wiederherstellt. Es gibt keinen Standardwert.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Gilt für den Schritt [Betriebssystemimage anwenden](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(Ausgabe)

Gibt den Laufwerkbuchstaben der Partition an, die nach Anwendung des Images die Betriebssystemdateien enthält.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (Eingabe)

*Gilt für den Schritt [Betriebssystemimage erfassen](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

Gibt den Pfad zum Windows-Verzeichnis des installierten Betriebssystems auf dem Referenzcomputer an. Die Tasksequenz überprüft, ob das Betriebssystem für die Erfassung durch Configuration Manager unterstützt wird.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (Ausgabe)

*Gilt für den Schritt [Windows für die Erfassung vorbereiten](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

Gibt den Pfad zum Windows-Verzeichnis des installierten Betriebssystems auf dem Referenzcomputer an. Die Tasksequenz überprüft, ob das Betriebssystem für die Erfassung durch Configuration Manager unterstützt wird.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a> OSDTimeZone (Eingabe)

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Gibt die Standardeinstellung für die Zeitzone an, die im neuen Betriebssystem verwendet wird.

Legen Sie den Wert dieser Variablen auf den invarianten Sprachennamen der Zeitzone fest. Verwenden Sie die Zeichenfolge z.B. im `Std`-Wert für eine Zeitzone unterhalb des folgenden Registrierungsschlüssels: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a> OSDTimeZone (Ausgabe)

*Gilt für den Schritt [Windows-Einstellungen erfassen](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Diese Variable wird auf die Zeitzone des Computers festgelegt. Der Wert wird nur festgelegt, wenn die Variable [OSDMigrateTimeZone](#OSDMigrateTimeZone) auf `true` festgelegt ist.

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a> OSDWindowsSettingsInputLocale

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Diese Variable gibt die Standardeinstellung für das Eingabegebietsschema an, die im neuen Betriebssystem verwendet wird.

Weitere Informationen zu diesem Wert für die Antwortdatei des Windows-Setups finden Sie unter [Microsoft-Windows-International-Core – InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a> OSDWindowsSettingsSystemLocale

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Gibt die Standardeinstellung für das Systemgebietsschema an, die im neuen Betriebssystem verwendet wird.

Weitere Informationen zu diesem Wert für die Antwortdatei des Windows-Setups finden Sie unter [Microsoft-Windows-International-Core – SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a> OSDWindowsSettingsUILanguage

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Diese Variable gibt die Standardeinstellung für die Benutzeroberflächensprache an, die im neuen Betriebssystem verwendet wird.

Weitere Informationen zu diesem Wert für die Antwortdatei des Windows-Setups finden Sie unter [Microsoft-Windows-International-Core – UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a> OSDWindowsSettingsUILanguageFallback

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Diese Variable gibt die Fallbackeinstellung für die Benutzeroberflächensprache an, die im neuen Betriebssystem verwendet wird.

Weitere Informationen zu diesem Wert für die Antwortdatei des Windows-Setups finden Sie unter [Microsoft-Windows-International-Core – UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a> OSDWindowsSettingsUserLocale

*Gilt für den Schritt [Windows-Einstellungen anwenden](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Diese Variable gibt die Standardeinstellung für das Benutzergebietsschema an, die im neuen Betriebssystem verwendet wird.

Weitere Informationen zu diesem Wert für die Antwortdatei des Windows-Setups finden Sie unter [Microsoft-Windows-International-Core – UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Gilt für den Schritt [Datenimage anwenden](task-sequence-steps.md#BKMK_ApplyDataImage).*

(Eingabe)

Hiermit wird angegeben, ob die auf der Zielpartition vorhandenen Dateien gelöscht werden sollen.

#### <a name="valid-values"></a>Gültige Werte

- `true` (Standard)
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Gilt für den Schritt [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(Eingabe)

Hiermit wird der Name der Arbeitsgruppe angegeben, der der Zielcomputer hinzugefügt wird.

Geben Sie entweder diese Variable oder die Variable [OSDDomainName](#OSDDomainName) an. Der Name der Arbeitsgruppe darf maximal 32 Zeichen umfassen.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a> SetupCompletePause

*Gilt für den Schritt [Betriebssystem aktualisieren](task-sequence-steps.md#BKMK_UpgradeOS).*

<!-- 4680263 -->

Ab Version 1910 kann diese Variable verwendet werden, um Zeitsteuerungsprobleme bei der Tasksequenz für das direkte Upgrade von Windows 10 auf Hochleistungsgeräten zu behandeln, wenn das Windows-Setup abgeschlossen ist. Wenn Sie dieser Variablen einen Wert in Sekunden zuweisen, wartet der Windows-Setupvorgang diese Zeitspanne, bevor die Tasksequenz gestartet wird. Mit diesem Timeout erhält der Configuration Manager-Client zusätzliche Zeit für die Initialisierung.

Die folgenden Protokolleinträge sind gängige Beispiele für dieses Problem, die sich mit dieser Variablen behandeln lassen:

- Die TSManager-Komponente zeichnet Einträge ähnlich den folgenden Fehlern in der Datei **smsts.log** auf:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- In Windows Setup werden Einträge ähnlich den folgenden Fehlern in der Datei **setupcomplete.log** aufgezeichnet:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Gilt für den Schritt [Windows und ConfigMgr einrichten](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).*

(Eingabe)

Gibt die Eigenschaften der Clientinstallation an, die die Tasksequenz beim Installieren des Configuration Manager-Clients verwendet.

Weitere Informationen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation ](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Gilt für den Schritt [Verbindung mit Netzwerkordner herstellen](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(Eingabe)

Gibt das Administratorkonto an, über das eine Verbindung mit der Netzwerkfreigabe in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) hergestellt wird. Geben Sie das Kontokennwort mit dem Wert [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) an.

Weitere Informationen zu Netzwerkorder-Verbindungskonten der Tasksequenz finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Gilt für den Schritt [Verbindung mit Netzwerkordner herstellen](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(Eingabe)

Gibt den Laufwerkbuchstaben des Netzwerks an, mit dem eine Verbindung hergestellt werden soll. Dieser Wert ist optional. Wenn er nicht angegeben ist, wird die Netzwerkverbindung keinem Laufwerkbuchstaben zugeordnet. Wenn dieser Wert angegeben wird, muss der Wert im Bereich „D–Z“ liegen. Verwenden Sie nicht „X“, weil dieser Laufwerkbuchstabe während der Windows PE-Phase von Windows PE verwendet wird.

#### <a name="examples"></a>Beispiele

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Gilt für den Schritt [Verbindung mit Netzwerkordner herstellen](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(Eingabe)

Gibt das Kennwort für [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) an, worüber eine Verbindung mit der Netzwerkfreigabe in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) hergestellt wird.

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Gilt für den Schritt [Verbindung mit Netzwerkordner herstellen](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(Eingabe)

Gibt den Netzwerkpfad für die Verbindung an. Wenn Sie diesen Pfad einem Laufwerkbuchstaben zuordnen müssen, verwenden Sie den [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter)-Wert.

#### <a name="example"></a>Beispiel

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Gilt für den Schritt [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(Eingabe)

Hiermit wird angegeben, ob sämtliche Updates oder nur obligatorische Updates installiert werden sollen.

#### <a name="valid-values"></a>Gültige Werte

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a> SMSRebootMessage

*Gilt für den Schritt [Computer neu starten](task-sequence-steps.md#BKMK_RestartComputer).*

(Eingabe)

Hiermit wird die Nachricht angegeben, die den Benutzern vor dem Neustart des Zielcomputers angezeigt wird. Wenn diese Variable nicht festgelegt ist, wird die Standardnachricht angezeigt. Die angegebene Meldung darf 512 Zeichen nicht überschreiten.

#### <a name="example"></a>Beispiel

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Gilt für den Schritt [Computer neu starten](task-sequence-steps.md#BKMK_RestartComputer).*

(Eingabe)

Gibt die Anzeigedauer der Warnmeldung an den Benutzer in Sekunden an, bis der Computer neu gestartet wird.

#### <a name="examples"></a>Beispiele

- `0` (Standard): Es wird keine Neustartmeldung angezeigt  
- `60`: Die Warnung wird eine Minute lang angezeigt  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

Die Wartezeit in Sekunden, nach der vom Client nach dem letzten erfolglosen Versuch ein neuer Versuch zum Herunterladen der Richtlinie unternommen wird. Standardmäßig wartet der Client **0** Sekunden, bevor er einen neuen Versuch startet.

Sie können diese Variable festlegen, indem Sie einen Prestart-Befehl von einem Medium oder per PXE verwenden.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

Die Anzahl der Versuche eines Clients, die Richtlinie herunterzuladen, nachdem beim ersten Versuch keine Richtlinien gefunden wurden. Standardmäßig startet der Client **0** neue Versuche.

Sie können diese Variable festlegen, indem Sie einen Prestart-Befehl von einem Medium oder per PXE verwenden.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Gibt an, auf welche Weise die Zuordnung zwischen Benutzern und dem Zielcomputer durch die Tasksequenz erfolgt. Legen Sie einen der folgenden Werte für die Variable fest:  

- **Automatisch:** Wenn die Tasksequenz das Betriebssystem auf dem Zielcomputer bereitstellt, erstellt sie auch eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer.  

- **Ausstehend:** Die Tasksequenz erstellt eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer. Ein Administrator muss die Beziehung genehmigen, damit sie festgelegt werden kann.  

- **Deaktiviert:** Die Tasksequenz verknüpft Benutzer bei der Betriebssystembereitstellung nicht mit dem Zielcomputer.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
In getrennten Szenarien versucht das Tasksequenzmodul wiederholt, Statusmeldungen an den Verwaltungspunkt zu senden. Dieses Verhalten in diesem Szenario führt zu Verzögerungen bei der Verarbeitung von Tasksequenzen.

Legen Sie diese Variable auf `true` fest. Dann versucht die Tasksequenz-Engine nicht, Statusmeldungen zu senden, nachdem beim Senden der ersten Meldung ein Fehler aufgetreten ist. Der erste Versuch umfasst mehrere Wiederholungen.

Wenn die Tasksequenz neu gestartet wird, bleibt der Wert dieser Variable erhalten. Die Tasksequenz versucht jedoch eine Meldung des Anfangsstatus zu senden. Der erste Versuch umfasst mehrere Wiederholungen. Bei Erfolg sendet die Tasksequenz unabhängig vom Wert dieser Variable weiterhin Statusmeldungen. Wenn der Status nicht gesendet werden kann, verwendet die Tasksequenz den Wert dieser Variable.

> [!NOTE]  
> Die [Tasksequenz-Statusberichterstattung](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) benötigt diese Statusmeldungen, um Status, Verlauf und Details der einzelnen Schritte anzuzeigen. Wenn Statusmeldungen nicht gesendet werden, werden sie nicht in der Warteschlange platziert. Zu einem späteren Zeitpunkt, wenn die Konnektivität für den Verwaltungspunkt wiederhergestellt ist, werden die Meldungen nicht gesendet. Dieses Verhalten hat zur Folge, dass ein Tasksequenzstatus als unvollständig gemeldet wird.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Gilt für den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).*

(Eingabe)

Auf einem 64-Bit-Betriebssystem sucht und führt die Tasksequenz das Programm standardmäßig in der Befehlszeile unter Verwendung des WOW64-Dateisystemredirectors aus. Dieses Verhalten ermöglicht dem Befehl, 32-Bit-Versionen der Betriebssystemprogramme und DLLs zu ermitteln. Wenn Sie diese Variable auf `true` festlegen, wird die Verwendung des WOW64-Dateisystemredirectors deaktiviert. Der Befehl findet native 64-Bit-Versionen der Betriebssystemprogramme und DLLs. Unter einem 32-Bit-Betriebssystem hat diese Variable keine Auswirkungen.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

Diese Variable enthält den Abbruchscodewert für das externe Downloadprogramm. Dieses Programm wird in der Variablen [SMSTSDownloadProgram](#SMSTSDownloadProgram) angegeben. Wenn das Programm einen Fehlercode zurückgibt, der dem Wert der SMSTSDownloadAbortCode-Variablen entspricht, dann schlägt der Download des Inhalts fehl, und es wird keine Downloadmethode versucht.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

Geben Sie mit dieser Variablen einen alternativen Inhaltsanbieter an. Ein alternativer Inhaltsanbieter ist ein Downloadprogramm zum Herunterladen von Inhalten. Die Tasksequenz verwendet den alternativen Inhaltsanbieter anstelle des Configuration Manager-Standarddownloadprogramms. Beim Herunterladen von Inhalten überprüft die Tasksequenz diese Variable. Wenn ein Programm angegeben ist, wird es von der Tasksequenz ausgeführt, um Inhalte herunterzuladen.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

Die Anzahl der Versuche, die Configuration Manager startet, um den Inhalt von einem Verteilungspunkt herunterzuladen. Standardmäßig startet der Client **2** neue Versuche.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

Die Wartezeit von Configuration Manager in Sekunden, bevor erneut versucht wird, Inhalt von einem Verteilungspunkt herunterzuladen. Standardmäßig wartet der Client **15** Sekunden, bevor er einen neuen Versuch startet.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Gilt für den Schritt [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Bei der Anforderung des Treiberkatalogs ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf die HTTP-Serververbindung wartet. Wenn das Timeout beim Herstellen der Verbindung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **60** Sekunden festgelegt.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Gilt für den Schritt [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Bei der Anforderung des Treiberkatalogs ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf eine Antwort wartet. Wenn das Timeout beim Herstellen der Verbindung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **480** Sekunden festgelegt.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Gilt für den Schritt [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Bei der Anforderung des Treiberkatalogs ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf die HTTP-Namensauflösung wartet. Wenn das Timeout beim Herstellen der Verbindung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **60** Sekunden festgelegt.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Gilt für den Schritt [Treiber automatisch anwenden](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Beim Senden einer Anforderung an den Treiberkatalog ist diese Variable die Anzahl der Sekunden, die die Tasksequenz auf das Senden der Anforderung wartet. Wenn das Timeout beim Senden der Anforderung überschritten wird, wird die Anforderung durch die Tasksequenz abgebrochen. Standardmäßig ist das Timeout auf **60** Sekunden festgelegt.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

Sobald ein Fehler in einer Tasksequenz auftritt, wird ein Dialogfeld mit der Fehlermeldung angezeigt. Nach Ablauf der Sekunden, die durch diese Variable festgelegt sind, wird diese Meldung automatisch von der Tasksequenz verworfen. Der Standardwert beträgt **900** Sekunden (15 Minuten).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

Verwenden Sie diese Variable, um die Anzeigesprache eines sprachneutralen Startimage zu ändern.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Gibt an, wo die Tasksequenz während der Ausführung temporäre Cachedateien auf dem Zielcomputer speichert.

Legen Sie diese Variable fest, bevor die Tasksequenz gestartet wird, indem Sie beispielsweise eine Sammlungsvariable bestimmen. Nach dem Start der Tasksequenz definiert Configuration Manager die [_SMSTSMDataPath](#SMSTSMDataPath)-Variable basierend darauf, wofür die SMSTSLocalDataDrive-Variable definiert wurde.

### <a name="smstsmp"></a><a name="SMSTSMP"></a> SMSTSMP

Verwenden Sie diese Variable zum Angeben der URL oder der IP-Adresse eines Configuration Manager-Verwaltungspunkts

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Gilt für die folgenden Schritte:*  

- [Anwendung installieren](task-sequence-steps.md#BKMK_InstallApplication)  
- [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(Eingabe)

Wenn der Client sich nicht im Intranet befindet, verwenden Sie diese Variable, um wiederholte Anforderungen der Verwaltungspunktliste zur Aktualisierung des Clients zu ermöglichen. Dieser Wert ist standardmäßig auf `True` festgelegt.

Wenn Clients sich im Internet befinden, legen Sie diese Variable auf `False` fest, um unnötige Verzögerungen zu vermeiden.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Gilt für die folgenden Schritte:*  

- [Anwendung installieren](task-sequence-steps.md#BKMK_InstallApplication)  
- [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(Eingabe)

Wenn die Tasksequenz die Verwaltungspunktliste aus den Ortungsdiensten nicht abrufen kann, gibt diese Variable an, wie viele Millisekunden eine Tasksequenz wartet, bevor der Schritt wiederholt wird. Standardmäßig wartet die Tasksequenz `60000` Millisekunden (60 Sekunden), bevor sie den Schritt wiederholt. Sie führt bis zu drei Wiederholungen aus.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Verwenden Sie diese Variable, um dem Client die Verwendung des Windows PE-Peercaches zu ermöglichen. Diese Funktion ist verfügbar, wenn Sie diese Variable auf `true` festlegen.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Ein benutzerdefinierter Netzwerkport, den der Windows PE-Peercache für die erste Übertragung verwendet. Der in den Clienteinstellungen konfigurierte Standardport ist **8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a> SMSTSPersistContent

Verwenden Sie diese Variable, um Inhalt im Tasksequenzcache vorübergehend beizubehalten. Diese Variable unterscheidet sich von [SMSTSPreserveContent](#SMSTSPreserveContent): „SMSTSPreserveContent“ bewahrt Inhalte im Configuration Manager-Clientcache auf, nachdem die Tasksequenz abgeschlossen wurde. „SMSTSPersistContent “ verwendet den Tasksequenzcache, während „SMSTSPreserveContent“ auf den Cache des Configuration Manager-Clients zugreift.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a> SMSTSPostAction

Gibt einen Befehl an, der nach Abschluss der Tasksequenz ausgeführt wird. Geben Sie beispielsweise `shutdown.exe /r /t 30 /f` an, um den Computer 30 Sekunden nach Abschluss der Tasksequenz neu zu starten.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Zwingt die Tasksequenz zur Ausführung einer bestimmten zielgerichteten Bereitstellung auf dem Zielcomputer. Legen Sie diese Variable durch einen Prestart-Befehl von einem Medium oder über PXE fest. Wenn diese Variable festgelegt ist, setzt die Tasksequenz alle erforderlichen Bereitstellungen außer Kraft.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

Diese Variable kennzeichnet Inhalte in der Tasksequenz, die nach der Bereitstellung im Configuration Manager-Clientcache erhalten bleiben sollen. Diese Variable unterscheidet sich von [SMSTSPersistContent](#SMSTSPersistContent): „SMSTSPersistContent“ bewahrt Inhalte nur solange auf, wie die Tasksequenz ausgeführt wird. „SMSTSPersistContent “ verwendet den Tasksequenzcache, während „SMSTSPreserveContent“ auf den Cache des Configuration Manager-Clients zugreift. Legen Sie „SMSTSPreserveContent“ auf `true` fest, damit diese Funktion verfügbar ist.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Gibt an, nach wie vielen Sekunden der Computer neu gestartet wird. Wenn diese Variable auf „0“ festgelegt ist, zeigt der Tasksequenz-Manager vor einem Neustart kein Benachrichtigungsdialogfeld an.

#### <a name="example"></a>Beispiel

- `0`: keine Benachrichtigung anzeigen  

- `60`: Benachrichtigung eine Minute anzeigen  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a> SMSTSRebootDelayNext

<!--4447680-->
Ab Version 1906 kann diese Variable mit der vorhandenen [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay)-Variablen verwendet werden. Wenn bei späteren Neustarts ein anderes Timeout verwendet werden soll als beim ersten Neustart, legen Sie „SMSTSRebootDelayNext“ auf einen anderen Sekundenwert fest.

#### <a name="example"></a>Beispiel

Dadurch können Sie Benutzer beim Start einer Tasksequenz für ein direktes Windows 10-Upgrade darauf aufmerksam machen, dass in 60 Minuten ein Neustart erfolgt. Nach diesem ersten langen Timeout sollen weitere Timeouts dann nur noch 60 Sekunden betragen. Legen Sie „SMSTSRebootDelay“ auf `3600` und „SMSTSRebootDelayNext“ auf `60` fest.  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Legt die Meldung fest, die im Benachrichtigungsdialogfeld beim Neustart angezeigt wird. Wenn diese Variable nicht festgelegt ist, wird eine Standardmeldung angezeigt.

#### <a name="example"></a>Beispiel

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

Gibt an, dass nach Abschluss des aktuellen Tasksequenzschritts ein Neustart erforderlich ist. Wenn der Tasksequenzschritt einen Neustart zum Abschließen der Aktion erfordert, legen Sie diese Variable fest. Nach dem Neustart des Computers wird die Tasksequenz mit dem nächsten Tasksequenzschritt fortgesetzt.

- `HD`: Neustart für das installierte Betriebssystem
- `WinPE`: Neustart für das verknüpfte Startabbild

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Fordert eine Wiederholung an, nachdem der aktuelle Tasksequenzschritt abgeschlossen ist. Wenn diese Tasksequenzvariable festgelegt ist, muss die Variable [SMSTSRebootRequested](#SMSTSRebootRequested) auf `true` festgelegt werden. Nach dem Computerneustart führt der Tasksequenz-Manager den gleichen Tasksequenzschritt erneut aus.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a> SMSTSRunCommandLineAsUser

*Ab Version 2002* <!-- 5573175 -->  
*Gilt für den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).*

Verwenden Sie Tasksequenzvariablen, um den Benutzerkontext für den Schritt **Befehlszeile ausführen** zu konfigurieren. Sie müssen den Schritt **Befehlszeile ausführen** nicht mit einem Platzhalterkonto konfigurieren, um die Variablen [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) und [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) zu verwenden.

Konfigurieren Sie `SMSTSRunCommandLineAsUser` mit einem der folgenden Werte:

- `true`: Alle weiteren Schritte von **Befehlszeile ausführen** werden im Kontext des in `SMSTSRunCommandLineUserName` angegebenen Benutzers ausgeführt.

- `false`: Alle weiteren Schritte von **Befehlszeile ausführen** werden im für diesen Schritt konfigurierten Kontext ausgeführt.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Gilt für den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).*

(Eingabe)

Hiermit wird das Konto angegeben, mit dem die Befehlszeile ausgeführt wird. Der Wert ist eine Zeichenfolge in der Form Benutzername oder Domäne\Benutzername. Geben Sie das Kontokennwort mit der Variablen [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) an.

> [!NOTE]
> Ab Version 2002 müssen Sie die Variable [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) mit dieser Variable verwenden, um den Benutzerkontext für diesen Schritt zu konfigurieren.
>
> Bei Version 1910 und früher konfigurieren Sie den Schritt **Befehlszeile ausführen** mit der Einstellung **Diesen Schritt mit folgendem Konto ausführen**. Wenn Sie diese Option aktivieren und den Benutzernamen und das Kennwort mit einer Variablen festlegen, geben Sie einen beliebigen Wert für das Konto an.

Weitere Informationen zum ausführenden Tasksequenzkonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword

*Gilt für den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).*

(Eingabe)

Gibt das Kennwort für das mit der Variablen [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) angegebene Konto an.

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a> SMSTSRunPowerShellAsUser

*Ab Version 2002* <!-- 5573175 -->  
*Gilt für den Schritt [PowerShell-Skript ausführen](task-sequence-steps.md#BKMK_RunPowerShellScript).*

Verwenden Sie Tasksequenzvariablen, um den Benutzerkontext für den Schritt **PowerShell-Skript ausführen** zu konfigurieren. Sie müssen den Schritt **PowerShell-Skript ausführen** nicht mit einem Platzhalterkonto konfigurieren, um die Variablen [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) und [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) zu verwenden.

Konfigurieren Sie `SMSTSRunPowerShellAsUser` mit einem der folgenden Werte:

- `true`: Alle weiteren Schritte von **PowerShell-Skript ausführen** werden im Kontext des in `SMSTSRunPowerShellUserName` angegebenen Benutzers ausgeführt.

- `false`: Alle weiteren Schritte von **PowerShell-Skript ausführen** werden im für diesen Schritt konfigurierten Kontext ausgeführt.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a> SMSTSRunPowerShellUserName

*Gilt für den Schritt [PowerShell-Skript ausführen](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(Eingabe)

Hiermit wird das Konto angegeben, mit dem das PowerShell-Skript ausgeführt wird. Der Wert ist eine Zeichenfolge in der Form Benutzername oder Domäne\Benutzername. Geben Sie das Kontokennwort mit der Variable [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) an.

> [!NOTE]
> Um diese Variablen zu verwenden, konfigurieren Sie den Schritt **PowerShell-Skript ausführen** mit der Einstellung **Diesen Schritt unter folgendem Konto ausführen**. Wenn Sie diese Option aktivieren und den Benutzernamen und das Kennwort mit einer Variablen festlegen, geben Sie einen beliebigen Wert für das Konto an.

Weitere Informationen zum ausführenden Tasksequenzkonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a> SMSTSRunPowerShellUserPassword

*Gilt für den Schritt [PowerShell-Skript ausführen](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(Eingabe)

Gibt das Kennwort für das von der Variablen [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) angegebene Konto an.

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Gilt für den Schritt [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(Eingabe)

Steuern Sie das Timeout für die Überprüfung auf Softwareupdates während dieses Schritts. Erhöhen Sie beispielsweise den Wert, wenn Sie zahlreiche Updates bei der Überprüfung erwarten. Der Standardwert beträgt `3600` Sekunden (60 Minuten). Der Variablenwert ist in Sekunden festgelegt.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Gibt die primären Benutzer des Zielcomputers in folgendem Format an: `<DomainName>\<UserName>`. Trennen Sie mehrere Benutzer durch ein Komma (`,`). Weitere Informationen finden Sie unter [Zuordnen von Benutzern zu einem Zielcomputer](../get-started/associate-users-with-a-destination-computer.md).

#### <a name="example"></a>Beispiel

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Gilt für den Schritt [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(Eingabe)

Diese optionale Tasksequenzvariable steuert das Clientverhalten, wenn die Installation eines Softwareupdates zwei Neustarts erfordert. Legen Sie diese Variable vor dem Ausführen dieses Schritts fest. So verhindern Sie, dass ein zweiter Neustart während der Installation des Softwareupdates einen Fehler bei der Tasksequenz verursacht.

Legen Sie den Wert „SMSTSWaitForSecondReboot“ in Sekunden fest, um anzugeben, für wie lange die Tasksequenz in diesem Schritt nach dem Neustart des Computers angehalten wird. Planen Sie genügend Zeit für einen zweiten Neustart ein.

Wenn Sie beispielsweise „SMSTSWaitForSecondReboot“ auf `600` festlegen, pausiert die Tasksequenz 10 Minuten nach einem Neustart, bevor weitere Schritte ausgeführt werden. Diese Variable ist hilfreich, wenn in einem einzigen Tasksequenzschritt „Softwareupdates installieren“ Hunderte von Softwareupdates installiert werden.

> [!Note]
> Diese Variable gilt nur für Tasksequenzen, mit denen ein Betriebssystem bereitgestellt wird. Bei benutzerdefinierten Tasksequenzen kann sie nicht verwendet werden. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a> TSDebugMode

<!--3612274-->
Ab Version 1906 können Sie diese Variable für eine Sammlung oder ein Computerobjekt, in der bzw. dem die Tasksequenz bereitgestellt wird, auf `TRUE` festlegen. Jedes Geräte, für das diese Variable festgelegt ist, versetzt für das Gerät bereitgestellte Tasksequenzen in den Debugmodus.

Weitere Informationen finden Sie unter [Debuggen einer Tasksequenz](../deploy-use/debug-task-sequence.md).

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a> TSDebugOnError

<!-- 5012536 -->
Ab Version 1910 können Sie diese Variable auf `TRUE` festlegen, um automatisch den [Tasksequenz-Debugger](../deploy-use/debug-task-sequence.md) zu starten, wenn die Tasksequenz einen Fehler zurückgibt.

Legen Sie diese Variable über den folgenden Schritt fest:

- Schritt [Tasksequenzvariable festlegen](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- Eine Sammlungsvariable. Weitere Informationen finden Sie unter [Festlegen von Variablen](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Steuern Sie mit dieser Variablen, wann die Tasksequenz Endbenutzern ihren Status anzeigt. Um den Status zu verschiedenen Zeitpunkten auszublenden oder anzuzeigen, legen Sie die Variable mehrmals innerhalb einer Tasksequenz fest.  

- `true`: Ausblenden des Tasksequenzstatus  

- `false`: Anzeigen des Tasksequenzstatus  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Gilt für den Schritt [Anwendung installieren](task-sequence-steps.md#BKMK_InstallApplication).*

(Eingabe)

Geben Sie an, ob die Tasksequenz-Engine eine erkannte Warnung als Fehler während dieses Schritts betrachten soll. Die Tasksequenz legt die Variable [_TSAppInstallStatus](#TSAppInstallStatus) auf `Warning` fest, wenn mindestens eine Anwendung oder eine erforderliche Abhängigkeit nicht installiert wurde, weil sie der Anforderung nicht entspricht. Wenn Sie diese Variable auf `True` festlegen, und die Tasksequenz die Variable **_TSAppInstallStatus** auf `Warning` setzt, ist das Ergebnis eine Fehlermeldung. Der Wert `False` entspricht dem Standardverhalten.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a> TSProgressInfoLevel

*Ab Version 2002*<!--5932692-->  

Legen Sie diese Variable fest, um den Typ der Informationen zu steuern, der vom Fortschrittsfenster der Tasksequenz angezeigt werden soll. Verwenden Sie die folgenden Werte für diese Variable:

- `1`: Schließen Sie den aktuellen Schritt und die Gesamtschritte in den Fortschrittstext ein. Beispiel: **2 von 10**
- `2`: Schließen Sie den aktuellen Schritt, die Gesamtschritte und den Prozentsatz mit ein, der den Fortschritt anzeigt. Beispiel: **2 von 10 (Fortschritt 20 %)**
- `3`: Schließen Sie den Prozentsatz ein, der den Fortschritt anzeigt. Beispiel: **(Fortschritt 20 %)**

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a> TSUEFIDrive

Findet in den Eigenschaften einer FAT32-Partition im Feld **Variable** Verwendung. Wenn die Tasksequenz diese Variable erkennt, wird der Datenträger auf den Wechsel zu UEFI vorbereitet, bevor der Computer neu gestartet wird. Weitere Informationen finden Sie unter [Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a> WorkingDirectory

*Gilt für den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine).*

(Eingabe)

Gibt das Startverzeichnis für eine Befehlszeilenaktion an. Der angegebene Verzeichnisname darf 255 Zeichen nicht überschreiten.

#### <a name="examples"></a>Beispiele

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Veraltete Variablen

Die folgenden Variablen sind veraltet:

- **OSDAllowUnsignedDriver:** wird bei der Bereitstellung von Windows Vista und neueren Betriebssystemen nicht verwendet
- **OSDBuildStorageDriverList:** gilt nur für Windows XP und Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode:** ist nur beim Bereitstellen von Windows XP oder Windows Server 2003 erforderlich
- **OSDInstallEditionIndex:** ist ab Windows Vista nicht erforderlich
- **OSDPreserveDriveLetter:** Weitere Informationen hierzu finden Sie unter [OSDPreserveDriveLetter](#osdpreservedriveletter).

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Diese Tasksequenzvariable ist veraltet.
>
> Beim Bereitstellen eines Betriebssystems bestimmt Windows Setup standardmäßig den am besten geeigneten Laufwerkbuchstaben (i.d.R. „C“).

*Früheres Verhalten*: Die Variable „OSDPreverveDriveLetter“ legte beim Anwenden eines Images fest, ob die Tasksequenz den in der Imagedatei (WIM) erfassten Laufwerkbuchstaben verwendet. Legen Sie den Wert dieser Variablen auf `false` fest, um den Speicherort zu verwenden, den Sie im Tasksequenzschritt **Betriebssystem anwenden** für die Einstellung **Ziel** angeben. Weitere Informationen finden Sie unter [Anwenden von Betriebssystemimages](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Weitere Informationen:

- [Tasksequenzschritte](task-sequence-steps.md)
- [Verwenden von Tasksequenzvariablen](using-task-sequence-variables.md)
- [Planungsüberlegungen für das Automatisieren von Tasks](../plan-design/planning-considerations-for-automating-tasks.md)