---
title: Softwareupdates installieren
titleSuffix: Configuration Manager
description: Empfehlungen zur Verwendung des Tasksequenzschritts „Softwareupdates installieren“ in Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 855351fc7fe28b40f23e1e01767fd62a782bc1e0
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606993"
---
# <a name="install-software-updates"></a>Softwareupdates installieren

*Gilt für: Configuration Manager (Current Branch)*

Der Schritt **Softwareupdates installieren** wird häufig in Configuration Manager-Tasksequenzen verwendet. Beim Installieren oder Aktualisieren des Betriebssystems werden die Komponenten für Softwareupdates ausgelöst, um nach Updates zu suchen und diese bereitzustellen. Dieser Schritt kann zu Herausforderungen für einige Kunden führen, z.B. zu langen Timeoutverzögerungen oder fehlenden Updates. Anhand der Informationen in diesem Artikel können Sie häufige Probleme bei diesem Schritt abmildern und bei Fehlern eine bessere Problembehandlung durchführen.

Weitere Informationen zu diesem Schritt finden Sie unter [Softwareupdates installieren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).



## <a name="recommendations"></a>Empfehlungen

Berücksichtigen Sie für einen erfolgreichen Prozess diese Empfehlungen:

- [Durchführen einer Offlinewartung](#use-offline-servicing)
- [Einzelner Index](#single-index)
- [Verringern der Imagegröße](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Durchführen einer Offlinewartung

Verwenden Sie Configuration Manager, um regelmäßig die anwendbaren Softwareupdates für Ihre Imagedateien zu installieren. Auf diese Weise verringert sich die Anzahl von Updates, die Sie während der Tasksequenz installieren müssen.

Weitere Informationen finden Sie unter [Anwenden von Softwareupdates auf ein Image](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Einzelner Index

Viele Imagedateien umfassen mehrere Indizes, z.B. für verschiedene Editionen von Windows. Beschränken Sie die Imagedatei auf einen einzelnen Index, den Sie benötigen. Auf diese Weise verringert sich die Zeit, die zum Anwenden von Softwareupdates auf das Image benötigt wird. Darüber hinaus wird die nächste Empfehlung zum Verringern der Imagegröße unterstützt.

Ab Version 1902 wird dieser Prozess automatisiert, wenn Sie ein Betriebssystemimage zum Standort hinzugefügt. Weitere Informationen finden Sie unter [Hinzufügen eines Betriebssystemimage](../get-started/manage-operating-system-images.md#BKMK_AddOSImages).<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a> Verringern der Imagegröße

Optimieren Sie beim Anwenden von Softwareupdates auf ein Image die Ausgabe, indem Sie abgelöste Updates entfernen. Verwenden Sie das DISM-Befehlszeilentool. Beispiel:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

Ab Version 1902 gibt es eine neue Option zum Automatisieren dieses Prozesses. Weitere Informationen finden Sie unter [Optimized image servicing (Optimierte Imagewartung)](../get-started/manage-operating-system-images.md#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Entscheidungen in Bezug auf den Imageentwurf

Beim Imageentwurf können sich verschiedene Optionen auf die Installation von Softwareupdates auswirken:

- [Regelmäßiges erneutes Erfassen des Images](#bkmk_goldimage)  
- [Durchführen einer Offlinewartung](#bkmk_offline)  
- [Ausschließliche Verwendung des Standardimages](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a> Regelmäßiges erneutes Erfassen des Images

Sie verfügen über einen automatisierten Prozess, um regelmäßig ein benutzerdefiniertes Betriebssystemimage zu erfassen. Über diese Tasksequenz zur Erfassung werden die neuesten Softwareupdates installiert. Es kann sich hierbei um kumulative, nicht kumulative und andere kritische Updates wie z.B. Wartungsstapelupdates handeln. Über die Tasksequenz zur Bereitstellung werden alle zusätzlichen Updates seit der Erfassung installiert.

Weitere Informationen zu diesem Prozess finden Sie unter [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

#### <a name="advantages"></a>Vorteile

- Es müssen zur Bereitstellungszeit weniger Updates pro Client angewendet werden, hierdurch wird bei der Bereitstellung Zeit und Bandbreite eingespart.
- Weniger Updates erzeugen weniger Neustarts.
- Angepasstes Image für die Organisation
- Weniger Variablen zur Bereitstellungszeit

#### <a name="disadvantages"></a>Nachteile

- Es wird Zeit zum Erstellen und Erfassen des Images benötigt, auch wenn der Prozess weitestgehend automatisiert erfolgt.
- Es wird mehr Zeit zum Verteilen des Images auf den Verteilungspunkten benötigt, dies kann als Ausfall für aktive Bereitstellungen betrachtet werden.
- Es wird unter Umständen mehr Zeit zum Testen über die Präproduktionsumgebung benötigt als im Patchzyklus für das Betriebssystem, wodurch das aktualisierte Image möglicherweise irrelevant wird.


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a> Durchführen einer Offlinewartung

Planen Sie Configuration Manager, um Softwareupdates auf Ihre Images anzuwenden.

Weitere Informationen finden Sie unter [Anwenden von Softwareupdates auf ein Image](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Vorteile

- Es müssen zur Bereitstellungszeit weniger Updates pro Client angewendet werden, hierdurch wird bei der Bereitstellung Zeit und Bandbreite eingespart.
- Weniger Updates erzeugen weniger Neustarts.
- Sie können den Wartungsprozess am Standort planen.

#### <a name="disadvantages"></a>Nachteile

- Updates müssen manuell ausgewählt werden.
- Es wird mehr Zeit zum Verteilen des Images auf den Verteilungspunkten benötigt.
- Es werden nur CBS-basierte Updates unterstützt. Microsoft 365 Apps-Updates können nicht angewendet werden.

> [!Tip]  
> Sie können die Auswahl von Softwareupdates mithilfe von PowerShell automatisieren. Verwenden Sie das Cmdlet [Get-CMSoftwareUpdate](/powershell/module/configurationmanager/get-cmsoftwareupdate), um eine Liste der Updates abzurufen. Verwenden Sie anschließend das Cmdlet [New-CMOperatingSystemImageUpdateSchedule](/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule), um den Zeitplan für die Offlinewartung zu erstellen. Das folgende Beispiel zeigt eine Methode zum Automatisieren dieser Aktion:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a> Ausschließliche Verwendung des Standardimages

Verwenden Sie die standardmäßige Windows-Imagedatei „install.wim“ in Ihren Tasksequenzen für die Bereitstellung.

#### <a name="advantages"></a>Vorteile

- Eine als funktionierend bekannte Quelle, die das Risiko einer Imagebeschädigung als mögliche Problemursache verringert
- Ausschluss von Imageänderungen als mögliche Problemursache

#### <a name="disadvantages"></a>Nachteile

- Potenziell hohe Anzahl von Updates während der Bereitstellung
- Längere Bereitstellungszeit für jedes Gerät
- Möglicherweise fehlen benötigte Anpassungen, sodass zusätzliche Tasksequenzschritte für eine Anpassung erforderlich sind



## <a name="flowchart"></a>Flussdiagramm

Dieses Flussdiagramm zeigt den Prozess zum Einschließen des Schritts „Softwareupdates installieren“ in eine Tasksequenz.

[Diagramm in voller Größe anzeigen](media/ts-step-install-software-updates.svg)

![Flussdiagramm zum Tasksequenzschritt „Softwareupdates installieren“](media/ts-step-install-software-updates.svg)  

1. **Prozess wird auf dem Client gestartet**: Eine auf einem Client ausgeführte Tasksequenz schließt den Schritt „Softwareupdates installieren“ ein.
2. **Richtlinien kompilieren und auswerten**: Der Client kompiliert alle Richtlinien zu Softwareupdates im WMI RequestedConfigs-Namespace. (CIAgent.log)
3. *Wird diese Instanz zum ersten Mal aufgerufen?*  
    1. **Ja**: Wechsel zu **Vollständige Überprüfung**.  
    2. **Nein**: *Ist der Schritt mit der Option [Bewerten von Softwareupdates aus zwischengespeicherten Überprüfungsergebnissen](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results) konfiguriert?*
        1. **Ja**: Wechsel zu **Überprüfung anhand von zwischengespeicherten Ergebnissen**.
        2. **Nein**: Wechsel zu **Vollständige Überprüfung**.
4. Überprüfungsprozess: Es wird entweder eine vollständige Überprüfung oder eine Überprüfung anhand der zwischengespeicherten Ergebnisse durchgeführt, parallel wird ein Überwachungsprozess ausgeführt.
    1. **Vollständige Überprüfung**: Die Tasksequenzengine ruft den Softwareupdate-Agent über die API zur Updateüberprüfung auf, um eine *vollständige* Überprüfung durchzuführen. (WUAHandler.log, ScanAgent.log)  
        1. **SUM-Agent-Überprüfung – vollständig**: Normaler Überprüfungsprozess über den Windows Update-Agent (WUA), der mit dem Softwareupdatepunkt kommuniziert, der WSUS ausführt. Anwendbare Updates werden dem lokalen Updatespeicher hinzugefügt. (WindowsUpdate.log, UpdateStore.log)
    2. **Überprüfung anhand von zwischengespeicherten Ergebnissen**: Die Tasksequenzengine ruft den Softwareupdate-Agent über die API zur Updateüberprüfung auf, um eine Überprüfung anhand von zwischengespeicherten Metadaten durchzuführen. (WUAHandler.log, ScanAgent.log)
        1. **SUM-Agent-Überprüfung – zwischengespeichert**: Der Windows Update-Agent (WUA) führt anhand der bereits im lokalen Updatespeicher zwischengespeicherten Updates eine Überprüfung durch. (WindowsUpdate.log, UpdateStore.log)
    3. **Überprüfungstimer starten**: Die Tasksequenzengine startet einen Timer und wartet. (Dieser Prozess erfolgt parallel zur vollständigen Überprüfung oder zur Überprüfung anhand von zwischengespeicherten Ergebnissen.)
        1. **Überwachung**: Die Taskseqenzengine überwacht den Status des SUM-Agents.
        2. *Welche Antwort wird vom SUM-Agent empfangen?*
            - **In Bearbeitung**: Hat der Timer den Wert in der Tasksequenzvariablen [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout) erreicht? (Standardwert: 1 Stunde)
                - **Ja**: Fehler bei Schritt.
                - **Nein**: Wechsel zu **Überwachung**.
            - **Fehlgeschlagen:** Fehler bei Schritt.
            - **Abgeschlossen**: Wechsel zu **Updateliste aufzählen**.
5. **Updateliste aufzählen**: Der SUM-Agent zählt die Liste der bei der Überprüfung zurückgegebenen Updates auf und bestimmt, welche Updates verfügbar oder erforderlich sind.
6. *Sind Updates in der Liste der Überprüfungsergebnisse enthalten?*
    - **Ja**: Wechsel zu **Updates installieren**.
    - **Nein**: Keine Updates zur Installation vorhanden, der Schritt wird erfolgreich abgeschlossen.
7. Bereitstellungsprozess: Der Prozess der Updateinstallation erfolgt parallel zum Prozess für die Bereitstellungsüberwachung.
    1. **Updates installieren**: Die Tasksequenzengine ruft den SUM-Agent über die API zur Updatebereitstellung auf, um alle verfügbaren oder nur die erforderlichen Updates zu installieren. Dieses Verhalten basiert auf der Konfiguration des Schritts – je nachdem, ob sie **Erforderlich für Installation – Nur erforderliche Softwareupdates** oder **Verfügbar für Installation – Alle Softwareupdates** ausgewählt haben. Sie können dieses Verhalten auch über die Variable [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget) angeben.
        1. **SUM-Agent-Installation**: Normaler Installationsprozess anhand einer vorhandenen Liste zwischengespeicherter Updates, mit Standardinhaltsdownload. Installation von Updates über Windows Update-Agent (WUA). (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Bereitstellungstimer starten und Fortschritt anzeigen**: Die Tasksequenzengine startet einen Installationstimer, zeigt den Fortschritt von Unteraufgaben in Intervallen von 10% in der TS-Benutzeroberfläche an und wartet.
        1. **Überwachung**: Die Taskseqenzengine ruft den Status des SUM-Agents ab.
        2. *Welche Antwort wird vom SUM-Agent empfangen?*
            - **In Bearbeitung**: *Ist der Installationsprozess seit 8 Stunden aktiv?*
                - **Ja**: Fehler bei Schritt.
                - **Nein**: Wechsel zu **Überwachung**.
            - **Fehlgeschlagen:** Fehler bei Schritt.
            - **Abgeschlossen**: Wechsel zu *Ist der Schritt mit der Option **Bewerten von Softwareupdates aus zwischengespeicherten Überprüfungsergebnissen** konfiguriert?* .


### <a name="timeouts"></a>Timeouts

Das Diagramm umfasst zwei Timeoutvariablen, die für diesen Schritt gelten. Es gibt weitere Standardtimer von anderen Komponenten, die diesen Prozess beeinflussen können.

- Timeout für Updateüberprüfung: 1 Stunde (smsts.log)  
- Timeout für Standortanforderung: 1 Stunde (LocationServices.log, CAS.log)  
- Timeout für Inhaltsdownload: 1 Stunde (DTS.log)  
- Timeout für inaktiven Verteilungspunkt: 1 Stunde (LocationServices.log, CAS.log)  
- Gesamttimeout für inaktive Installation: 8 Stunden (smsts.log)  



## <a name="troubleshooting"></a>Problembehandlung

Verwenden Sie die folgenden Ressourcen und zusätzlichen Informationen als Hilfe bei der Problembehandlung für diesen Schritt:

- Stellen Sie sicher, dass Ihre Softwareupdatebereitstellungen dieselbe Sammlung als Ziel verwenden wie die Tasksequenzbereitstellung.  

- Stellen Sie sicher, dass Softwareupdatepunkte in Begrenzungsgruppen eingeschlossen werden. Weitere Informationen finden Sie in diesem [Microsoft-Support-Artikel](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Informationen zur Problembehandlung für den Prozess der Softwareupdateverwaltung finden Sie unter [Problembehandlung bei der Softwareupdateverwaltung](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Verringern Sie zur Verbesserung der Gesamtleistung die Größe des Softwareupdatekatalogs. Beispiel:  

    - Entfernen Sie nicht benötigte Klassifizierungen, Produkte und Sprachen. Weitere Informationen finden Sie unter [Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte](../../sum/get-started/configure-classifications-and-products.md).  

    - Führen Sie eine Neuindizierung für die Standortdatenbank durch, und erstellen Sie die Statistik neu. Weitere Informationen finden Sie im [Configuration Manager Perf and Scale Guidance Whitepaper](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e) (Whitepaper zu Configuration Manager-Leistung und Skalierung).  

    - Lehnen Sie nicht benötigte Updates ab. Beispiel:
        - Abgelöst (diese Aktion steht in Configuration Manager ab Version 1810 zur Verfügung, weitere Informationen finden Sie hier: [WSUS-Cleanupverhalten ab Version 1810](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810))
        - Itanium
        - Beta
        - Version Next
        - ARM
        - Nicht bereitgestellte Windows-Versionen