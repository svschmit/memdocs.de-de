---
title: Planen von Automatisierungstasks
titleSuffix: Configuration Manager
description: In diesem Artikel wird das Planen von Tasks beschrieben, bevor Sie Tasksequenzen zum Automatisieren von Tasks in Configuration Manager erstellen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708098"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Planen von Automatisierungstasks in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In Ihrer Configuration Manager-Umgebung können Sie Tasksequenzen zum Automatisieren von Tasks erstellen. Diese Tasks reichen von der Erfassung eines Betriebssystems auf einem Referenzcomputer bis zur Bereitstellung des Betriebssystems auf mehreren Zielcomputern. Die Aktionen der Tasksequenz werden in den einzelnen Schritten der Sequenz definiert. Wenn die Tasksequenz ausgeführt wird, werden die Aktionen der einzelnen Schritte auf Befehlszeilenebene im Kontext des lokalen Systems ausgeführt. Dieses Verhalten bedeutet, dass die Tasksequenz ohne Benutzereingriff vollständig automatisiert wird.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a> Tasksequenzschritte und -aktionen  

Schritte sind die Grundkomponenten einer Tasksequenz. Hierzu können Befehle wie die Folgenden zählen:

- Konfigurieren und Erfassen des Betriebssystems eines Referenzcomputers
- Installieren von Windows, Hardwaretreibern, des Configuration Manager-Clients und von Software auf dem Zielcomputer

Die Aktionen des Schritts definieren die Befehle eines Tasksequenzschritts. Es gibt zwei Arten von Aktionen:  

- Eine Aktion, die Sie mit einer Befehlszeilenzeichenfolge definieren, wird als *benutzerdefinierte Aktion* bezeichnet.  
- Eine von Configuration Manager vordefinierte Aktion wird als *integrierte Aktion* bezeichnet.  

Von einer Tasksequenz kann eine beliebige Kombination aus benutzerdefinierten und integrierten Aktionen ausgeführt werden.  

Tasksequenzschritte können auch Bedingungen umfassen, die das Verhalten des Schritts steuern. Zu diesen Verhaltensweisen zählen das Beenden oder Fortsetzen der Tasksequenz, wenn ein Fehler auftritt. Ein Bedingungstyp ist eine Tasksequenzvariable. Beispielsweise testen Sie mit der Variable **SMSTSLastActionRetCode** die Bedingung des vorherigen Schritts. Fügen Sie Bedingungen zu einem einzelnen Schritt oder einer Gruppe von Schritten hinzu.  

Die Tasksequenz verarbeitet Schritte nacheinander. Eine solche Sequenz enthält die Aktion des Schritts sowie Bedingungen für den Schritt. Wenn die Verarbeitung eines Tasksequenzschritts von Configuration Manager gestartet wird, wird der nächste Schritt erst nach Abschluss der vorherigen Aktion gestartet.

Eine Tasksequenz gilt in folgenden Fällen als abgeschlossen:

- Alle zugehörigen Schritte sind abgeschlossen.  
- Ein fehlerhafter Schritt führt dazu, dass Configuration Manager die Ausführung der Tasksequenz beendet, bevor alle Schritte abgeschlossen sind.  

Wenn der Schritt einer Tasksequenz beispielsweise kein referenziertes Image oder Paket auf einem Verteilungspunkt finden kann, enthält die Tasksequenz einen fehlerhaften Verweis. Configuration Manager beendet die Ausführung der Tasksequenz an diesem Punkt, es sei denn, der fehlerhafte Schritt enthält die Bedingung, dass dieser beim Auftreten eines Fehlers fortgesetzt werden soll.  

> [!IMPORTANT]  
> Eine Tasksequenz kann standardmäßig nicht weiter ausgeführt werden, nachdem bei einem Schritt oder einer Aktion ein Fehler aufgetreten ist. Wenn die Tasksequenz auch dann fortgesetzt werden soll, wenn in einem Schritt ein Fehler auftritt, bearbeiten Sie die Tasksequenz, wechseln Sie auf die Registerkarte **Optionen** , und wählen Sie anschließend **Bei Fehler fortsetzen** aus.  

Weitere Informationen zu den Schritten, die einer Tasksequenz hinzugefügt werden können, finden Sie unter [Tasksequenzschritte](../understand/task-sequence-steps.md).  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a> Tasksequenzgruppen  

