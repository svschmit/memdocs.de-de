---
title: Technical Preview 1802 | Microsoft-Dokumentation
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1802 zur Verfügung stehen.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 50e05d07ec3e2612c170157c45f5e64abe3766de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701328"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Funktionen in der Technical Preview 1802 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1802 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. 

Lesen Sie sich die Informationen unter [Technical Preview für Configuration Manager](technical-preview.md) durch, bevor Sie diese Technical Preview-Version installieren. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Bekannte Probleme in dieser Technical Preview
- **Beim Update auf die Vorschauversion tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie über einen [primären Standortserver im Modus „Passiv“](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) verfügen, müssen Sie den Standortserver im Modus „Passiv“ deinstallieren, bevor Sie ein Update auf diese neue Preview-Version durchführen. Sie können den Standortserver im passiven Modus erneut installieren, wenn das Update an Ihrem Standort abgeschlossen wurde.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Configuration Manager-Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im Modus „Passiv“ aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen** aus.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.
  <!--sms 489412-->


</br>

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Übertragen der Endpoint Protection-Workload auf Intune mithilfe der Co-Verwaltung    
<!-- 1357365 -->
In diesem Release können Sie jetzt die Endpoint Protection-Workload von Configuration Manager auf Intune übertragen, nachdem Sie die Co-Verwaltung aktiviert haben. Um die Endpoint Protection-Workload zu übertragen, öffnen Sie die Seite mit den Eigenschaften der Co-Verwaltung, und schieben Sie den Schieberegler von „Configuration Manager“ auf **Pilot** oder **Alle**. Weitere Informationen finden Sie unter [Co-Verwaltung für Windows 10-Geräte](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Konfigurieren der Windows-Übermittlungsoptimierung für die Verwendung von Configuration Manager-Begrenzungsgruppen
<!-- 1324696 -->
Sie verwenden Configuration Manager-Begrenzungsgruppen, um die Inhaltsverteilung über Ihr gesamtes Unternehmensnetzwerk und Remotebüros hinweg zu definieren und zu regulieren. [Windows-Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization) ist eine cloudbasierte Peer-zu-Peer-Technologie zum gemeinsamen Nutzen von Inhalten auf Windows 10-Geräten. Ab diesem Release können Sie die Übermittlungsoptimierung so konfigurieren, dass bei der Freigabe von Inhalten für Peers Ihre Begrenzungsgruppen verwendet werden. Eine neue Clienteinstellung wendet die Begrenzungsgruppen-ID als Gruppen-ID für die Übermittlungsoptimierung auf dem Client an. Wenn der Client mit dem Übermittlungsoptimierungs-Clouddienst kommuniziert, wird diese ID zum Ermitteln von Peers verwendet, auf denen sich der gewünschte Inhalt befindet. 

### <a name="prerequisites"></a>Voraussetzungen
- Die Übermittlungsoptimierung ist nur auf Windows 10-Clients verfügbar.

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Erstellen Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** im Knoten **Clienteinstellungen** eine neue benutzerdefinierte Richtlinie für Clientgeräteeinstellungen.
2. Wählen Sie die neue Gruppe **Übermittlungsoptimierung** aus.
3. Aktivieren Sie die Einstellung **Verwenden Sie Configuration Manager-Begrenzungsgruppen für die Gruppen-ID der Übermittlungsoptimierung**.

Weitere Informationen finden Sie in den [Optionen für die Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization) unter dem Übermittlungsmodus **Gruppe**.



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Tasksequenz für direktes Windows 10-Upgrade über das Cloudverwaltungsgateway
<!-- 1357149 -->

Die [Tasksequenz für direktes Windows 10-Upgrade](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) unterstützt jetzt die Bereitstellung auf internetbasierten Clients, die über das [Cloudverwaltungsgateway](../clients/manage/cmg/plan-cloud-management-gateway.md) verwaltet werden. Mit dieser Funktion können Remotebenutzer einfacher ein Upgrade auf Windows 10 durchführen, ohne eine Verbindung mit dem Unternehmensnetzwerk herstellen zu müssen. 

Stellen Sie sicher, dass alle Inhalte, auf die von der Tasksequenz für das direkte Upgrade verwiesen wird, auf einem [Cloudverteilungspunkt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) bereitgestellt wurden. Andernfalls können die Geräte die Tasksequenz nicht ausführen.

Wenn Sie eine Upgradetasksequenz bereitstellen, verwenden Sie folgende Einstellungen:
- **Ausführung der Tasksequenz für internetbasierten Client zulassen** auf der Registerkarte „Benutzerfreundlichkeit“ der Bereitstellung.
- **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** auf der Registerkarte „Verteilungspunkte“ der Bereitstellung. Andere Optionen wie z.B. **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** funktionieren in diesem Szenario nicht. Die Tasksequenz-Engine kann derzeit keine Inhalte aus einem Cloudverteilungspunkt abrufen. Der Configuration Manager-Client muss die Inhalte aus dem Cloudverteilungspunkt herunterladen, bevor die Tasksequenz gestartet wird.
- (*Optional*) **Inhalt für diese Tasksequenz vorab herunterladen** auf der Registerkarte „Allgemein“ der Bereitstellung. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Verbesserungen an der Tasksequenz für direktes Windows 10-Upgrade
<!-- 1357425 -->
Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält jetzt zusätzliche Gruppen mit empfohlenen Aktionen, die vor und nach dem Upgradevorgang hinzugefügt werden können. Diese Aktionen werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Neue Gruppen unter **Vorbereitung auf das Upgrade**
- **Stromversorgung überprüfen:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um zu überprüfen, ob der Computer sich im Akku- oder Netzbetrieb befindet. Für diese Aktion ist ein benutzerdefiniertes Skript oder ein Hilfsprogramm erforderlich, um diese Prüfung auszuführen.
- **Netzwerk-/Drahtlosverbindung überprüfen:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um sicherzustellen, dass der Computer keine Drahtlos-, sondern eine Netzwerkverbindung verwendet. Für diese Aktion ist ein benutzerdefiniertes Skript oder ein Hilfsprogramm erforderlich, um diese Prüfung auszuführen.
- **Inkompatible Anwendungen entfernen:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um alle Anwendungen zu entfernen, die nicht mit dieser Version von Windows 10 kompatibel sind. Die Methoden zum Deinstallieren einer Anwendung variieren. Wenn die Anwendung den Windows Installer verwendet, kopieren Sie die Befehlszeile **Programm deinstallieren** von der Registerkarte **Programme** in den Eigenschaften des Windows Installer-Bereitstellungstyps der Anwendung. Fügen Sie dann in diese Gruppe mit der Befehlszeile zum Deinstallieren des Programms einen Schritt **Befehlszeile ausführen** ein. Beispiel: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Inkompatible Treiber entfernen:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um alle Treiber zu entfernen, die nicht mit dieser Version von Windows 10 kompatibel sind.
- **Sicherheitsprogramme von Drittanbietern entfernen/anhalten:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Sicherheitsprogramme von Drittanbietern – z.B. Antivirenprogramme – zu entfernen.
   - Wenn Sie ein Drittanbieterprogramm zur Datenträgerverschlüsselung verwenden, geben Sie den Verschlüsselungstreiber in Windows Setup mit der [Befehlszeilenoption](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers** an. Fügen Sie der Tasksequenz in dieser Gruppe einen Schritt [Tasksequenzvariable festlegen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) hinzu. Legen Sie die Tasksequenzvariable auf **OSDSetupAdditionalUpgradeOptions** fest. Legen Sie den Wert auf **/ReflectDriver** mit dem Pfad zum Treiber fest. Die [Tasksequenz-Aktionsvariable](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) fügt die von der Tasksequenz verwendete Windows Setup-Befehlszeile an. Wenden Sie sich an den Anbieter Ihrer Software, um weitere Informationen zu diesem Vorgang zu erhalten.

### <a name="new-groups-under-post-processing"></a>Neue Gruppen unter **Nachverarbeitung**
- **Setupbasierte Treiber anwenden:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um setupbasierte Treiber (EXE) aus Paketen zu installieren.
- **Sicherheitsprogramme von Drittanbietern installieren/aktivieren:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Sicherheitsprogramme von Drittanbietern – z.B. Antivirenprogramme – zu installieren oder zu aktivieren. 
- **Windows-Standard-Apps und Zuordnungen festlegen:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Windows-Standard-Apps und Dateizuordnungen festzulegen. Bereiten Sie zuerst einen Referenzcomputer mit den gewünschten App-Zuordnungen vor. Führen Sie dann die folgende Befehlszeile für den Export aus: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Fügen Sie die XML-Datei zu einem Paket hinzu. Fügen Sie dann in dieser Gruppe einen Schritt [Befehlszeile ausführen](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) hinzu. Geben Sie das Paket, das die XML-Datei enthält, sowie die folgende Befehlszeile an: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Weitere Informationen finden Sie unter [Exportieren oder Importieren von standardmäßigen Anwendungszuordnungen](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Anpassungen und Personalisierungen anwenden:** Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Startmenüanpassungen, z.B. das Organisieren von Programmgruppen, anzuwenden. Weitere Informationen finden Sie unter [Anpassen des Startbildschirms](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Weitere Empfehlungen
- Lesen Sie die Windows-Dokumentation zum [Beheben von Windows 10-Upgradefehlern](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Dieser Artikel enthält auch detaillierte Informationen zum Upgradeprozess.
- Aktivieren Sie im Standardschritt **Bereitschaft überprüfen** die Option **Mindestens erforderlicher freier Speicherplatz (MB)** . Legen Sie den Wert für das Upgrade eines 32-Bit-Betriebssystems auf mindestens **16384** (16 GB) fest. Für ein 64-Bit-System beträgt der Wert **20480** (20 GB). 
- Verwenden Sie die [integrierte Tasksequenzvariable](../../osd/understand/task-sequence-variables.md) **SMSTSDownloadRetryCount**, um erneut zu versuchen, die Richtlinie herunterzuladen. Derzeit ist die Variable standardmäßig auf „2“ festgelegt, der Client unternimmt also zwei Wiederholungsversuche. Wenn Ihre Clients keine kabelgebundene Verbindung zum Unternehmensnetzwerk verwenden, können weitere Wiederholungen dabei helfen, dass der Client die Richtlinie abrufen kann. Die Verwendung dieser Variable hat keine negativen Nebenwirkungen, außer dass ein verzögerter Fehler auftritt, wenn die Richtlinie nicht heruntergeladen werden kann.<!-- 501016 --> Erhöhen Sie auch die Variable **SMSTSDownloadRetryDelay** vom Standardwert „15 Sekunden“.
- Führen Sie eine Inline-Kompatibilitätsbewertung durch. 
   - Fügen Sie an einem frühen Punkt in der Gruppe **Für Aktualisierung vorbereiten** einen zweiten Schritt **Betriebssystem aktualisieren** hinzu. Nennen Sie den Schritt *Upgradebewertung*. Geben Sie das gleiche Upgradepaket an, und aktivieren Sie die Option **Kompatibilitätsprüfung für Windows Setup ausführen, ohne Upgrade zu starten**. Aktivieren Sie **Bei Fehler fortsetzen** auf der Registerkarte „Optionen“. 
   - Fügen Sie unmittelbar nach dem Schritt *Upgradebewertung* einen Schritt **Befehlszeile ausführen** hinzu. Geben Sie die folgende Befehlszeile an:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Fügen Sie auf der Registerkarte **Optionen** die folgende Bedingung hinzu: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Dieser Rückgabecode ist die dezimale Entsprechung von MOSETUP_E_COMPAT_SCANONLY (0xC1900210), einer erfolgreichen Kompatibilitätsüberprüfung ohne Fehler. Wenn der Schritt *Upgradebewertung* erfolgreich ausgeführt wurde und diesen Code zurückgibt, wird dieser Schritt übersprungen. Wenn der Bewertungsschritt einen anderen Rückgabecode zurückgibt, führt dieser Schritt in der Tasksequenz mit dem Rückgabecode aus der Windows Setup-Kompatibilitätsüberprüfung zu einem Fehler.
   - Weitere Informationen finden Sie unter [Betriebssystem aktualisieren](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Wenn Sie das Gerät während dieser Tasksequenz von BIOS zu UEFI konvertieren möchten, finden Sie weitere Informationen unter [Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Wenn Sie weitere Empfehlungen oder Vorschläge unterbreiten möchten, senden Sie **Feedback** von der Registerkarte **Startseite** des Menübands.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Verbesserungen an PXE-fähigen Verteilungspunkten
<!-- 1357580 -->
Um das Verhalten der [neuen PXE-Funktion](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) zu verdeutlichen, die in der Technical Preview-Version 1706 eingeführt wurde, haben wir die Option **IPv6 unterstützen** umbenannt. Aktivieren Sie auf der Registerkarte **PXE** der Eigenschaften des Verteilungspunkts die Option **PXE-Antwortdienst ohne Windows-Bereitstellungsdienst aktivieren**. 

Diese Option aktiviert einen PXE-Antwortdienst auf dem Verteilungspunkt, der keinen Windows-Bereitstellungsdienst (Windows Deployment Service, WDS) benötigt. Wenn Sie diese neue Option auf einem Verteilungspunkt aktivieren, auf dem PXE bereits aktiviert ist, hält Configuration Manager den WDS an. Wenn Sie diese neue Option deaktivieren, aber trotzdem die **PXE-Unterstützung für Clients aktivieren**, aktiviert der Verteilungspunkt den WDS wieder.

Da WDS nicht erforderlich ist, kann auf dem PXE-fähigen Verteilungspunkt ein Client- oder Serverbetriebssystem ausgeführt werden, einschließlich Windows Server Core. Dieser neue PXE-Antwortdienst unterstützt weiterhin IPv6 und erweitert zudem die Flexibilität von PXE-fähigen Verteilungspunkten in Remotebüros.

> [!NOTE]
> Dieser Dienst verwendet die gleiche grundlegende Technologie wie der [clientbasierte PXE-Antwortdienst](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) in der Technical Preview-Version 1712. Dieses Feature erfordert nicht den Mehraufwand der Verteilungspunktrolle.

### <a name="multicast"></a>Multicast
Damit auf der Registerkarte **Multicast** der Eigenschaften des Verteilungspunkts Multicastfunktionen aktiviert und konfiguriert werden können, muss der Verteilungspunkt WDS verwenden. 
- Wenn Sie die Optionen **PXE-Unterstützung für Clients aktivieren** und **Multicast aktivieren, um gleichzeitig Daten an mehrere Clients zu senden** verwenden, können Sie die Option **PXE-Antwortdienst ohne Windows-Bereitstellungsdienst aktivieren** nicht verwenden.
- Wenn Sie die Optionen **PXE-Unterstützung für Clients aktivieren** und **PXE-Antwortdienst ohne Windows-Bereitstellungsdienst aktivieren** verwenden, können Sie die Option **Multicast aktivieren, um gleichzeitig Daten an mehrere Clients zu senden** nicht verwenden.



## <a name="deployment-templates-for-task-sequences"></a>Bereitstellungsvorlagen für Tasksequenzen
<!-- 1357391 -->
Der Bereitstellungs-Assistent für Tasksequenzen kann jetzt eine Bereitstellungsvorlage erstellen. Die Bereitstellungsvorlage kann gespeichert und auf eine vorhandene oder neue Tasksequenz angewendet werden, um eine Bereitstellung zu erstellen. 

### <a name="try-it-out"></a>Probieren Sie es aus!  
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen. 

 **Erstellen einer Bereitstellungsvorlage für eine neue Tasksequenzbereitstellung** <br/> 
1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.
2. Klicken Sie mit der rechten Maustaste auf eine Tasksequenz, und wählen Sie **Bereitstellen** aus. 
3. Beachten Sie, dass sich auf der Registerkarte **Allgemein** jetzt die Option **Bereitstellungsvorlage auswählen** befindet. 
4. Führen Sie die Schritte im **Assistenten zum Bereitstellen von Software** aus, und wählen Sie die gewünschten Bereitstellungseinstellungen für die Tasksequenz aus. 
5. Klicken Sie auf der Registerkarte **Zusammenfassung** des **Assistent zum Bereitstellen von Software** auf **Als Vorlage speichern**.
6. Benennen Sie die Vorlage, und wählen Sie die Einstellungen aus, die in der Vorlage gespeichert werden sollen. 
7. Klicken Sie auf **Speichern**. Die Vorlage steht jetzt in der Option **Bereitstellungsvorlage auswählen** zur Auswahl bereit.



## <a name="product-lifecycle-dashboard"></a>Dashboard für den Produktlebenszyklus
<!--1319632-->
Das neue [Dashboard für den Produktlebenszyklus](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) zeigt den Status der Microsoft-Lebenszyklusrichtlinie für Microsoft-Produkte an, die auf mit Configuration Manager verwalteten Geräten installiert sind. Das Dashboard bietet Ihnen Informationen zu Microsoft-Produkten in Ihrer Umgebung, deren Supportfähigkeit und den Daten des Supportendes. Auf diesem Dashboard erfahren Sie, welche Art von Support für die jeweiligen Produkte verfügbar ist. 

Um auf das Dashboard für den Lebenszyklus zuzugreifen, wechseln Sie in der Configuration Manager-Konsole zu **Assets und Konformität** >**Asset Intelligence** >**Produktlebenszyklus**.



## <a name="improvements-to-reporting"></a>Verbesserungen bei der Berichterstellung
<!--1357653-->
Aufgrund [Ihres Feedbacks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) haben wir einen neuen Bericht hinzugefügt: **Windows 10-Wartungsdetails für eine bestimmte Sammlung**. Dieser Bericht die Ressourcen-ID, den NetBIOS-Namen, den Betriebssystemnamen, den Namen der Betriebssystemversion, den Build, den Betriebssystembranch und den Wartungsstatus für Windows 10-Geräte. Um auf den Bericht zuzugreifen, wechseln Sie zu **Überwachung** >**Berichterstellung** >**Berichte** >**Betriebssysteme** >**Windows 10-Wartungsdetails für eine bestimmte Sammlung**.



## <a name="improvements-to-software-center"></a>Verbesserungen für Software Center
<!--1357592-->
Aufgrund [Ihres Feedbacks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) können installierte Anwendungen jetzt im Softwarecenter ausgeblendet werden. Bereits installierte Anwendungen werden auf der Registerkarte „Anwendungen“ nicht mehr angezeigt, wenn diese Option aktiviert ist. 

### <a name="try-it-out"></a>Probieren Sie es aus!
Aktivieren Sie in den Softwarecenter-Clienteinstellungen die Einstellung **Installierte Anwendungen im Softwarecenter ausblenden**. Beachten Sie das Verhalten im Softwarecenter, wenn ein Endbenutzer eine Anwendung installiert.



## <a name="improvements-to-run-scripts"></a>Verbesserungen für die Funktion „Skripts ausführen“
<!--1236459-->
Das Feature [Skripts ausführen](../../apps/deploy-use/create-deploy-scripts.md) gibt die Skriptausgabe jetzt mit JSON-Formatierung zurück. Dieses Format gibt konsistent eine lesbare Skriptausgabe zurück. Für nicht ausgeführte Skripts wird möglicherweise keine Ausgabe zurückgegeben. 



## <a name="boundary-group-fallback-for-management-points"></a>Fallback für Begrenzungsgruppen für Verwaltungspunkte
<!-- 1324594 -->
Ab diesem Release können Sie Fallbackbeziehungen für Verwaltungspunkte zwischen [Begrenzungsgruppen](../servers/deploy/configure/boundary-groups.md) konfigurieren. Dieses Verhalten ermöglicht eine bessere Steuerung der von Clients verwendeten Verwaltungspunkte. Auf der Registerkarte **Beziehungen** der Eigenschaften einer Begrenzungsgruppe gibt es jetzt eine neue Spalte für den Verwaltungspunkt. Wenn Sie eine neue Fallback-Begrenzungsgruppe hinzufügen, ist die Fallbackzeit für den Verwaltungspunkt derzeit immer Null (0). Dieses Verhalten entspricht dem **Standardverhalten** der Standardbegrenzungsgruppe des Standorts.

Bisher tritt ein allgemeines Problem auf, wenn Sie über einen geschützten Verwaltungspunkt in einem sicheren Netzwerk verfügen. Clients im Hauptunternehmensnetzwerk empfangen eine Richtlinie, die diesen geschützten Verwaltungspunkt enthält, auch wenn sie über eine Firewall nicht mit diesem Punkt kommunizieren können. Um dieses Problem zu beheben, verwenden Sie die Option **Nie ein Fallback durchführen**, um sicherzustellen, dass Clients nur ein Fallback auf Verwaltungspunkte durchführen, mit denen sie kommunizieren können.

Beim Upgrade des Standorts auf diese Version fügt Configuration Manager alle Verwaltungspunkte ohne Internetzugriff der Standardbegrenzungsgruppe des Standorts hinzu. Dieses Upgradeverhalten stellt sicher, dass ältere Clientversionen weiterhin mit Verwaltungspunkten kommunizieren können. Damit Sie dieses Feature vollständig nutzen können, verschieben Sie Ihre Verwaltungspunkte in die gewünschten Begrenzungsgruppen.

Das Fallback bei Verwaltungspunkten in Begrenzungsgruppen ändert das Verhalten während der Clientinstallation (ccmsetup) nicht. Wenn der anfängliche Verwaltungspunkt nicht in der Befehlszeile mit dem Parameter „/MP“ angegeben wird, empfängt der neue Client die vollständige Liste aller verfügbaren Verwaltungspunkte. Für den anfänglichen Bootstrapprozess verwendet der Client den ersten Verwaltungspunkt, auf den er zugreifen kann. Sobald der Client beim Standort registriert ist, erhält er die gemäß diesem neuen Verhalten ordnungsgemäß sortierte Verwaltungspunktliste. 

### <a name="prerequisites"></a>Voraussetzungen
- Aktivieren Sie [bevorzugte Verwaltungspunkte](../servers/deploy/configure/boundary-groups.md#bkmk_preferred). Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Klicken Sie im Menüband auf **Hierarchieeinstellungen**. Wählen Sie auf der Registerkarte **Allgemein** die Option **Clients bevorzugen das Verwenden von in Begrenzungsgruppen angegebenen Verwaltungspunkten**. 

### <a name="known-issues"></a>Bekannte Probleme
- Bei Prozessen der Betriebssystembereitstellung haben Begrenzungsgruppen keine Bedeutung.

### <a name="troubleshooting"></a>Problembehandlung
Im **LocationServices.log** werden neue Einträge angezeigt. Das Attribut **Ort** identifiziert einen der folgenden Zustände:
- 0: Unbekannt
- 1: Der angegebene Verwaltungspunkt befindet sich nur in der standardmäßigen Standortbegrenzungsgruppe für das Fallback.
- 2: Der angegebene Verwaltungspunkt befindet sich in einer Remotebegrenzungsgruppe oder einer benachbarten Begrenzungsgruppe. Wenn sich der Verwaltungspunkt sowohl in einer benachbarten als auch der standardmäßigen Standortbegrenzungsgruppe befindet, lautet der Wert für den Ort „2“.
- 3: Der angegebene Verwaltungspunkt befindet sich in der lokalen oder aktuellen Begrenzungsgruppe. Wenn sich der Verwaltungspunkt sowohl in der aktuellen als auch entweder in einer benachbarten oder der standardmäßigen Standortbegrenzungsgruppe befindet, lautet der Wert für den Ort „3“. Wenn Sie die Einstellung für bevorzugte Verwaltungspunkte in den Hierarchieeinstellungen nicht aktivieren, lautet der Ort immer „3“, unabhängig davon, in welcher Begrenzungsgruppe sich der Verwaltungspunkt befindet.

Clients verwenden zuerst lokale Verwaltungspunkte (Ort 3), danach Remotepunkte (Ort 2), dann Fallbackpunkte (Ort 1). 

Wenn ein Client innerhalb von zehn Minuten fünf Fehler empfängt und mit keinem Verwaltungspunkt in der aktuellen Begrenzungsgruppe kommunizieren kann, versucht er, einen Verwaltungspunkt in einer benachbarten Begrenzungsgruppe oder der standardmäßigen Standortbegrenzungsgruppe zu kontaktieren. Wenn der Verwaltungspunkt in der aktuellen Begrenzungsgruppe zu einem späteren Zeitpunkt wieder online geschaltet wird, kehrt der Client beim nächsten Aktualisierungszyklus zum lokalen Verwaltungspunkt zurück. Der Aktualisierungszyklus beträgt 24 Stunden. Er beginnt ebenfalls von Neuem, wenn der Configuration Manager-Agent-Dienst neu gestartet wird.



## <a name="improved-support-for-cng-certificates"></a>Verbesserte Unterstützung für CNG-Zertifikate
<!-- 1357314 -->
Configuration Manager in Version 1710 (aktueller Branch) unterstützt [CNG-Zertifikate (Cryptography: Next Generation)](../plan-design/network/cng-certificates-overview.md). In Version 1710 ist die Unterstützung auf Clientzertifikate in verschiedenen Szenarien begrenzt. 

Ab diesem Technical Preview-Release können Sie CNG-für die folgenden HTTPS-fähigen Serverrollen verwenden:
- Verwaltungspunkt
- Verteilungspunkt
- Softwareupdatepunkt

Die Liste der [nicht unterstützten Szenarien](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) bleibt gleich.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Unterstützung für Cloudverwaltungsgateway für Azure Resource Manager
<!-- 1324735 -->
Beim Erstellen einer Instanz des [Cloudverwaltungsgateways](../clients/manage/cmg/plan-cloud-management-gateway.md) (Cloud Management Gateway, CMG) bietet der Assistent jetzt die Option, eine **Azure Resource Manager-Bereitstellung** zu erstellen. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) ist eine moderne Plattform zum Verwalten aller Lösungsressourcen als eine einzige Entität, die als [Ressourcengruppe](/azure/azure-resource-manager/resource-group-overview#resource-groups) bezeichnet wird. Beim Bereitstellen eines Cloudverwaltungsgateways mit Azure Resource Manager verwendet der Standort Azure Active Directory (Azure AD), um die erforderlichen Cloudressourcen zu authentifizieren und zu erstellen. Diese modernisierte Bereitstellung benötigt kein klassisches Azure-Verwaltungszertifikat.  

Der CMG-Assistent bietet weiterhin die Option einer **klassischen Dienstbereitstellung** mit einem Azure-Verwaltungszertifikat. Um die Bereitstellung und Verwaltung von Ressourcen zu vereinfachen, empfiehlt sich die Verwendung des Azure Resource Manager-Bereitstellungsmodells für alle neuen CMG-Instanzen. Stellen Sie nach Möglichkeit vorhandene CMG-Instanzen über Resource Manager erneut bereit.

Configuration Manager migriert keine vorhandenen klassischen CMG-Instanzen zum Azure Resource Manager-Bereitstellungsmodell. Erstellen Sie mithilfe von Azure Resource Manager-Bereitstellungen neue CMG-Instanzen, und entfernen Sie dann die klassischen CMG-Instanzen. 

> [!IMPORTANT]
> Diese Funktion aktiviert nicht die Unterstützung für Azure-Clouddienstanbieter (Cloud Service Providers, CSPs). Die CMG-Bereitstellung mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSPs nicht unterstützt wird. Weitere Informationen finden Sie unter [verfügbare Azure-Dienste in Azure-CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Voraussetzungen
- Integration in [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Die Azure AD-Benutzerermittlung ist nicht erforderlich.
- Die gleichen [Anforderungen für das Cloudverwaltungsgateway](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements), mit Ausnahme des Azure-Verwaltungszertifikats.

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Cloud Services**, und wählen Sie dann **Cloudverwaltungsgateway** aus. Klicken Sie im Menüband auf **Cloudverwaltungsgateway erstellen**. 
2. Wählen Sie auf der Seite **Allgemein** die Option **Azure Resource Manager-Bereitstellung** aus. Klicken Sie auf **Anmelden**, um sich mit dem Administratorkonto eines Azure-Abonnements zu authentifizieren. Der Assistent füllt die verbleibenden Felder automatisch aus den Azure AD-Abonnementinformationen auf, die im Rahmen der Voraussetzungen für die Integration gespeichert wurden. Wenn Sie mehrere Abonnements besitzen, wählen Sie das Abonnement aus, das Sie verwenden möchten. Klicken Sie auf **Weiter**.  
3. Geben Sie auf der Seite **Einstellungen** wie gewohnt das PKI-Serverzertifikat an. Dieses Zertifikat definiert den CMG-Dienstnamen in Azure. Wählen Sie die **Region** und danach eine der Ressourcengruppenoptionen **Neu erstellen** oder **Vorhandene verwenden** aus. Geben Sie den Namen für die neue Ressourcengruppe ein, oder wählen Sie aus der Dropdownliste eine vorhandene Ressourcengruppe aus. 
4. Schließen Sie den Assistenten ab.

> [!NOTE] 
> Azure weist der ausgewählten Azure AD-Server-App die Abonnementberechtigung **Mitwirkender** zu. 

Überwachen Sie den Fortschritt der Dienstbereitstellung mit **cloudmgr.log** auf dem Dienstverbindungspunkt.



## <a name="approve-application-requests-for-users-per-device"></a>Genehmigen von Anwendungsanforderungen für Benutzer pro Gerät
<!-- 1357015 -->
Ab diesem Release ist der Name des Geräts jetzt Teil der Anforderung, wenn ein Benutzer eine Anwendung anfordert, für die eine Genehmigung erforderlich ist. Wenn ein Administrator die Anforderung genehmigt, kann der Benutzer die Anwendung nur auf diesem spezifischen Gerät installieren. Der Benutzer muss eine weitere Anforderung senden, um die Anwendung auf einem anderen Gerät installieren zu können. 

> [!NOTE]
> Dieses Feature ist optional. Wenn Sie ein Update auf dieses Release durchführen, aktivieren Sie dieses Feature im Update-Assistenten. Alternativ dazu können Sie das Feature auch später in der Konsole aktivieren. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Voraussetzungen
- Aktualisieren Sie den Configuration Manager-Client auf die neueste Version.
- Aktivieren Sie die Clienteinstellung **Neues Softwarecenter verwenden** in der Gruppe [Computer-Agent](../clients/deploy/about-client-settings.md#computer-agent).

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Stellen Sie eine Anwendung als für eine Benutzersammlung verfügbar bereit.
2. Aktivieren Sie auf der Seite **Bereitstellungseinstellungen** die Option: **Ein Administrator muss eine Anforderung für diese Anwendung auf dem Gerät genehmigen**.
3. Als Zielbenutzer verwenden Sie das Softwarecenter, um eine Anforderung für die Anwendung zu übermitteln. 
4. Sehen Sie sich in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** die **Genehmigungsanforderungen** an. Sie finden jetzt in Liste eine Spalte **Gerät** für jede Anforderung. Wenn Sie eine Aktion zur Anforderung ausführen, enthält das Dialogfeld „Anwendungsanforderung“ auch den Namen des Geräts, von dem aus der Benutzer die Anforderung übermittelt hat.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Verwenden des Softwarecenters zum Durchsuchen und Installieren von Anwendungen, die für Benutzer verfügbar sein sollen, auf in Azure AD eingebundenen Geräten
<!-- 1322613 -->
Wenn Sie Anwendungen als für Benutzer verfügbar bereitstellen, können diese die Anwendungen über das Softwarecenter auf Azure Active Directory-Geräten durchsuchen und installieren.  

### <a name="prerequisites"></a>Voraussetzungen
- Aktivieren Sie HTTPS auf dem Verwaltungspunkt.
- Integrieren Sie den Standort in [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md).
- Stellen Sie eine Anwendung als für eine Benutzersammlung verfügbar bereit.
- Verteilen Sie Anwendungsinhalte an einen [Cloudverteilungspunkt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md).
- Aktivieren Sie die Clienteinstellung **Neues Softwarecenter verwenden** in der Gruppe [Computer-Agent](../clients/deploy/about-client-settings.md#computer-agent).
- Für den Client gelten folgende Voraussetzungen: 
   - Windows 10
   - Er muss in Azure AD eingebunden sein, dies wird auch als „in die Clouddomäne eingebunden“ bezeichnet.
- Zur Unterstützung internetbasierter Clients:
    - [Cloudverwaltungsgateway](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Aktivieren Sie die Clienteinstellung: **Benutzerrichtlinienanforderungen von Internetclients aktivieren** in der Gruppe [Clientrichtlinie](../clients/deploy/about-client-settings.md#client-policy).
- Zur Unterstützung von Clients im Unternehmensnetzwerk:
    - Fügen Sie den Cloudverteilungspunkt zu einer Begrenzungsgruppe hinzu, die von den Clients verwendet wird.
    - Clients müssen den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des HTTPS-fähigen Verwaltungspunkts auflösen können.



## <a name="report-on-windows-autopilot-device-information"></a>Melden von Windows AutoPilot-Geräteinformationen
<!-- 1351442 -->
Windows AutoPilot ist eine moderne Lösung für das Onboarding und Konfigurieren neuer Windows 10-Geräte. Weitere Informationen finden Sie unter [Übersicht über Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Eine Methode, vorhandene Geräte bei Windows AutoPilot zu registrieren, ist das Hochladen von Geräteinformationen in den Microsoft Store für Unternehmen und Bildungseinrichtungen. Zu diesen Informationen gehört die Seriennummer des Geräts, der Windows-Produktbezeichner und eine Hardwarebezeichner. Verwenden Sie Configuration Manager, um diese Geräteinformationen zu erfassen und zu melden. 

### <a name="prerequisites"></a>Voraussetzungen
- Die Geräteinformationen gelten nur für Clients unter Windows 10, Version 1703 und höher.

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** nacheinander die Knoten **Berichterstellung** und **Berichte**, und wählen Sie den Knoten **Hardware – allgemein** aus.
2. Führen Sie den neuen Bericht **Windows AutoPilot-Geräteinformationen** aus, und sehen Sie sich die Ergebnisse an. 
3. Klicken Sie im Berichts-Viewer auf das Symbol **Exportieren**, und wählen Sie die Option **CSV (Komma-getrennt)** aus.
4. Nachdem Sie die Datei gespeichert haben, laden Sie die Daten in den Microsoft Store für Unternehmen und Bildungseinrichtungen hoch. Weitere Informationen finden Sie unter [Hinzufügen von Geräten zum Microsoft Store für Unternehmen und Bildungseinrichtungen](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Verbesserungen an Configuration Manager-Richtlinien für Windows Defender Exploit Guard
<!-- 1356220 -->
In Configuration Manager für [Windows Defender Exploit Guard](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) wurden zusätzliche Richtlinieneinstellungen für die Komponenten für die Verringerung der Angriffsfläche und den überwachten Ordnerzugriff hinzugefügt.

**Neue Einstellungen für den überwachten Ordnerzugriff**<br/>
Es gibt zwei weitere Optionen, wenn Sie den überwachten Ordnerzugriff konfigurieren: **Nur Datenträgersektoren blockieren** und **Nur Datenträgersektoren überwachen**. Mit diesen beiden Einstellungen kann der überwachte Ordnerzugriff nur für Bootsektoren aktiviert werden, der Schutz bestimmter Ordner oder der standardmäßig geschützten Ordner wird damit nicht aktiviert. 

**Neue Einstellungen zur Verringerung der Angriffsfläche**
- Nutzen Sie einen erweiterten Schutz vor Ransomware.
- Blockieren Sie den Diebstahl von Anmeldeinformationen vom Subsystem der lokalen Windows-Sicherheitsautorität. 
- Blockieren Sie die Ausführung von ausführbaren Dateien, wenn diese bestimmte Kriterien hinsichtlich Verbreitung, Alter oder Vertrauenswürdigkeit nicht erfüllen. 
- Blockieren Sie die Ausführung nicht vertrauenswürdiger und nicht signierter Prozesse von einem USB-Datenträger.



## <a name="microsoft-edge-browser-policies"></a>Richtlinien für den Microsoft Edge-Browser
<!-- 1357310 -->
Kunden, die den [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256)-Webbrowser auf Windows 10-Clients verwenden, können jetzt eine Richtlinie für Configuration Manager-Konformitätseinstellungen erstellen, um verschiedene Microsoft Edge-Einstellungen zu konfigurieren. Diese Richtlinie umfasst derzeit die folgenden Einstellungen:
- **Microsoft Edge-Browser als Standard** festlegen: Konfiguriert die Windows 10-Standard-App-Einstellung für Webbrowser auf Microsoft.
- **Dropdown in der Adressleiste zulassen:** Erfordert Windows 10, Version 1703 oder höher. Weitere Informationen finden Sie unter der [AllowAddressBarDropdown-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Das Synchronisieren von Favoriten zwischen Microsoft-Browsern zulassen:** Erfordert Windows 10, Version 1703 oder höher. Weitere Informationen finden Sie unter der [SyncFavoritesBetweenIEAndMicrosoftEdge-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Das Löschen von Browserdaten beim Beenden zulassen:** Erfordert Windows 10, Version 1703 oder höher. Weitere Informationen finden Sie unter der [ClearBrowsingDataOnExit-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **DNT-Kopfzeilen zulassen:** Weitere Informationen finden Sie unter [AllowDoNotTrack-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **AutoAusfüllen zulassen:** Weitere Informationen finden Sie unter [AllowAutofill-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Cookies zulassen:** Weitere Informationen finden Sie unter [AllowCookies-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Popupblocker zulassen:** Weitere Informationen finden Sie unter [AllowPopups-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Suchvorschläge in Adressleiste zulassen:** Weitere Informationen finden Sie unter [AllowSearchSuggestionsinAddressBar-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Senden von Intranetdatenverkehr an Internet Explorer zulassen:** Weitere Informationen finden Sie unter [SendIntranetTraffictoInternetExplorer-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Kennwort-Manager zulassen:** Weitere Informationen finden Sie unter [AllowPasswordManager-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Entwicklertools zulassen:** Weitere Informationen finden Sie unter [AllowDeveloperTools-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Erweiterungen zulassen:** Weitere Informationen finden Sie unter [AllowExtensions-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Voraussetzungen
- In Azure Active Directory eingebundener Windows 10-Client. 

### <a name="known-issues"></a>Bekannte Probleme
- Für lokale in die Domäne eingebundene Geräte kann diese Richtlinie in diesem Release nicht angewendet werden. Dieses Problem trifft auch auf hybride, in die Domäne eingebundene Geräte zu.

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

**Erstellen der Richtlinie**
1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie **Konformitätseinstellungen**, und wählen Sie den neuen Knoten **Microsoft Edge-Browserprofile** aus. Klicken Sie auf die Menübandoption **Richtlinie für den Microsoft Edge-Browser erstellen**.
2. Geben Sie einen **Namen** für die Richtlinie ein, geben Sie optional eine **Beschreibung** ein, und klicken Sie auf **Weiter**.
3. Ändern Sie auf der Seite **Einstellungen** den Wert für die Einstellungen, die in diese Richtlinie einbezogen werden sollen, zu **Konfiguriert**, und klicken Sie auf **Weiter**.
4. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen und -architekturen aus, für die diese Richtlinie gelten soll, und klicken Sie auf **Weiter**. 
5. Schließen Sie den Assistenten ab.

**Bereitstellen der Richtlinie**
1. Wählen Sie Ihre Richtlinie aus, und klicken Sie auf die Menübandoption **Bereitstellen**.
2. Klicken Sie auf **Durchsuchen**, um die Benutzer- oder Gerätesammlung auszuwählen, in der die Richtlinie bereitgestellt werden soll. 
3. Wählen Sie nach Bedarf weitere Optionen aus. Generieren Sie Warnungen, wenn die Richtlinie nicht konform ist. Legen Sie den Zeitplan fest, nach dem der Client die Konformität des Geräts mit dieser Richtlinie auswertet.
4. Klicken Sie auf **OK**, um die Bereitstellung zu erstellen.

Wie bei jeder anderen Richtlinie für Konformitätseinstellungen gleicht der Client die Einstellungen gemäß dem von Ihnen angegebenen Zeitplan ab. In der Configuration Manager-Konsole können Sie die [Gerätekonformität überwachen und Berichte anzeigen](../../compliance/deploy-use/monitor-compliance-settings.md).



## <a name="report-for-default-browser-counts"></a>Bericht für Anzahl von Standardbrowsern
<!-- 1357830 -->
Es gibt jetzt einen neuen Bericht, der die Anzahl von Clients anzeigt, auf denen ein bestimmter Webbrowser als Windows-Standardeinstellung festgelegt ist. 

### <a name="known-issues"></a>Bekannte Probleme
- Wenn Sie den Bericht zum ersten Mal öffnen, wird nur die Anzahl angezeigt, nicht die BrowserProgID. Um dieses Problem zu umgehen, bearbeiten Sie die Abfrage für den Bericht, damit folgende Syntax verwendet wird:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.
1. Erweitern Sie in der **Configuration Manager**-Konsole im Arbeitsbereich **Überwachung** nacheinander die Knoten **Berichterstellung** und **Berichte**, und wählen Sie **Software – Unternehmen und Produkte** aus.
2. Führen Sie den Bericht die **Anzahl von Standardbrowsern** aus.

Verwenden Sie für allgemeine BrowserProgIDs die folgende Referenz:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE.HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera Software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Unterstützung für Windows 10-ARM64-Geräte
<!-- 1353704 -->
Ab diesem Release wird der Configuration Manager-Client auf Windows 10-ARM64-Geräten unterstützt. Vorhandene Clientverwaltungsfeatures sollten jetzt mit diesen neuen Geräten funktionieren. Beispiele: Hardware- und Softwareinventur, Softwareupdates und Anwendungsverwaltung. Die Betriebssystembereitstellung wird zurzeit nicht unterstützt. 

## <a name="changes-to-phased-deployments"></a>Änderungen an Bereitstellungen in Phasen
<!-- 1357405 -->
Bereitstellungen in Phasen automatisieren ein koordiniertes Rollout von Software in einer bestimmten Reihenfolge über mehrere Sammlungen hinweg. In dieser Technical Preview-Version kann der Assistent für die Bereitstellung in Phasen für Tasksequenzen in der Verwaltungskonsole fertig gestellt werden, und Bereitstellungen können erstellt werden. Die zweite Phase startet jedoch nicht automatisch, nachdem die Erfolgskriterien der ersten Phase erfüllt wurden. Die zweite Phase kann manuell mit einer SQL-Anweisung gestartet werden.   

### <a name="try-it-out"></a>Probieren Sie es aus!  
  Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.
 
**Erstellen Sie eine Bereitstellung in Phasen für eine Tasksequenz** </br>
1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.
2. Klicken Sie mit der rechten Maustaste auf eine bereits vorhandene Tasksequenz, und klicken Sie auf **Create Phased Deployment** (Bereitstellung in Phasen). 
3. Vergeben Sie auf der Registerkarte **Allgemein** einen Namen für die Bereitstellung in Phasen, fügen Sie (optional)eine Beschreibung hinzu, und klicken Sie auf **Standardmäßige Bereitstellung in zwei Phasen automatisch erstellen**. 
4. Füllen Sie die Felder **Erste Sammlung** und **Zweite Sammlung** auf. Wählen Sie **Weiter** aus.
5. Wählen Sie in der Registerkarte **Einstellungen** für jede Einstellung des Zeitplans eine Option aus, und klicken Sie anschließend auf **Weiter**. 
6. Bearbeiten Sie die Phasen falls nötig in der Registerkarte **Phasen**, und klicken Sie auf **Weiter**.
7. Bestätigen Sie Ihre Auswahl in der Registerkarte **Zusammenfassung**, und klicken Sie auf **Weiter**, um fortzufahren.
8. Wenn die Erfolgskriterien für die erste Phase erfüllt wurden, befolgen Sie die Anweisungen, um die zweite Phase mit einer SQL-Anweisung zu starten.
 
**Starten der zweiten Phase mit einer SQL-Anweisung**
1. Ermitteln Sie mit der folgenden SQL-Abfrage die PhasedDeploymentID für Ihre erstellte Bereitstellung:<br/> `Select * from PhasedDeployment`
2. Führen Sie die folgende Anweisung aus, um die Produktionsphase zu starten:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
