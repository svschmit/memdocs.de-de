---
title: Überwachen von Inhalt
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zur Überwachung von verteiltem Inhalt mithilfe der Configuration Manager-Konsole.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110014"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Überwachen von Inhalten, die Sie mit Configuration Manager verteilen

*Gilt für: Configuration Manager (Current Branch)*

Mit der Configuration Manager-Konsole können Sie unter anderem die folgenden verteilten Inhalte überwachen:  

- Den Status aller Pakettypen für die zugeordneten Verteilungspunkte.  
- Den Inhaltsprüfungsstatus des Paketinhalts.  
- Den Status von Inhalt, der einer bestimmten Verteilungspunktgruppe zugeordnet ist.  
- Den Zustand von Inhalt, der einem Verteilungspunkt zugeordnet ist.  
- Den Status optionaler Features jedes Verteilungspunkts (Inhaltsprüfung, PXE und Multicast).  

> [!NOTE]  
> Von Configuration Manager wird nur der Inhalt auf einem Verteilungspunkt überwacht, der sich in der Inhaltsbibliothek befindet. Inhalt, der auf dem Verteilungspunkt in Paketfreigaben oder benutzerdefinierten Freigaben gespeichert ist, wird nicht überwacht.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Überwachung des Inhaltsstatus

Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Inhaltsstatus** Informationen zu Inhaltspaketen. In der Configuration Manager-Konsole können Sie z. B. folgende Informationen überprüfen:  

- Paketname, -typ und -ID
- An wie viele Verteilungspunkte ein Paket gesendet wurde
- Kompatibilitätsrate
- Wann das Paket erstellt wurde
- Quellversion

Zudem finden Sie dort für jedes Paket detaillierte Statusinformationen. Beispiele:  

- Verteilungsstatus
- Fehleranzahl
- Ausstehende Verteilungen  
- Anzahl der Installationen

Sie können außerdem Verteilungen an einen Verteilungspunkt verwalten, die noch in Bearbeitung sind bzw. aufgrund von Fehlern nicht erfolgreich ausgeführt werden konnten:  

- Die Option zum Abbrechen oder erneuten Verteilen des Inhalts ist verfügbar, wenn Sie im Fensterbereich **Bestandsdetails** die Bereitstellungsstatusmeldung zu einem Verteilungsauftrag an einen Verteilungspunkt anzeigen. Diesen Bereich finden Sie entweder auf der Registerkarte **In Bearbeitung** oder auf der Registerkarte **Fehler** des Knotens **Inhaltsstatus**.  
- Darüber hinaus wird in den Auftragsdetails der Prozentsatz des Auftrags angezeigt, der beim Anzeigen der Details eines Auftrags auf der Registerkarte **In Bearbeitung** abgeschlossen wurde. In den Auftragsdetails wird auch die Anzahl der Wiederholungsversuche angezeigt, die für einen Auftrag verbleiben. Wenn Sie die Details zu einem Auftrag auf der Registerkarte **Fehler** überprüfen, wird die Zeit bis zum nächsten Wiederholungsversuch angezeigt.  

Beim Abbrechen einer Bereitstellung, die noch nicht abgeschlossen ist, wird der Verteilungsauftrag zur Übertragung des betreffenden Inhalts beendet:  

- Der Status der Bereitstellung wird dann aktualisiert, um anzuzeigen, dass die Verteilung nicht durchgeführt werden konnte und von einer Benutzeraktion abgebrochen wurde.  
- Dieser neue Status wird auf der Registerkarte **Fehler** angezeigt.  

> [!NOTE]  
> Wenn eine Bereitstellung fast abgeschlossen ist, kann ein Befehl zum Abbrechen der Verteilung möglicherweise nicht rechtzeitig vor Abschluss der Verteilung an den Verteilungspunkt verarbeitet werden. In diesem Fall wird der Abbruch der Bereitstellung ignoriert, und der Status der Bereitstellung wird als erfolgreich angezeigt.  
>
> Zwar können Sie die Option zum Abbrechen einer Verteilung an einen Verteilungspunkt auf einem Standortserver auswählen, aber diese Auswahl ist unwirksam. Dieses Verhalten liegt daran, dass der Standortserver und der Verteilungspunkt auf einem Standortserver den gleichen Single Instance Content Store verwenden. Es gibt keinen tatsächlichen Verteilungsauftrag, der abgebrochen werden könnte.  

