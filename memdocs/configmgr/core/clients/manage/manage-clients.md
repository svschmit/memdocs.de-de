---
title: Verwalten von Clients
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Clients in Configuration Manager verwalten.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6d1ee82e116a6d4375e37ccca84c8b35707f8e1
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334588"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Verwalten von Clients in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn der Konfigurations-Manager-Client auf einem Gerät installiert und erfolgreich einem Standort zugewiesen wurde, wird Ihnen das Gerät im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Geräte** angezeigt sowie in mindestens einer Sammlung im Knoten **Gerätesammlungen**. Wählen Sie das Gerät oder eine Sammlung aus, und führen Sie dann Verwaltungsvorgänge aus. Es gibt jedoch andere Möglichkeiten, um den Client zu verwalten. Hierfür können andere Arbeitsbereiche in der Konsole oder Aufgaben außerhalb der Konsole verwendet werden.  

> [!NOTE]  
> Wenn der Configuration Manager-Client installiert wurde, aber noch nicht erfolgreich einem Standort zugewiesen wurde, wird dieser möglicherweise nicht in der Konsole angezeigt. Nachdem der Client einem Standort zugewiesen wurde, aktualisieren Sie die Sammlungsmitgliedschaft und dann die Konsolenansicht.  
>
> Ein Gerät kann auch in der Konsole angezeigt werden, wenn der Configuration Manager-Client nicht installiert wurde. Dieses Verhalten tritt auf, wenn der Standort ein Gerät ermittelt, aber der Client nicht installiert und zugewiesen wurde.
>
> Mobile Geräte, die mit dem [Exchange Server-Connector](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) oder der [lokalen Verwaltung mobiler Geräte](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) verwaltet werden, installieren den Configuration Manager-Client nicht.  
>
> Verwenden Sie die Spalte **Client** im Knoten **Geräte**, um zu ermitteln, ob der Client installiert ist, um ein Gerät über die Konsole zu verwalten.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Verwalten von Clients mithilfe des Knotens **Geräte**  

Je nach Typ des Geräts sind einige dieser Optionen möglicherweise nicht verfügbar.  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Geräte** aus.  

2. Wählen Sie mindestens ein Gerät aus, und wählen Sie dann einen der Clientverwaltungstasks aus dem Menüband aus. (Alternativ können Sie mit der rechten Maustaste auf das Gerät klicken.)  

### <a name="import-user-device-affinity"></a>Importieren der Affinität zwischen Benutzer und Gerät

Konfigurieren Sie die Zuordnungen zwischen Benutzern und Geräten, sodass Sie Benutzern Software effizient bereitstellen können.  

Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="import-computer-information"></a>Importieren von Computerinformationen

Starten Sie den **Assistent zum Importieren von Computerinformationen**, um neue Computerinformationen in die Configuration Manager-Datenbank zu importieren. Sie können mehrere Computer mithilfe einer Datei importieren oder Informationen für einen einzelnen Computer angeben.

### <a name="add-selected-items"></a>Hinzufügen ausgewählter Elemente

Bietet folgende Optionen:

- **Ausgewählte Elemente der vorhandenen Gerätesammlung hinzufügen:** Öffnet das Dialogfeld **Sammlung auswählen** . Wählen Sie die Sammlung aus, zu der Sie dieses Gerät hinzufügen möchten. Das Gerät wird mithilfe der Regel für **direkte Mitgliedschaft** in die Sammlung eingefügt.  

- **Ausgewählte Elemente der neuen Gerätesammlung hinzufügen:** öffnet den **Assistenten zum Erstellen von Gerätesammlungen**, mit dem Sie eine neue Sammlung erstellen können. Die ausgewählte Sammlung wird mithilfe der Regel für **direkte Mitgliedschaft** in die Sammlung eingefügt.  

Weitere Informationen finden Sie unter [Erstellen von Sammlungen](collections/create-collections.md).

### <a name="install-client"></a>Client installieren

Öffnet den **Assistenten zur Clientinstallation**. Dieser Assistent nutzt eine Clientpushinstallation, um den Configuration Manager-Client auf dem ausgewählten Gerät zu installieren bzw. noch mal zu installieren.