Mehrere Schritte einer Tasksequenz können gruppiert werden. Eine Tasksequenzgruppe besteht aus einem Namen, einer optionalen Beschreibung und optionalen Bedingungen. Die Tasksequenz wertet die Gruppenbedingungen als Einheit aus, bevor sie mit dem nächsten Schritt fortfährt. Schachteln Sie Gruppen ineinander, oder verwenden Sie eine Kombination aus Schritten und Untergruppen. Gruppen sind zum Kombinieren mehrerer Schritte nützlich, für die eine gemeinsame Bedingung gilt.  

Weisen Sie Tasksequenzgruppen einen Namen zu. Er muss nicht eindeutig sein. Sie können auch eine optionale Beschreibung für die Tasksequenzgruppe angeben.  

> [!IMPORTANT]  
> Eine Tasksequenzgruppe kann standardmäßig nicht weiter ausgeführt werden, wenn bei einem Schritt oder einer eingebetteten Gruppe innerhalb der Gruppe ein Fehler auftritt. Wenn die Tasksequenz nach einem Fehler bei einem Schritt oder einer eingebetteten Gruppe fortgesetzt werden soll, legen Sie für den Schritt oder die Gruppe die Option **Bei Fehler fortsetzen** fest.  

In der folgenden Tabelle wird die Wirkung der Option **Bei Fehler fortsetzen** bei gruppierten Schritten veranschaulicht.  

In diesem Beispiel gibt es zwei Gruppen von Tasksequenzen, die jeweils drei Tasksequenzschritte enthalten.  

|Tasksequenzgruppe oder -schritt|Einstellung „Bei Fehler fortsetzen“|  
|---------------------------------|-------------------------------|  
|**Tasksequenzgruppe 1**|**Bei Fehler fortsetzen** ausgewählt|  
|Tasksequenzschritt 1|**Bei Fehler fortsetzen** ausgewählt|  
|Tasksequenzschritt 2|Nicht festgelegt.|  
|Tasksequenzschritt 3|Nicht festgelegt.|  
|**Tasksequenzgruppe 2**|Nicht festgelegt.|  
|Tasksequenzschritt 4|Nicht festgelegt.|  
|Tasksequenzschritt 5|Nicht festgelegt.|  
|Tasksequenzschritt 6|Nicht festgelegt.|  

- Tritt bei Tasksequenzschritt 1 ein Fehler auf, wird die Tasksequenz mit Tasksequenzschritt 2 fortgesetzt.  

- Tritt bei Tasksequenzschritt 2 ein Fehler auf, wird die Tasksequenz mit Tasksequenzschritt 3 fortgesetzt. Da Tasksequenzgruppe 1 auf **Bei Fehler fortsetzen** konfiguriert ist, fährt die Tasksequenz mit Tasksequenzgruppe 2 fort. Als Nächstes wird Tasksequenzschritt 4 ausgeführt.  

- Wenn bei Tasksequenzschritt 4 ein Fehler auftritt, werden keine weiteren Schritte ausgeführt. Bei der Tasksequenz tritt ein Fehler auf, da die Einstellung **Bei Fehler fortsetzen** nicht für Tasksequenzgruppe 2 konfiguriert ist.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Hinzufügen von untergeordneten Tasksequenzen zu einer Tasksequenz

<!--1261338-->

Fügen Sie einen neuen Tasksequenzschritt hinzu, der eine andere Tasksequenz ausführt. Dieser Schritt erstellt eine Über-/Unterordnungsbeziehung zwischen den Tasksequenzen. Dadurch können Sie modularere Tasksequenzen erstellen, die Sie wiederverwenden können.  