Beim erneuten Verteilen von Inhalt an einen Verteilungspunkt, bei dessen Übertragung zuvor ein Fehler auftrat, beginnt der Configuration Manager sofort mit der erneuten Bereitstellung des Inhalts an den Verteilungspunkt. Der Status der Bereitstellung wird entsprechend aktualisiert, um den laufenden Stand der erneuten Bereitstellung widerzuspiegeln.  

### <a name="tasks-to-monitor-content"></a>Tasks zum Überwachen von Inhalten

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie **Verteilungsstatus**, und wählen Sie den Knoten **Inhaltsstatus** aus. In diesem Knoten werden die Pakete angezeigt.  

2. Wählen Sie das zu verwaltende Paket aus.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Inhalt** die Option **Status anzeigen** aus. In der Konsole werden detaillierte Statusinformationen zum Paket angezeigt.

Fahren Sie mit einem der folgenden Abschnitte fort, um weitere Aktionen durchzuführen:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Abbrechen einer Verteilung, die noch in Bearbeitung ist  

1. Wechseln Sie zur Registerkarte **In Bearbeitung**.

2. Klicken Sie im Bereich **Bestandsdetails** mit der rechten Maustaste auf den Eintrag für die abzubrechende Verteilung, und wählen Sie **Abbrechen** aus.  

3. Klicken Sie auf **Ja**, um den Vorgang zu bestätigen und den Verteilungsauftrag an den betreffenden Verteilungspunkt abzubrechen.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Erneutes Verteilen von Inhalt, dessen Verteilung aufgrund von Fehlern nicht abgeschlossen werden konnte  

1. Wechseln Sie zur Registerkarte **Fehler**.

2. Klicken Sie im Bereich **Bestandsdetails** mit der rechten Maustaste auf den Eintrag für die Verteilung, die neu verteilt werden soll, und wählen Sie **Neu verteilen** aus.  

3. Klicken Sie auf **Ja**, um die Aktion zu bestätigen und den erneuten Verteilungsvorgang an den betreffenden Verteilungspunkt zu starten.  


## <a name="distribution-point-group-status"></a>Status der Verteilungspunktgruppe

Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktgruppe** Informationen zu Verteilungspunktgruppen. Sie können z. B. folgende Informationen überprüfen:  

- Name, Beschreibung und Status der Verteilungspunktgruppe
- Wie viele Verteilungspunkte zur Verteilungspunktgruppe gehören
- Wie viele Pakete der Gruppe zugewiesen wurden
- Die Kompatibilitätsrate

Zudem können Sie die folgenden detaillierten Statusinformationen überprüfen:  

- Fehler für die Verteilungspunktgruppe  
- Wie viele Verteilungen aktuell in Bearbeitung sind
- Wie viele erfolgreich verteilt wurde  

### <a name="monitor-distribution-point-group-status"></a>Überwachen des Status einer Verteilungspunktgruppe  

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie **Verteilungsstatus**, und wählen Sie den Knoten **Status der Verteilungspunktgruppe** aus. Die Verteilungspunktgruppen werden angezeigt.  

2. Wählen Sie die Verteilungspunktgruppe aus, für die detaillierte Statusinformationen angezeigt werden sollen.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands die Option **Status anzeigen** aus. Detaillierte Statusinformationen für die Verteilungspunktgruppe werden angezeigt.  


## <a name="distribution-point-configuration-status"></a>Status der Verteilungspunktkonfiguration

Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktkonfiguration** Informationen zum Verteilungspunkt. Sie können prüfen, welche Attribute für den Verteilungspunkt aktiviert sind, z. B. PXE, Multicast und Inhaltsprüfung. Überprüfen Sie außerdem den Verteilungsstatus des Verteilungspunkts.

> [!WARNING]  
> Der Status der Verteilungspunktkonfiguration bezieht sich auf die letzten 24 Stunden. Wenn der Verteilungspunkt nach einem Fehler wiederhergestellt wird, wird der Fehlerstatus möglicherweise bis zu 24 Stunden nach der Wiederherstellung des Verteilungspunkts angezeigt.  