> [!TIP]  
> Es gibt viele verschiedene Möglichkeiten, den Configuration Manager-Client zu installieren. Obwohl die Clientpushinstallation eine praktische Methode zum Installieren des Clients über die Konsole darstellt, weist diese Methode viele Abhängigkeiten auf und eignet sich nicht für alle Umgebungen. Weitere Informationen über Abhängigkeiten finden Sie unter [Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation). Weitere Informationen zu anderen Clientinstallationsmethoden finden Sie unter [Clientinstallationsmethoden](../deploy/plan/client-installation-methods.md).

Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe von Clientpush](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

### <a name="run-script"></a>Skript ausführen

Öffnet den Assistenten zum **Ausführen von Skripts**, um ein PowerShell-Skript auf dem ausgewählten Gerät auszuführen.

Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="install-application"></a>Installieren der Anwendung

Installieren Sie eine Anwendung in Echtzeit auf einem Gerät. Dieses Feature kann dazu beitragen, den Bedarf an getrennten Sammlungen für jede Anwendung zu reduzieren.

Weitere Informationen finden Sie unter [Installieren von Anwendungen auf einem Gerät](../../../apps/deploy-use/install-app-for-device.md).

### <a name="reassign-site"></a>Neuzuweisen des Standorts

Weisen Sie bei Bedarf einen oder mehrere Clients, einschließlich verwalteter mobiler Geräte, einem anderen primären Standort in der Hierarchie neu zu. Sie können Clients einzeln neu zuweisen oder mehrere auswählen, um sie in größeren Mengen neu zuzuweisen.  

### <a name="client-settings---resultant-client-settings"></a>Clienteinstellungen: resultierende Clienteinstellungen

Wenn Sie mehrere Clienteinstellungen auf demselben Gerät bereitstellen, ist die Priorisierung und Kombination der Einstellungen eine komplexe Angelegenheit. Verwenden Sie diese Option, um die resultierenden Clienteinstellungen anzuzeigen, die auf diesem Gerät bereitgestellt werden.

Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../deploy/configure-client-settings.md).

### <a name="start"></a>Starten

- Führen Sie **Ressourcen-Explorer** aus, um die Informationen zur Hardware- und Softwareinventur eines Windows-Clients anzuzeigen. Weitere Informationen finden Sie in den folgenden Artikeln:

  - [Verwenden von Ressourcen-Explorer zum Anzeigen des Hardwarebestands](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Verwenden von Ressourcen-Explorer zum Anzeigen des Softwarebestands](inventory/use-resource-explorer-to-view-software-inventory.md)