Weitere Informationen finden Sie unter [Ausführen einer Tasksequenz](../understand/task-sequence-steps.md#child-task-sequence).

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a> Tasksequenzvariablen  

Tasksequenzvariablen stellen eine Gruppe von Name-Wert-Paaren dar. Sie geben die Einstellungen für Konfigurations- und Betriebssystembereitstellungen für Computer-, Betriebssystem- und Benutzerzustands-Konfigurationstasks für einen Configuration Manager-Client an. Mit Tasksequenzvariablen können die Schritte in einer Tasksequenz konfiguriert und angepasst werden.  

Wenn Sie eine Tasksequenz ausführen, speichert diese viele der Tasksequenzeinstellungen als Umgebungsvariablen. Sie können auf die Werte der integrierten Tasksequenzvariablen zugreifen oder diese ändern. Sie können auch neue Tasksequenzvariablen erstellen, um die Ausführung einer Tasksequenz auf einem Zielcomputer anzupassen.  

Verwenden Sie Tasksequenzvariablen zur Durchführung der folgenden Aktionen:  

- Konfigurieren von Einstellungen für eine Tasksequenzaktion  

- Bereitstellen von Befehlszeilenargumenten für einen Tasksequenzschritt  

- Auswerten einer Bedingung, von der bestimmt wird, ob ein Tasksequenzschritt oder eine Tasksequenzgruppe ausgeführt werden soll  

- Angeben von Werten für benutzerdefinierte Skripts, die in einer Tasksequenz verwendet werden  

Beispiel: Eine Tasksequenz enthält den Tasksequenzschritt **Einer Domäne oder Arbeitsgruppe beitreten**. Stellen Sie die Tasksequenz für verschiedene Sammlungen bereit, wobei die Sammlungsmitgliedschaft durch die Domänenmitgliedschaft bestimmt wird. Geben Sie eine sammlungsspezifische Tasksequenzvariable für den Domänennamen jeder Sammlung an. Geben Sie dann anhand dieser Tasksequenzvariable den jeweiligen Domänennamen in der Tasksequenz an.  

Weitere Informationen finden Sie unter [Gewusst wie: Verwenden von Tasksequenzvariablen](../understand/using-task-sequence-variables.md).

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a> Erstellen einer Tasksequenz  

Erstellen Sie Tasksequenzen mithilfe des Tasksequenzerstellungs-Assistenten. Mit dem Assistenten können integrierte Sequenzen zur Ausführung bestimmter Tasks oder benutzerdefinierte Tasksequenzen zur Ausführung vieler verschiedener Tasks erstellt werden. Mit dem Assistenten können Sie die folgenden Typen von Tasksequenzen erstellen:

- Installieren eines vorhandenen Betriebssystemimage auf einem Zielcomputer  

- Erstellen und Erfassen eines Betriebssystemimage von einem Referenzcomputer  

- Durchführen eines Upgrades auf Windows 10 über ein Betriebssystemupgradepaket auf einem Zielcomputer

- Erstellen einer benutzerdefinierten Tasksequenz, die einen benutzerdefinierten Task oder eine spezielle Betriebssystembereitstellung ausführt  

Weitere Informationen finden Sie unter [Erstellen von Tasksequenzen](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Bearbeiten einer Tasksequenz  

Bearbeiten Sie die Tasksequenz mithilfe des **Tasksequenz-Editors**. Mit dem Editor kann die Tasksequenz wie folgt geändert werden:  

- Hinzufügen von Schritten zur Tasksequenz bzw. Entfernen von Schritten aus dieser  

- Ändern der Reihenfolge der Tasksequenzschritte  

- Hinzufügen oder Entfernen von Gruppen von Schritten  

- Angeben, ob die Tasksequenz beim Auftreten eines Fehlers fortgesetzt wird  

- Hinzufügen von Bedingungen zu den Schritten und Gruppen einer Tasksequenz  

> [!IMPORTANT]  
> Wenn die Tasksequenz nicht zugeordnete Verweise auf ein Objekt aufgrund der Bearbeitung aufweist, werden Sie vom Editor aufgefordert, den Verweis zu beheben, bevor er geschlossen werden kann. Es können folgende Aktionen durchgeführt werden:  
>
> - Korrigieren des Verweises
> - Löschen des Objekts ohne Verweis aus der Tasksequenz  
> - Vorübergehendes Deaktivieren des fehlerhaften Tasksequenzschritts, bis der fehlerhafte Verweis korrigiert oder entfernt wurde  

Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md).  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a> Bereitstellen einer Tasksequenz  

Stellen Sie eine Tasksequenz auf Zielcomputern bereit, die sich in einer beliebigen Configuration Manager-Sammlung befinden. Verwenden Sie die integrierte Sammlung **Alle unbekannten Computer**, um Betriebssysteme auf unbekannten Computern bereitzustellen. Es ist nicht möglich, eine Tasksequenz für Benutzersammlungen bereitzustellen.  

> [!IMPORTANT]  
> Stellen Sie keine Tasksequenzen bereit, mit denen Betriebssysteme in ungeeigneten Sammlungen installiert werden. Achten Sie darauf, dass die Sammlung, für die Sie die Tasksequenz bereitstellen, nur die Computer enthält, auf denen das Betriebssystem installiert werden soll. Um unerwünschte Betriebssystembereitstellungen zu vermeiden, konfigurieren Sie die Einstellungen für Bereitstellungen mit hohem Risiko. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Die Tasksequenz wird von jedem Zielcomputer, der die Tasksequenz erhält, den in der Bereitstellung angegebenen Einstellungen entsprechend ausgeführt. Die Tasksequenzen selbst enthalten keine zugeordneten Dateien oder Programme. Alle Dateien, auf die von einer Tasksequenz verwiesen wird, müssen sich bereits auf dem Zielcomputer oder auf einem Verteilungspunkt befinden, die für Clients zugänglich sind.

> [!NOTE]  
> Die Tasksequenz installiert Pakete, auf die von Programmen verwiesen wird, selbst wenn das Programm oder Paket bereits auf dem Zielcomputer installiert ist.
>
> Wenn von der Tasksequenz eine Anwendung installiert wird, wird die Anwendung nur installiert, wenn die Anforderungsregeln für die Anwendung erfüllt sind und die Anwendung nicht bereits installiert ist. Ob dies der Fall ist, wird von der Erkennungsmethode festgestellt, die für die Anwendung angegeben wurde.  

Der Configuration Manager-Client führt beim Herunterladen einer Clientrichtlinie eine Tasksequenzbereitstellung aus. Informationen zum Auslösen dieser Aktion, anstatt auf den nächsten Abrufzyklus zu warten, finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

Sie können beim Bereitstellen von Tasksequenzen für Windows Embedded-Geräte mit einem aktivierten Schreibfilter angeben, ob der Schreibfilter auf dem Gerät während der Bereitstellung deaktiviert und das Gerät nach der Bereitstellung neu gestartet werden soll. Wenn der Schreibfilter nicht deaktiviert ist, wird die Tasksequenz in einem temporären Overlay bereitgestellt und ist nach dem Neustart des Geräts nicht verfügbar.  

> [!NOTE]  
> Stellen Sie beim Bereitstellen einer Tasksequenz auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist. So können Sie verwalten, wann der Schreibfilter deaktiviert bzw. aktiviert ist und wann das Gerät neu gestartet wird.  
>
> Wenn Tasksequenzen von Clients außerhalb eines Wartungsfensters heruntergeladen werden, wird die Tasksequenz zweimal heruntergeladen. In diesem Szenario lädt der Client die Tasksequenz herunter, deaktiviert den Schreibfilter, startet den Computer neu und lädt die Tasksequenz dann erneut herunter. Dieses Verhalten ist darauf zurückzuführen, dass die Tasksequenz ursprünglich in das temporäre Overlay heruntergeladen wurde, das beim Neustart des Geräts gelöscht wird.  

Weitere Informationen zum Bereitstellen von Tasksequenzen finden Sie unter [Bereitstellen einer Tasksequenz](../deploy-use/deploy-a-task-sequence.md).  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a> Exportieren und Importieren

Configuration Manager erlaubt das Exportieren und Importieren von Tasksequenzen. Wenn Sie eine Tasksequenz exportieren, können Sie die Objekte einschließen, auf die von der Tasksequenz verwiesen wird.

Weitere Informationen finden Sie unter [Exportieren und Importieren von Tasksequenzen](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Ausführen einer Tasksequenz  

Tanksequenzen werden stets über das lokale Systemkonto ausgeführt. Beim Ausführen der Tasksequenz sucht der Configuration Manager-Client zunächst nach referenzierten Paketen, bevor die Schritte der Tasksequenz gestartet werden. Wenn er ein referenziertes Paket nicht überprüfen oder herunterladen kann, gibt die Tasksequenz für den zugehörigen Tasksequenzschritt einen Fehler zurück.  

> [!Note]  
> Mithilfe des Tasksequenzschritts **Befehlszeile ausführen** kann ein Befehl unter einem anderen Konto ausgeführt werden.  

Wenn Sie eine Tasksequenzbereitstellung zum Herunterladen und Ausführen konfigurieren, lädt der Configuration Manager-Client alle abhängigen Inhalte in den jeweiligen Cache herunter. Wenn der Clientcache zu klein ist oder der Inhalt nicht gefunden werden kann, tritt bei der Tasksequenz ein Fehler auf. Der Client generiert eine Statusmeldung.

Sie können auch angeben, dass der Client den Inhalt nur herunterlädt, wenn dies erforderlich ist. Wählen Sie hierfür in der Tasksequenzbereitstellung **Inhalt lokal herunterladen, wenn dies für die Ausführung der Tasksequenz erforderlich ist** aus. Alternativ können Sie die Option **Programm vom Verteilungspunkt ausführen** auswählen. Bei dieser Option installiert der Client die Dateien direkt vom Verteilungspunkt aus, ohne sie zuerst in den Cache herunterzuladen.

Wenn Sie die Tasksequenzbereitstellung als **Verfügbar** konfigurieren und der Client keinen abhängigen Inhalt für die Tasksequenz finden kann, sendet er sofort einen Fehler. Bei einer Bereitstellung mit dem Status **Erforderlich** würde der Configuration Manager-Client in diesem Fall warten. Er versucht erneut, den Inhalt bis zum Stichtag herunterzuladen, für den Fall, dass der Inhalt noch nicht zu einem Inhaltsort repliziert wurde, auf den der Client zugreifen kann.  

Nachdem eine Tasksequenz erfolgreich abgeschlossen oder fehlerhaft beendet wurde, wird dieser Zustand von Configuration Manager entsprechend im Clientverlauf protokolliert.

Sobald eine Tasksequenz auf einem Computer gestartet wurde, kann sie nicht mehr abgebrochen oder beendet werden.  

> [!IMPORTANT]  
> Falls für einen Schritt der Tasksequenz ein Neustart des Computers erforderlich ist, muss für den Client das Starten über eine formatierte Festplattenpartition möglich sein. Andernfalls tritt für die Tasksequenz unabhängig davon ein Fehler auf, ob eine von Ihnen angegebene Fehlerbehandlung in der Tasksequenz vorhanden ist.  

Wenn ein abhängiges Objekt einer Tasksequenz auf eine neuere Version aktualisiert wird, werden auch alle Tasksequenzen, die auf das Paket verweisen, automatisch aktualisiert. Es verweist auf die neueste Version, unabhängig davon, wie viele Updates Sie bereitgestellt haben.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a> Verwenden von Wartungsfenstern

Sie können den Zeitpunkt der Ausführung einer Tasksequenz angeben, indem Sie ein Wartungsfenster für die Gerätesammlung definieren. Sie konfigurieren Wartungsfenster mit einem Startdatum, einer Start- und Endzeit sowie einem Wiederholungsmuster. Beim Festlegen des Zeitplans für das Wartungsfenster können Sie angeben, dass das Wartungsfenster nur für Tasksequenzen gelten soll. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
> Wenn Sie ein Wartungsfenster zum Ausführen einer Tasksequenz konfigurieren, wird die Tasksequenz auch nach dem Schließen des Wartungsfensters weiter ausgeführt.  

Wenn ein Gerät mehr als ein Wartungsfenster anwendet, ignoriert der Client möglicherweise das Wartungsfenster **Alle Bereitstellungen**. Ab Version 1810 verwenden Sie die folgende Clienteinstellung, um dieses Verhalten zu steuern: **Installation von Softwareupdates im Wartungsfenster „Alle Bereitstellungen“ aktivieren, wenn das Wartungsfenster „Softwareupdate“ verfügbar ist**. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a> Tasksequenzen und das Netzwerkzugriffskonto  

> [!Important]  
> Die Verwendung eines Netzwerkzugriffskontos für einige Betriebssystembereitstellungsszenarios ist nicht mehr erforderlich. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](#enhanced-http).

Obwohl Tasksequenzen im Kontext des lokalen Systemkontos ausgeführt werden, müssen Sie das [Netzwerkzugriffskonto](../../core/plan-design/hierarchy/accounts.md#network-access-account) in folgenden Situationen möglicherweise konfigurieren:  

- Wenn die Tasksequenz versucht, auf Configuration Manager-Inhalte auf Verteilungspunkten zuzugreifen. Konfigurieren Sie das Netzwerkzugriffskonto entsprechend, da anderenfalls ein Fehler bei der Tasksequenz auftritt.

- Wenn Sie ein Startimage verwenden, um eine Betriebssystembereitstellung zu initiieren. In diesem Fall verwendet Configuration Manager die Windows PE-Umgebung, bei der es sich nicht um ein vollständiges Betriebssystem handelt. Die Windows PE-Umgebung verwendet einen automatisch generierten zufälligen Namen, der keiner Domäne angehört. Wenn Sie das Netzwerkzugriffskonto nicht ordnungsgemäß konfigurieren, kann der Computer nicht auf die für die Tasksequenz erforderlichen Inhalte zugreifen.  

> [!NOTE]  
> Das Netzwerkzugriffskonto wird nie als Sicherheitskontext für die Ausführung von Programmen, die Installation von Anwendungen oder Updates oder die Ausführung von Tasksequenzen verwendet. Das Netzwerkzugriffskonto wird nur für den Zugriff auf die zugeordneten Ressourcen im Netzwerk verwendet.  

Weitere Informationen zum Netzwerkzugriffskonto finden Sie unter [Netzwerkzugriffskonto](../../core/plan-design/hierarchy/accounts.md#network-access-account).  

### <a name="enhanced-http"></a>Erweitertes HTTP
<!--1358278-->

Wenn Sie **Erweitertes HTTP** aktivieren, ist für die folgenden Szenarios kein Netzwerkzugriffskonto erforderlich, um Inhalt von einem Verteilungspunkt herunterzuladen:

- Tasksequenzen, die über ein Bootmedium oder über PXE ausgeführt werden  
- Tasksequenzen, die über das Softwarecenter ausgeführt werden  

Diese Tasksequenzen können für die Betriebssystembereitstellung oder benutzerdefinierte Bereitstellung verwendet werden. Sie werden auch von Arbeitsgruppencomputern unterstützt.

Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../../core/plan-design/hierarchy/enhanced-http.md).  

> [!Note]  
> Für die folgenden Betriebssystembereitstellungsszenarios ist die Verwendung eines Netzwerkzugriffskontos weiterhin erforderlich:
>  
> - Die Option zum [Bereitstellen einer Tasksequenz](../deploy-use/deploy-a-task-sequence.md): **Auf Inhalt bei Bedarf direkt von einem Verteilungspunkt aus zugreifen, wenn dies für die Ausführung der Tasksequenz erforderlich ist**
> - Die Schrittoption [Zustandsspeicher anfordern](../understand/task-sequence-steps.md#BKMK_RequestStateStore): **Das Netzwerkzugriffskonto verwenden, wenn das Computerkonto keine Verbindung mit dem Zustandsspeicher hergestellt werden kann**
> - Beim Herstellen einer Verbindung mit einer nicht vertrauenswürdigen Domäne oder zwischen Active Directory-Gesamtstrukturen
> - Die Schrittoption [Betriebssystemimage anwenden](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage): **Auf Inhalt direkt vom Verteilungspunkt aus zugreifen**
> - Die [erweiterte Einstellung](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) für eine Tasksequenz: **Ein anderes Programm zuerst ausführen**
> - [Multicast](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a> Erstellen von Medien

Sie können Tasksequenzen und die damit verbundene Dateien und Abhängigkeiten auf verschiedene Medientypen schreiben. Configuration Manager unterstützt Wechselmedien wie DVDs, USB-Speichersticks für die Erfassung und eigenständige sowie startbare Medien. Vorab bereitgestellte Medien verwenden Windows-Imagedateien (WIM).  

Geben Sie bei der Erstellung von Medien ein Kennwort ein, um den Zugriff zu steuern. Eine Person muss dann auf dem Zielcomputer das Kennwort eingeben, um die Tasksequenz ausführen zu können.  

Wenn Sie eine Tasksequenz von einem Medium ausführen, wird die angegebene Prozessorarchitektur des Mediums nicht erkannt. Wenn die angegebene Architektur nicht der des Zielcomputers entspricht, versucht die Tasksequenz dennoch, sie auszuführen. Wenn die Architektur des Mediums nicht der des Zielcomputers entspricht, verursacht die Tasksequenz einen Fehler.  

Weitere Informationen finden Sie unter [Erstellen von Tasksequenzmedien](../deploy-use/create-task-sequence-media.md).  

### <a name="media-types"></a>Medientypen

Configuration Manager unterstützt die folgenden Typen von Medien:  

#### <a name="capture-media"></a>Erfassungsmedien

Mithilfe von Erfassungsmedien wird ein Betriebssystemimage erfasst, das Sie außerhalb der Configuration Manager-Infrastruktur konfigurieren und erstellen. Erfassungsmedien können benutzerdefinierte Programme enthalten, die vor einer Tasksequenz ausgeführt werden können. Vom benutzerdefinierten Programm kann mit dem Desktop interagiert werden. Benutzer können zur Werteingabe aufgefordert werden, und die von der Tasksequenz verwendeten Variablen können erstellt werden.  

Weitere Informationen finden Sie unter [Erstellen von Erfassungsmedien](../deploy-use/create-capture-media.md).  

#### <a name="stand-alone-media"></a>Eigenständige Medien

Eigenständige Medien enthalten die Tasksequenz und alle zugeordneten Objekte, die für die Ausführung der Tasksequenz erforderlich sind. Tasksequenzen auf eigenständigen Medien können ausgeführt werden, wenn Configuration Manager keine oder nur begrenzte Verbindungen mit dem Netzwerk aufweist. Führen Sie eigenständige Medien auf folgende Arten aus:  

- Wenn der Zielcomputer nicht gestartet ist, wird das der Tasksequenz zugeordnete Windows PE-Image vom eigenständigen Medium aus verwendet und die Tasksequenz wird gestartet.  

- Starten Sie das eigenständige Medium manuell. Wenn ein Benutzer auf dem Computer angemeldet ist, können sie die Tasksequenz über das Medium initiieren.  

> [!IMPORTANT]  
> Die Schritte einer Tasksequenz für eigenständige Medien müssen ausgeführt werden können, ohne dass Daten aus dem Netzwerk abgerufen werden müssen. Anderenfalls tritt beim Tasksequenzschritt, der die Daten abruft, ein Fehler auf. Dies ist beispielsweise bei einem Tasksequenzschritt der Fall, der einen Verteilungspunkt zum Abrufen eines Pakets benötigt. Wenn das eigenständige Medium das erforderliche Paket enthält, wird der Tasksequenzschritt erfolgreich ausgeführt.  

Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](../deploy-use/create-stand-alone-media.md).  

#### <a name="bootable-media"></a>Startbare Medien

Startbare Medien enthalten die zum Starten eines Zielcomputers erforderlichen Dateien, sodass der Zielcomputer eine Verbindung mit der Configuration Manager-Infrastruktur herstellen kann. Anschließend wird auf Grundlage seiner Sammlungsmitgliedschaften bestimmt, welche Tasksequenzen auszuführen sind. Das Medium enthält nicht die Tasksequenz oder abhängige Objekte. Stattdessen lädt der Client den Inhalt über das Netzwerk herunter. Diese Methode empfiehlt sich bei Bereitstellungen auf neuen Computern oder Bare-Metal-Computern, auf denen kein Betriebssystem auf dem Zielcomputer installiert ist.  

Weitere Informationen finden Sie unter [Erstellen startbarer Medien](../deploy-use/create-bootable-media.md).  

#### <a name="prestaged-media"></a>Vorab bereitgestellte Medien

Mithilfe des vorab bereitgestellten Mediums wird ein Betriebssystemimage auf einem nicht bereitgestellten Zielcomputer bereitgestellt. Das vorab bereitgestellte Medium wird als Windows-Imagedatei (WIM) gespeichert. Diese Datei kann vom Hersteller oder im Stagingzentrum eines Unternehmens auf einem Bare-Metal-Computer installiert werden. Ein Vorteil von vorab bereitgestellten Medien ist, dass diese Medien keine Verbindung mit Ihrer Configuration Manager-Umgebung herstellen müssen.  

Weitere Informationen finden Sie unter [Erstellen vorab bereitgestellter Medien](../deploy-use/create-prestaged-media.md).  

## <a name="next-steps"></a>Nächste Schritte

- [Sicherheit und Datenschutz für die Betriebssystembereitstellung](security-and-privacy-for-operating-system-deployment.md)

- [Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