### <a name="monitor-distribution-point-configuration-status"></a>Überwachen des Status einer Verteilungspunktkonfiguration  

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie **Verteilungsstatus**, und wählen Sie den Knoten **Status der Verteilungspunktkonfiguration** aus.  

2. Wählen Sie einen Verteilungspunkt aus.  

3. Wechseln Sie im Ergebnisbereich zur Registerkarte **Details**. Dort werden Statusinformationen zum Verteilungspunkt angezeigt.  


## <a name="client-data-sources-dashboard"></a>Dashboard „Clientdatenquellen“

Erlangen Sie anhand des Dashboards **Clientdatenquellen** ein besseres Verständnis darüber, woher Clients in Ihrer Umgebung Inhalte abrufen. Das Dashboard zeigt Daten an, nachdem Clients Inhalte heruntergeladen haben und diese Informationen dem Standort gemeldet wurden. Dieser Vorgang kann bis zu 24 Stunden dauern.

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen das **Clientpeercache**-Feature aktivieren, bevor Sie es verwenden können. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../manage/install-in-console-updates.md#bkmk_options).  

Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie **Verteilungsstatus**, und wählen Sie den Knoten **Clientdatenquellen** aus. Wählen Sie einen Zeitraum aus, der auf das Dashboard angewendet werden soll. Wählen Sie anschließend die Begrenzungsgruppe aus, für die Informationen angezeigt werden sollen. Sie können Ihre Maus über Kacheln bewegen, um weitere Details zu den verschiedenen Inhalts- oder Richtlinienquellen zu erhalten.

Verwenden Sie auch den Bericht **Clientdatenquellen – Zusammenfassung**, um eine Zusammenfassung der Clientdatenquellen für die einzelnen Begrenzungsgruppen anzuzeigen.

### <a name="dashboard-tiles"></a>Dashboardkacheln

Das Dashboard umfasst die folgenden Kacheln:  

#### <a name="client-content-sources"></a>Quellen für Clientinhalte

Hier werden die Quellen angezeigt, von denen Clients Inhalte beziehen:

- Verteilungspunkt
- [Cloudverteilungspunkte](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Peercache](../../../plan-design/hierarchy/client-peer-cache.md)
- [Übermittlungsoptimierung](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (ab Version 1906)<sup>[Hinweis 1](#bkmk_note1)</sup>
- Microsoft Update: Geräte melden diese Quelle, wenn der Configuration Manager-Client Softwareupdates von Microsoft-Clouddiensten herunterlädt. Zu diesen Diensten gehören Microsoft Update und Microsoft 365 Apps for Enterprise.

![Kachel „Quellen für Clientinhalte“ auf dem Dashboard](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Ab Version 1906<!--3555759-->führen Sie zum Einschließen der Übermittlungsoptimierung in dieses Dashboard die folgenden Aktionen aus:
>
> - Konfigurieren Sie in der Gruppe „Softwareupdates“ die Clienteinstellung **Enable installation of Express Updates on clients** (Installation von Express-Updates auf Clients aktivieren).
>
> - Bereitstellen von Windows 10-Express-Updates
>
> Weitere Informationen finden Sie unter [Verwalten von Expressinstallationsdateien für Windows 10-Updates](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Verteilungspunkte

Zeigt die Anzahl der Verteilungspunkte an, die zur ausgewählten Begrenzungsgruppe gehören.

#### <a name="clients-that-used-a-distribution-point"></a>Clients, die einen Verteilungspunkt verwendet haben

In dieser Kachel wird angezeigt, wie viele Clients in der ausgewählten Begrenzungsgruppe über einen Verteilungspunkt Inhalte abgerufen haben.

#### <a name="peer-cache-sources"></a>Peercachequellen

In dieser Kachel wird für die ausgewählte Begrenzungsgruppe angezeigt, von wie vielen Peercachequellen ein Downloadverlauf gemeldet wurde.

#### <a name="clients-that-used-a-peer"></a>Clients, die einen Peer verwendet haben

In dieser Kachel wird angezeigt, wie viele Clients in der ausgewählten Begrenzungsgruppe zum Abrufen von Inhalten eine Peercachequelle verwendet haben.

#### <a name="top-distributed-content"></a>Top-Inhalte zur Verteilung

Die am häufigsten verteilten Pakete nach Quelltyp