- Verwalten Sie das Gerät remote, indem Sie die **Remotesteuerung**, die **Remoteunterstützung** oder den **Remotedesktopclient** verwenden. Weitere Informationen finden Sie unter [Remoteverwaltung eines Windows-Clientcomputers](remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="approve"></a>Genehmigen

Wenn die Kommunikation zwischen Client und Standortsystemen über HTTP erfolgt und ein selbstsigniertes Zertifikat verwendet wird, müssen Sie die Clients genehmigen, um sie als vertrauenswürdige Computer zu identifizieren. Standardmäßig werden Clients aus der gleichen Active Directory-Gesamtstruktur, aus vertrauenswürdigen Gesamtstrukturen sowie verbundene Azure AD-Mandanten (Azure Active Directory) von der Standortkonfiguration automatisch genehmigt<!-- MEMDocs#318 -->. Aufgrund dieses Standardverhaltens müssen Sie nicht jeden Client manuell genehmigen. Arbeitsgruppencomputer und andere Computer, die Sie als vertrauenswürdig einstufen, die jedoch nicht genehmigt sind, müssen Sie jedoch manuell genehmigen.

> [!IMPORTANT]  
> Bei nicht genehmigten Clients sind einige Verwaltungsfunktionen möglicherweise nicht ausführbar. Dieses Szenario wird jedoch für Configuration Manager nicht unterstützt.  

Sie müssen keine Clients genehmigen, deren Kommunikation mit Standortsystemen immer über HTTPS erfolgt, und auch keine Clients, von denen zur Kommunikation mit Standortsystemen über HTTP ein PKI-Zertifikat verwendet wird. Von diesen Clients wird mithilfe der PKI-Zertifikate eine Vertrauensstellung hergestellt.

### <a name="block-or-unblock"></a>Blockieren und Zulassen

Blockieren Sie einen Client, den Sie nicht mehr als vertrauenswürdig einstufen. Durch das Blockieren wird verhindert, dass der Client Richtlinien empfängt und dass die Standortsysteme mit diesem kommunizieren.  

> [!IMPORTANT]  
> Durch das Blockieren eines Clients wird nur die Kommunikation vom Client an die Configuration Manager-Standortsysteme verhindert. Die Kommunikation mit anderen Geräten wird nicht verhindert. Aus Sicherheitsgründen gibt es einige Einschränkungen, wenn die Kommunikation vom Client mit den Standortsystemen über HTTP anstatt HTTPS erfolgt.  

Sie können die Blockierung blockierter Clients wieder aufheben.

Weitere Informationen finden Sie unter [Bestimmen, ob Clients blockiert werden sollen](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Löschen erforderlicher PXE-Bereitstellungen

Sie können eine erforderliche PXE-Bereitstellung erneut bereitstellen, indem Sie den Status der letzten PXE-Bereitstellung löschen, die einer Configuration Manager-Sammlung oder einem Computer zugewiesen ist. Mit dieser Aktion wird der Status der Bereitstellung zurückgesetzt, und die letzten erforderlichen Bereitstellungen werden erneut installiert.

Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### <a name="client-notification"></a>Clientbenachrichtigung

Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](client-notification.md#client-notification).

### <a name="endpoint-protection"></a>Endpoint Protection

Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](client-notification.md#endpoint-protection).

### <a name="edit-primary-users"></a>Bearbeiten primärer Benutzer

Sie können die Benutzer des Geräts der letzten 90 Tage anzeigen oder den primären Benutzer des Geräts festlegen.

Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="wipe-a-mobile-device"></a>Zurücksetzen eines mobilen Geräts

Sie können mobile Geräte zurücksetzen, die den betreffenden Befehl unterstützen. Durch diese Aktion werden alle Daten auf den mobilen Geräten endgültig gelöscht. Hiervon sind auch die persönlichen Einstellungen und Daten betroffen. Normalerweise wird das mobile Gerät durch diese Aktion auf die Werkseinstellungen zurückgesetzt. Bereinigen Sie mobile Geräte, wenn sie nicht mehr vertrauenswürdig sind. Dies wird beispielsweise empfohlen, wenn das Gerät verloren geht oder gestohlen wird.  

> [!TIP]  
> Lesen Sie die Dokumentation des Herstellers, um sich darüber zu informieren, wie ein Befehl zum Remotezurücksetzen vom Gerät verarbeitet wird.  

Der Zurücksetzungsbefehl wird oft erst nach einer zeitlichen Verzögerung vom mobilen Gerät empfangen:  

- Wenn das mobile Gerät von Configuration Manager registriert wurde, empfängt der Client den Befehl, sobald die Clientrichtlinie das nächste Mal heruntergeladen wird.

- Wenn das mobile Gerät vom Exchange Server-Connector verwaltet wird, wird der Befehl empfangen, wenn die nächste Synchronisierung mit Exchange erfolgt.  

Verwenden Sie die Spalte **Zurücksetzungsstatus**, um zu überwachen, wann der Zurücksetzungsbefehl empfangen wird. Sie können den Zurücksetzungsbefehl abbrechen, bis vom Gerät eine Zurücksetzungsbestätigung an Configuration Manager gesendet wird.  

### <a name="retire-a-mobile-device"></a>Außerkraftsetzen eines mobilen Geräts

Die Option **Außerkraftsetzen** wird nur von mobilen Geräten unterstützt, die mit der lokalen Verwaltung mobiler Geräte registriert wurden.  

Weitere Informationen finden Sie unter [Schützen von Daten mit Remotezurücksetzung, Remotesperre oder Zurücksetzen der Kennung](../../../mdm/deploy-use/wipe-lock-reset-devices.md).

### <a name="change-ownership"></a>Ändern des Besitzers

Wenn ein Gerät nicht mit einer Domäne verknüpft ist oder über eine Installation des Configuration Manager-Clients verfügt, verwenden Sie diese Option, um den Besitz von **Unternehmen** in **Persönlich** zu ändern.  

Sie können diesen Wert in Anwendungsanforderungen zum Steuern von Bereitstellungen verwenden und auch die Menge der Inventurinformationen steuern, die von Geräten von Benutzern gesammelt werden.  

Möglicherweise müssen Sie der Ansicht die Spalte **Gerätebesitzer** hinzufügen, indem Sie mit der rechten Maustaste auf eine beliebige Spaltenüberschrift klicken und sie auswählen.

### <a name="delete"></a>Löschen

> [!WARNING]  
> Löschen Sie einen Client nicht, wenn Sie den Configuration Manager-Client deinstallieren oder aus einer Sammlung entfernen möchten.  

Mit der Aktion **Löschen** wird der Clientdatensatz manuell aus der Configuration Manager-Datenbank entfernt. Verwenden Sie diese Aktion ausschließlich zum Beheben eines Problems. Wenn Sie das Objekt löschen, der Client aber weiterhin installiert ist und mit dem Standort kommuniziert, erstellt die Frequenzermittlung den Clientdatensatz noch mal. Er wird noch mal in der Configuration Manager-Konsole angezeigt, obwohl der Clientverlauf und bisherige Zuordnungen nicht mehr vorhanden sind.  
> [!NOTE]  
> Wenn Sie einen Client eines mobilen Geräts löschen, der von Configuration Manager registriert wurde, widerruft diese Aktion auch das ausgestellte PKI-Zertifikat. Dieses Zertifikat wird dann vom Verwaltungspunkt abgelehnt, auch wenn IIS die CRL (Zertifikatsperrungsliste) nicht überprüft.
>
> Zertifikate auf Legacyclients bei mobilen Geräten werden nicht gesperrt, wenn Sie diese Clients löschen.

Informationen zum Deinstallieren des Clients finden Sie unter [Deinstallieren des Configuration Manager-Clients](#BKMK_UninstalClient).  

Informationen zum Zuweisen des Clients zu einem neuen primären Standort finden Sie unter [Zuweisen von Clients zu einem Standort](../deploy/assign-clients-to-a-site.md).

Konfigurieren Sie die Sammlungseigenschaften neu, um den Client aus einer Sammlung zu entfernen. Weitere Informationen finden Sie unter [Verwalten von Sammlungen](collections/manage-collections.md).

### <a name="refresh"></a>Aktualisieren

Aktualisieren Sie die Konsolenansicht mit den neuesten Daten in der Datenbank. Beispielsweise wenn ein Gerät in der Ermittlungsliste angezeigt wird, aber nicht als installiert angezeigt wird. Nachdem Sie den Client installiert und sichergestellt haben, dass er dem Standort zugewiesen ist, klicken Sie auf **Aktualisieren**.

### <a name="properties"></a>Eigenschaften

Überprüfen Sie die Ermittlungsdaten und Bereitstellungen für den Client.

Sie können außerdem Variablen konfigurieren, die von Tasksequenzen zum Bereitstellen eines Betriebssystems für das Gerät verwendet werden. Weitere Informationen finden Sie unter [Erstellen von Tasksequenzvariablen für Geräte und Sammlungen](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Verwalten von Clients mithilfe des Knotens **Gerätesammlungen**

Viele der Aufgaben, die im Knoten **Geräte** für Geräte verfügbar sind, sind ebenfalls für Sammlungen verfügbar. Die Konsole führt den Vorgang automatisch für alle qualifizierten Geräte in der Sammlung aus. Wenn eine Aktion für eine gesamte Sammlung ausgeführt wird, werden zusätzliche Netzwerkpakete generiert und die CPU-Nutzung auf dem Standortserver steigt.  

Beachten Sie die folgenden Fragen, bevor Sie Tasks auf der Sammlungsebene ausführen. Nach dem Start kann der Task nicht mehr in der Konsole beendet werden.

- Wie viele Geräte befinden sich in der Sammlung?
- Sind die Geräte über Netzwerkverbindungen mit geringer Bandbreite verbunden?
- Wie viel Zeit muss aufgewendet werde, um diese Aufgabe für alle Geräte auszuführen?

Weitere Informationen finden Sie unter [Verwalten von Sammlungen](collections/manage-collections.md).


## <a name="restart-clients"></a>Neustarten von Clients

Verwenden Sie die Configuration Manager-Konsole, um Clients zu identifizieren, für die ein Neustart erforderlich ist. Verwenden Sie eine Aktion zur Clientbenachrichtigung, um diese neu zu starten.

> [!Tip]
> Aktivieren Sie das automatische Clientupgrade, um Ihre Clients mit weniger Aufwand auf dem neuesten Stand zu halten. Weitere Informationen finden Sie unter [Informationen zum automatischen Clientupgrade](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Wechseln Sie zum Arbeitsbereich **Bestand und Kompatibilität** in der Configuration Manager-Konsole, und klicken Sie auf den Knoten **Geräte**, um Geräte zu identifizieren, für die ein Neustart aussteht. Zeigen Sie dann im Bereich „Details“ den Status für jedes Gerät in einer neuen Spalte namens **Neustart ausstehend** an. Jedes Gerät besitzt mindestens einen der folgenden Werte:

- **Nein:** Es steht kein Neustart aus.
- **Configuration Manager:** Dieser Wert stammt aus der Koordinierungskomponente für den Neustart des Clients (RebootCoordinator.log).
- **Datei umbenennen:** Dieser Wert stammt aus einem Bericht von Windows für einen ausstehenden Umbenennungsvorgang für eine Datei (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations).
- **Windows Update:** Dieser Wert stammt vom Windows Update-Agent, der meldet, dass ein ausstehender Neustart für mindestens ein Update erforderlich ist (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired).
- **Feature hinzufügen oder entfernen:** Dieser Wert stammt von einem komponentenbasierten Windows-Dienst und gibt an, dass das Hinzufügen oder Entfernen eines Windows-Features einen Neustart erfordert (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending).

### <a name="create-the-client-notification-to-restart-a-device"></a>Erstellen einer Clientbenachrichtigung zum Neustarten eines Geräts

1. Wählen Sie das Gerät in der Sammlung im Knoten **Gerätesammlungen** der Konsole aus, das Sie neu starten möchten.
2. Klicken Sie im Menüband auf **Clientbenachrichtigung**, und klicken Sie dann auf **Neu starten**. Dadurch wird ein Fenster mit Informationen zum Neustart geöffnet. Klicken Sie zum Bestätigen der Anforderung des Neustarts auf **OK**.

Wenn ein Client diese Benachrichtigung empfängt, wird dort ein **Softwarecenter**-Benachrichtigungsfenster geöffnet, um den Benutzer über den Neustart zu informieren. Standardmäßig erfolgt der Neustart nach 90 Minuten. Sie können den Zeitpunkt des Neustarts durch Konfigurieren der [Clienteinstellungen](../deploy/configure-client-settings.md) ändern. Sie finden die Einstellungen für das Neustartverhalten in den Standardeinstellungen auf der Registerkarte [Computerneustart](../deploy/about-client-settings.md#computer-restart).


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a> Konfigurieren des Clientcaches

Der Clientcache speichert temporäre Dateien, die beim Installieren von Anwendungen und Programmen durch Clients verwendet werden. Softwareupdates verwenden ebenfalls den Clientcache. Diese versuchen jedoch unabhängig von der Größeneinstellung stets, Downloads in den Cache durchzuführen. Konfigurieren Sie die Cacheeinstellungen (z.B. Größe und Speicherort), wenn Sie den Client installieren, die Clientpushinstallation verwenden oder die Installation abgeschlossen haben.

Sie können die Cacheordnergröße mithilfe von Clienteinstellungen in der Configuration Manager-Konsole konfigurieren. Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../deploy/about-client-settings.md#client-cache-settings).

Der Standardspeicherort für den Configuration Manager-Clientcache ist `%windir%\ccmcache`, und der Standardspeicherplatz auf dem Datenträger beträgt 5120 MB.  

> [!IMPORTANT]  
> Verschlüsseln Sie den Ordner für den Clientcache nicht. Das Herunterladen von Inhalten in einen verschlüsselten Ordner ist nicht möglich.  

### <a name="about-the-client-cache"></a>Informationen zum Clientcache  

Der Configuration Manager-Client lädt den Inhalt für erforderliche Software unmittelbar nach dem Zeitpunkt der Verfügbarkeit der Bereitstellung herunter, führt ihn jedoch erst zum geplanten Bereitstellungszeitpunkt aus. Zum geplanten Zeitpunkt überprüft der Configuration Manager-Client, ob der Inhalt im Cache verfügbar ist. Wenn Inhalte im Cache enthalten sind und in der richtigen Version vorliegen, werden diese Cacheinhalte verwendet. Wenn die erforderliche Version des Inhalts geändert wird oder der Client den Inhalt löscht, um Speicherplatz für ein anderes Paket freizugeben, lädt der Client den Inhalt erneut in den Cache herunter.  

Wenn versucht wird, Inhalte für ein Programm oder eine Anwendung herunterzuladen, deren Größe die Cachegröße überschreitet, tritt bei der Bereitstellung wegen unzureichender Cachegröße ein Fehler auf. Der Client generiert die Statusmeldung 10050 für unzureichende Cachegröße. Das spätere Erhöhen der Cachegröße führt zu folgendem Ergebnis:  

- Erforderliches Programm: Der Client versucht nicht automatisch noch mal, den Inhalt herunterzuladen. Stellen Sie das Paket und das Programm erneut für den Client bereit.  
- Erforderliche Anwendung: Der Client versucht beim Herunterladen der Clientrichtlinie erneut automatisch, die Inhalte herunterzuladen.  

Wenn der Client versucht, Inhalte herunterzuladen, die die Cachegröße unterschreiten, der Cache jedoch voll ist, werden alle *erforderlichen* Bereitstellungen wiederholt versucht, bis:

- der Cachespeicher verfügbar ist.
- ein Timeout für den Download auftritt.
- die Anzahl der Wiederholungen den Grenzwert erreicht.

Wenn Sie die Cachegröße später erhöhen, wird vom Client im nächsten Wiederholungsintervall noch mal versucht, die Inhalte herunterzuladen. Der Client startet alle vier Stunden einen neuen Versuch, die Inhalte herunterzuladen, bis 18 Versuche ausgeführt wurden.  

Inhalte im Cache werden nicht automatisch gelöscht. Sie werden mindestens einen Tag lang im Cache beibehalten, nachdem sie vom Client verwendet wurden. Wenn Sie die Inhalte so konfigurieren, dass diese dauerhaft im Clientcache gespeichert werden, werden sie nicht automatisch vom Client gelöscht. Wenn der Cachespeicher von Inhalten verwendet wird, die innerhalb der letzten 24 Stunden heruntergeladen wurden, und der Client neue Inhalte herunterladen muss, können Sie entweder den Cachespeicher erhöhen oder die Option zum Löschen von gespeicherten Cacheinhalten auswählen.

Nur für Anwendungen: Wenn die Inhalte für eine zugehörige Bereitstellung derzeit im Cache vorhanden sind, lädt der Client nur neue oder geänderte Dateien herunter. Zugehörige Bereitstellungen umfassen solche für ältere Revisionen desselben Bereitstellungstyps und von abgelösten Anwendungen.

Gehen Sie wie folgt vor, um den Clientcache während der manuellen Clientinstallation oder nach der Installation des Clients zu konfigurieren.  

### <a name="configure-the-cache-during-manual-client-installation"></a>Konfigurieren des Caches während der manuellen Clientinstallation  

Führen Sie den Befehl CCMSetup.exe vom Installationsquellspeicherort aus. Geben Sie dabei nach Bedarf die folgenden Eigenschaften durch Leerzeichen getrennt an:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Verwenden Sie anstelle vom SMSCACHESIZE die Einstellungen für die Cachegröße, die in den **Clienteinstellungen** in der Configuration Manager-Konsole verfügbar sind. Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../deploy/about-client-settings.md#client-cache-settings).

Weitere Informationen zum Verwenden dieser Befehlszeileneigenschaften für „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften](../deploy/about-client-installation-properties.md).

### <a name="configure-the-cache-during-client-push-installation"></a>Konfigurieren des Caches während der Clientpushinstallation  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Wählen Sie den entsprechenden Standort aus. Klicken Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und wählen Sie **Clientpushinstallation** aus. Wechseln Sie zur Registerkarte **Installationseigenschaften**.  

3. Geben Sie die folgenden Eigenschaften getrennt durch Leerzeichen an:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Verwenden Sie anstelle vom SMSCACHESIZE die Einstellungen für die Cachegröße, die in den **Clienteinstellungen** in der Configuration Manager-Konsole verfügbar sind. Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../deploy/about-client-settings.md#client-cache-settings).

     Weitere Informationen zum Verwenden dieser Befehlszeileneigenschaften für „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften](../deploy/about-client-installation-properties.md).  

### <a name="configure-the-cache-on-the-client-computer"></a>Konfigurieren des Caches auf dem Clientcomputer  

1. Öffnen Sie die **Configuration Manager**-Systemsteuerung auf dem Clientcomputer.  

2. Wechseln Sie zur Registerkarte **Cache**. Legen Sie die Eigenschaften für den Speicherplatz und den Speicherort fest. Der Standardspeicherort ist `%windir%\ccmcache`.  

3. Wählen Sie zum Löschen der Dateien im Cacheordner **Dateien löschen** aus.  

### <a name="configure-client-cache-size-in-client-settings"></a>Konfigurieren der Clientcachegröße in den Clienteinstellungen

Sie können die Größe des Clientcaches anpassen, ohne den Client neu installieren zu müssen. Verwenden Sie die Einstellungen für die Cachegröße in den **Clienteinstellungen** der Configuration Manager-Konsole. Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../deploy/about-client-settings.md#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a> Deinstallieren des Clients

Sie können die Configuration Manager-Clientsoftware mithilfe der **CCMSetup.exe** mit der Eigenschaft **/Uninstall** von einem Computer deinstallieren. Führen Sie die „CCMSetup.exe“ auf einem einzelnen Computer über die Eingabeaufforderung aus, oder stellen Sie ein Paket bereit, um den Client von einer Sammlung von Computern zu deinstallieren.  

> [!NOTE]  
> Sie können den Configuration Manager-Client auf mobilen Geräten nicht deinstallieren. Wenn die Deinstallation des Configuration Manager-Clients von einem mobilen Gerät aus erforderlich ist, müssen Sie das Gerät zurücksetzen. Dadurch werden alle Daten auf dem mobilen Gerät gelöscht.  

1. Öffnen Sie eine Windows-Eingabeaufforderung als Administrator. Ändern Sie den Ordner in den Speicherort der „CCMSetup.exe“, z. B. `cd %windir%\ccmsetup`.

2. Führen Sie den folgenden Befehl aus: `CCMSetup.exe /uninstall`

> [!TIP]  
> Bei der Deinstallation werden keine Ergebnisse auf dem Bildschirm angezeigt. Sehen Sie sich die folgende Protokolldatei an, um zu überprüfen, ob der Client erfolgreich deinstalliert wurde: `%windir%\ccmsetup\logs\CCMSetup.log`.  
>
> Wenn Sie warten müssen, bis der Deinstallationsprozess abgeschlossen ist, bevor Sie etwas anderes tun, führen Sie `Wait-Process CCMSetup` in PowerShell aus. Dieser Befehl kann ein Skript anhalten, bis der CCMSetup-Prozess abgeschlossen ist.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a> Verwalten von in Konflikt stehenden Datensätzen

Configuration Manager verwendet Hardware-IDs, um Clients zu identifizieren, bei denen es sich um Duplikate handeln könnte, und informiert Sie über in Konflikt stehende Datensätze. Wenn Sie z.B. einen Computer erneut installieren, bleibt die Hardware-ID unverändert, während die von Configuration Manager verwendete GUID sich ändern kann.  

Configuration Manager löst Konflikte automatisch mithilfe der Windows-Authentifizierung des Computerkontos oder eines PKI-Zertifikats aus einer vertrauenswürdigen Quelle. Wenn Configuration Manager den Konflikt von doppelten Hardware-IDs nicht auflösen kann, bestimmt eine Hierarchieeinstellung das Verhalten.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Ändern der Hierarchieeinstellung zum Verwalten von in Konflikt stehenden Datensätzen  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.

1. Wählen Sie im Menüband **Hierarchieeinstellungen** aus.

1. Wechseln Sie zur Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze**, und wählen Sie eine der folgenden Optionen aus:

    - **In Konflikt stehende Datensätze automatisch auflösen**
    - **In Konflikt stehende Datensätze manuell auflösen**

### <a name="manually-resolve-conflicting-records"></a>In Konflikt stehende Datensätze manuell auflösen  

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie den **Systemstatus**, und wählen Sie den Knoten **In Konflikt stehende Datensätze** aus.  

1. Wählen Sie mindestens einen in Konflikt stehenden Datensatz aus, und klicken Sie dann auf **In Konflikt stehende Datensätze**.  

1. Wählen Sie eine der folgenden Optionen aus:  

    - **Zusammenführen:** Hiermit kombinieren Sie den neu erkannten Datensatz mit dem vorhandenen Clientdatensatz.  

    - **Neu:** Hiermit erstellen Sie einen neuen Datensatz für den in Konflikt stehenden Clientdatensatz.  

    - **Blockieren:** Hiermit erstellen Sie einen neuen Datensatz für den in Konflikt stehenden Clientdatensatz, markieren ihn jedoch als gesperrt.  


## <a name="manage-duplicate-hardware-identifiers"></a>Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients

Sie können eine Liste von Hardware-IDs angeben, die von Configuration Manager für den PXE-Start und die Clientregistrierung ignorieren werden sollen. Diese Liste wirkt zwei gängigen Problemen entgegen:

1. Viele neue Geräte umfassen keinen integrierten Ethernet-Port. Techniker verwenden einen USB-zu-Ethernet-Adapter, um eine Kabelverbindung für die Betriebssystembereitstellung herzustellen. Diese Adapter werden aus Kostengründen und wegen der allgemeinen Nutzbarkeit häufig gemeinsam genutzt. Der Standort verwendet die MAC-Adresse dieses Adapters zum Identifizieren des Geräts. Daher kann die nochmalige Verwendung des Adapters ohne zusätzliche Administratoraktionen nach jeder Bereitstellung zu Problemen führen. Schließen Sie die MAC-Adresse des Adapters aus, um diesen für ein solches Szenario wiederzuverwenden.

2. Während das SMBIOS-Attribut eindeutig sein sollte, verfügen einige spezielle Hardwaregeräte über doppelte IDs. Schließen Sie diese doppelten ID aus, und verwenden Sie die eindeutige MAC-Adresse jedes Geräts.

Verwenden Sie den folgenden Prozess, um zu ignorierende Hardware-IDs für Configuration Manager hinzuzufügen:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.

2. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.

3. Wechseln Sie zur Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze**. Klicken Sie im Abschnitt **Doppelte Hardware-IDs** auf **Hinzufügen**, um neue Hardware-IDs hinzuzufügen.

> [!TIP]
> Ab Version 1910 können Sie die folgenden PowerShell-Cmdlets zum Automatisieren der Verwaltung doppelter Hardwarebezeichner verwenden:<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a> Starten des Richtlinienabrufs

Clientrichtlinien werden von Configuration Manager-Clients nach einem als Clienteinstellung konfigurierten Zeitplan heruntergeladen. Sie können den Richtlinienabruf bei Bedarf auch über den Client starten. Dies ist beispielsweise für die Problembehandlung oder zum Testen von Situationen nützlich.  

- [Clientbenachrichtigung](#bkmk_policy-notify)
- [Clientsystemsteuerung](#bkmk_policy-manual)
- [Support Center (Supportcenter)](#bkmk_policy-support)
- [Skript](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a> Starten des Clientrichtlinienabrufs mit Clientbenachrichtigungen  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie **Geräte** aus.  

1. Wählen Sie das Gerät aus, das Richtlinien herunterladen soll. Klicken Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Gerät** auf **Clientbenachrichtigung**, und klicken Sie dann auf **Computerrichtlinie herunterladen**.  

    > [!NOTE]  
    > Sie können die Clientbenachrichtigung auch verwenden, um den Richtlinienabruf auf allen Geräten in einer Sammlung zu starten.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a> Starten des Clientrichtlinienabrufs über die Configuration Manager-Clientsystemsteuerung

1. Öffnen Sie die **Configuration Manager**-Systemsteuerung auf dem Computer.  

2. Wechseln Sie zur Registerkarte **Aktionen**. Klicken Sie auf **Computerrichtlinienabruf und Auswertungszyklus**, um die Computerrichtlinie zu starten, und klicken Sie anschließend auf **Jetzt ausführen**.  

3. Klicken Sie zum Bestätigen der Eingabeaufforderung auf **OK**.  

4. Wiederholen Sie diese Schritte für alle weiteren Aktionen. Zum Beispiel **Benutzerrichtlinienabruf und Auswertungszyklus** für Benutzerclienteinstellungen.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a> Starten des Clientrichtlinienabrufs über Supportcenter

Verwenden Sie das Supportcenter, um Clientrichtlinien anzufordern und anzuzeigen. Weitere Informationen finden Sie in der [Referenz zum Supportcenter](../../support/support-center-ui-reference.md#bkmk_support-policy).

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a> Starten des Clientrichtlinienabrufs mithilfe eines Skripts  

1. Öffnen Sie einen Skript-Editor, z. B. Notepad oder Windows PowerShell ISE.  

2. Kopieren Sie den folgenden PowerShell-Beispielcode,<!-- SCCMDocs#1591 --> und fügen Sie ihn in die Datei ein:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Weitere Informationen über Plan-IDs finden Sie unter [Nachrichten-IDs](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Speichern Sie die Datei mit der Erweiterung PS1.  

4. Führen Sie das Skript auf dem Client aus.
