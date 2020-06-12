---
title: Referenz für Wartungstasks
titleSuffix: Configuration Manager
description: Details zu den einzelnen Standortwartungstasks für den Configuration Manager
ms.date: 06/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e989de5acab778374c233862d0ab4d7077899d28
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428590"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Referenz für Wartungstasks im Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden Details zu den einzelnen Standortwartungstasks für den Configuration Manager aufgelistet. Jeder Eintrag gibt die Standorttypen an, für die der Task verfügbar ist, und ob er standardmäßig aktiviert ist.

Weitere Informationen finden Sie unter [Benutzerdefinierte Wartungstasks einrichten](maintenance-tasks.md#set-up-maintenance-tasks).  

## <a name="tasks"></a>Tasks

### <a name="backup-site-server"></a>Standortserver sichern

Erstellen Sie mit diesem Task eine Sicherung Ihrer wichtigen Informationen, um einen Standort und die Configuration Manager-Datenbank wiederherzustellen. Weitere Informationen finden Sie unter [Sichern eines Configuration Manager-Standorts](backup-and-recovery.md).  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Nicht aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="check-application-title-with-inventory-information"></a>Anwendungstitel mit Inventurinformationen prüfen

Verwenden Sie diesen Task, um die Konsistenz zwischen Softwaretiteln in der Softwareinventur und im Asset Intelligence-Katalog zu gewährleisten. Weitere Informationen finden Sie unter [Einführung in Asset Intelligence in Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|Primärer Standort|Nicht verfügbar|
|Sekundärer Standort|Nicht verfügbar|

### <a name="clear-undiscovered-clients"></a>Nicht entdeckte Clients löschen

> [!Tip]
> Dieser Task wird möglicherweise auch in der Konsole mit dem Namen **Installationsflag löschen** angezeigt.

Verwenden Sie diesen Task, um das Installationsflag für Clients zu entfernen, die während des **Clientneuermittlungs-Zeitraums** keinen von der Frequenzermittlung erstellten Datensatz übermitteln. Durch das Installationsflag wird die automatische Clientpushinstallation auf einen Computer verhindert, auf dem ein aktiver Configuration Manager-Client vorhanden ist.  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Nicht aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-application-request-data"></a>Veraltete Anwendungsanforderungsdaten löschen

Verwenden Sie diesen Task, um veraltete Anwendungsanforderungen aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [Create and deploy an application with System Center Configuration Manager (Erstellen und Bereitstellen einer Anwendung mit System Center Configuration Manager)](../../../apps/get-started/create-and-deploy-an-application.md).  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-application-revisions"></a>Veraltete Anwendungsrevisionen löschen

Verwenden Sie diesen Task, um Anwendungsrevisionen zu löschen, die nicht mehr referenziert werden. Weitere Informationen finden Sie unter [Überarbeiten und Ablösen von Anwendungen in System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md).

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-client-download-history"></a>Veralteten Clientdownloadverlauf löschen

Verwenden Sie diesen Task, um Verlaufsdaten über die von Clients verwendete Downloadquelle zu löschen. Dieser Standort verwendet Downloadquelleninformationen zum Auffüllen des [Dashboards „Clientdatenquellen“](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-client-operations"></a>Veraltete Clientvorgänge löschen

Verwenden Sie diesen Task, um alle veralteten Daten für Clientvorgänge aus der Standortdatenbank zu löschen. Diese Daten umfassen beispielsweise die folgenden Vorgänge:

- Veraltete oder abgelaufene Clientbenachrichtigungen wie z. B. Downloadanforderungen für Computer- oder Benutzerrichtlinien
- Endpoint Protection wie Anforderungen zum Ausführen von Überprüfungen oder Herunterladen aktualisierter Definitionen, die ein Administrator für Clients übermittelt hat.
- Skripts ausführen, Statusergebnisse

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-client-presence-history"></a>Veralteten Anwesenheitsverlauf für Clients löschen
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Verwenden Sie diesen Task zum Löschen veralteter Verlaufsdaten über den Onlinestatus von Clients, die von der Clientbenachrichtigung erfasst wurden. Er löscht Informationen über Clients, deren Status älter als der angegebene Zeitraum ist. Weitere Informationen finden Sie unter [Überwachen von Clients in Configuration Manager](../../clients/manage/monitor-clients.md).

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Veraltete Daten zum Cloudverwaltungsgateway-Datenverkehr löschen

Verwenden Sie diesen Task, um alle veralteten Daten über den Datenverkehr aus der Standortdatenbank zu löschen, die das [Cloudverwaltungsgateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) aus der Standortdatenbank durchlaufen. Diese Daten umfassen Folgendes:

- Die Anzahl der Anforderungen
- Gesamte Anforderungsbytes
- Gesamte Antwortbytes
- Anzahl der Anforderungen mit Fehlern
- Maximale Anzahl gleichzeitiger Anforderungen

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-cmpivot-results"></a>Veraltete CMPivot-Ergebnisse löschen

Verwenden Sie diesen Task, um veraltete Informationen über Clients in CMPivot-Abfragen aus der Standortdatenbank zu löschen. Weitere Informationen finden Sie unter [CMPivot for real-time data (CMPivot für Echtzeitdaten)](cmpivot.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-collected-files"></a>Veraltete gesammelte Dateien löschen

Verwenden Sie diesen Task, um veraltete Informationen zu gesammelten Dateien aus der Datenbank zu löschen. Mit diesem Task werden darüber hinaus die gesammelten Dateien aus der Ordnerstruktur des Standortservers auf dem ausgewählten Standort gelöscht. Standardmäßig werden die fünf neuesten Kopien der gesammelten Dateien auf dem Standortserver im Verzeichnis **Inboxes\sinv.box\FileCol** gespeichert. Weitere Informationen finden Sie unter [Einführung in die Softwareinventur](../../clients/manage/inventory/introduction-to-software-inventory.md).  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-computer-association-data"></a>Veraltete Computerzuordnungsdaten löschen

Verwenden Sie diesen Task, um veraltete Computerzuordnungsdaten für die Bereitstellung von Betriebssystemen aus der Datenbank zu löschen. Diese Informationen werden verwendet, wenn der Benutzerstatus während einer Tasksequenz wiederhergestellt wird. Weitere Informationen finden Sie unter [Verwalten des Benutzerstatus](../../../osd/get-started/manage-user-state.md).  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-console-connection-data"></a>Veraltete Konsolenverbindungsdaten löschen

Mit diesem Task werden Daten über Konsolenverbindungen mit dem Standort aus der Standortdatenbank gelöscht.<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-delete-detection-data"></a>Veraltete Erkennungsdaten von Löschvorgängen löschen

Verwenden Sie diesen Task, um veraltete Daten aus der Datenbank zu löschen, die mithilfe von Extraktionsansichten erstellt wurden. Er löscht alte Datenänderungsinformationen, die von externen Systemen zum Extrahieren von Daten aus der Datenbank verwendet werden.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-device-wipe-record"></a>Veralteten Datensatz für Zurücksetzen von Geräten löschen

Verwenden Sie diesen Task, um veraltete Daten zu Zurücksetzungsaktionen für mobile Geräte aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [Schützen von Daten durch Remotezurücksetzen, Sperren oder Zurücksetzen der Kennung](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-discovery-data"></a>Veraltete Ermittlungsdaten löschen

Verwenden Sie diesen Task, um veraltete Ermittlungsdaten aus der Datenbank zu löschen. Diese Daten können Datensätze enthalten aus:

- Taktermittlung
- Netzwerkermittlung
- Active Directory-Ermittlungsmethoden: System, Benutzer und Gruppe

Über diesen Task werden außerdem veraltete Geräte mit „Außer Betrieb“ markiert. Bei Ausführung dieses Tasks an einem Standort werden mit diesem Standort verknüpfte Daten gelöscht. Die Änderungen werden anschließend an andere Standort repliziert. Weitere Informationen finden Sie unter [Run discovery (Ausführen der Ermittlung)](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-distribution-point-usage-stats"></a>Löschen veralteter Daten zur Verteilungspunktverwendung

Verwenden Sie diesen Task, um veraltete Daten für Verteilungspunkte aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist.  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-enrolled-devices"></a>Veraltete angemeldete Geräte löschen

Löschen Sie mit diesem Task veraltete Daten zu mobilen Geräten aus der Datenbank, die über einen bestimmten Zeitraum keine Informationen an den Standort übermittelt haben.

Dieser Task gilt für Geräte, die bei der [lokalen MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) von Configuration Manager registriert sind. Weitere Informationen zu diesen Geräten finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Nicht aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-ep-health-status-history-data"></a>Veraltete Verlaufsdaten zum Endpoint Protection-Integritätsstatus löschen

Verwenden Sie diesen Task, um veraltete Statusinformationen für Endpoint Protection (EP) aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [How to monitor Endpoint Protection Status (Überwachen des Endpoint Protection-Status)](../../../protect/deploy-use/monitor-endpoint-protection.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-exchange-partnership"></a>Veraltete Exchange-Partnerschaft löschen

> [!Tip]
> > Dieser Task wird möglicherweise auch in der Konsole mit dem Namen **Veraltete mithilfe von Exchange Server Connector verwaltete Geräte löschen** angezeigt.

Verwenden Sie diesen Task, um veraltete Daten über mobile Geräte zu löschen, die vom Exchange Server-Connector verwaltet werden. Der Standort löscht diese Daten gemäß der Einstellung **Anzahl der Tage der Inaktivität, nach der mobile Geräte ignoriert werden** auf der Registerkarte **Ermittlung** der Eigenschaften für den Exchange Server-Connector. Weitere Informationen finden Sie unter [Verwalten von Mobilgeräten mit System Center Configuration Manager und Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-inventory-history"></a>Veralteten Inventurverlauf löschen

Verwenden Sie diesen Task, um Inventurdaten aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Weitere Informationen finden Sie unter [Anzeigen der Hardwareinventur mit dem Ressourcen-Explorer](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-log-data"></a>Veraltete Protokolldaten löschen

Verwenden Sie diesen Task, um veraltete für die Problembehandlung verwendete Protokolldaten aus der Datenbank zu löschen. Diese Daten stehen nicht im Zusammenhang mit Configuration Manager-Komponentenvorgängen.  

> [!IMPORTANT]  
> Standardmäßig wird dieser Task an jedem Standort täglich ausgeführt. An einem Standort der zentralen Verwaltung und primären Standorten werden mit dem Task Daten gelöscht, die älter als 30 Tage sind. Stellen Sie beim Verwenden von SQL Server Express an einem sekundären Standort sicher, dass dieser Task täglich ausgeführt wird und Daten gelöscht werden, die seit sieben Tagen inaktiv sind.  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|**Sekundärer Standort**|Aktiviert|

### <a name="delete-aged-metering-data"></a>Veraltete Softwaremessungsdaten löschen

Verwenden Sie diesen Task, um veraltete Softwaremessungsdaten aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Weitere Informationen finden Sie unter [Softwaremessung](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-metering-summary-data"></a>Veraltete Softwaremessungs-Zusammenfassungsdaten löschen

Verwenden Sie diesen Task, um veraltete Zusammenfassungsdaten für die Softwaremessung aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Weitere Informationen finden Sie unter [Softwaremessung](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-notification-server-history"></a>Veralteten Benachrichtigungsserververlauf löschen

Dieser Task löscht einen veralteten Clientanwesenheitsverlauf.

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-notification-task-history"></a>Veralteten Benachrichtigungstaskverlauf löschen

Verwenden Sie diesen Task, um Informationen zu Clientbenachrichtigungstasks aus der Standortdatenbank zu löschen. Dieser Task gilt für Daten, die für einen angegebenen Zeitraum nicht aktualisiert wurden. Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](../../clients/manage/client-notification.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-passcode-records"></a>Veraltete Kennungsdatensätze löschen

Verwenden Sie diesen Task am Standort auf oberster Ebene der Hierarchie, um veraltete Daten zu Kennungsrückstellungen für Windows Phone-Geräte zu löschen. Daten zum Zurücksetzen der Kennung sind verschlüsselt, enthalten allerdings die PIN für Geräte. Standardmäßig ist dieser Task aktiviert und löscht Daten, die älter als 1 Tag sind.  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-replication-data"></a>Veraltete Replikationsdaten löschen

Verwenden Sie diesen Task, um veraltete Daten zur Datenbankreplikation zwischen Configuration Manager-Standorten aus der Datenbank zu löschen. Wenn Sie die Konfiguration dieses Wartungstasks ändern, wirkt sich die Konfiguration auf jeden entsprechenden Standort in der Hierarchie aus. Weitere Informationen finden Sie unter [Überwachen der Datenbankreplikation](monitor-replication.md).  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|**Sekundärer Standort**|Aktiviert|

### <a name="delete-aged-replication-summary-data"></a>Veraltete Zusammenfassungsdatenreplikation löschen

Verwenden Sie diesen Task zum Löschen von Informationen über veraltete Zusammenfassungsdaten für die Replikation aus der Standortdatenbank, wenn die Daten innerhalb eines angegebenen Zeitraums nicht aktualisiert wurden. Weitere Informationen finden Sie unter [Überwachen der Datenbankreplikation](monitor-replication.md).  

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|**Sekundärer Standort**|Aktiviert|

### <a name="delete-aged-status-messages"></a>Veraltete Statusmeldungen löschen

Verwenden Sie diesen Task, um veraltete über Statusfilterregeln konfigurierte Statusmeldungsdaten aus der Datenbank zu löschen. Weitere Informationen hierzu finden Sie unter [Überwachen des Systemstatus für Configuration Manager](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-threat-data"></a>Veraltete Bedrohungsdaten löschen

Verwenden Sie diesen Task, um veraltete Endpoint Protection-Bedrohungsdaten aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Weitere Informationen finden Sie unter [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-unknown-computers"></a>Veraltete unbekannte Computer löschen

Verwenden Sie diesen Task zum Löschen von Informationen über unbekannte Computer aus der Standortdatenbank, wenn die Daten innerhalb eines angegebenen Zeitraums nicht aktualisiert wurden. Weitere Informationen finden Sie unter [Prepare for unknown computer deployments (Vorbereiten auf Bereitstellungen für unbekannte Computer)](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-aged-user-device-affinity-data"></a>Veraltete Daten zur Affinität zwischen Benutzer und Gerät löschen

Verwenden Sie diesen Task, um veraltete Daten zur Affinität zwischen Benutzer und Gerät aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-duplicate-system-discovery-data"></a>Doppelt vorhandene Systemermittlungsdaten löschen

Verwenden Sie diesen Task, um von der Systemermittlung generierte doppelte Datensätze aus der Standortdatenbank zu löschen.<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|Primärer Standort|Nicht verfügbar|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Abgelaufene MDM-Paketeinträge zur Massenregistrierung löschen

Verwenden Sie diesen Task, um alte Massenregistrierungszertifikate und dazugehörige Profile zu löschen, nachdem das Registrierungszertifikat abgelaufen ist. Weitere Informationen finden Sie unter [Erstellen von Zertifikatprofilen](../../../protect/deploy-use/create-certificate-profiles.md).

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-inactive-client-discovery-data"></a>Inaktive Clientermittlungsdaten löschen

Verwenden Sie diesen Task, um Ermittlungsdaten für inaktive Clients aus der Datenbank zu löschen. Der Standort kennzeichnet Clients als inaktiv, wenn der Client als veraltet markiert wird, sowie durch für den Clientstatus vorgenommene Konfigurationen.

Dieser Task kann nur für Ressourcen ausgeführt werden, bei denen es sich um Configuration Manager-Clients handelt. Er unterscheidet sich vom Task **Veraltete Ermittlungsdaten löschen**, über den alle veralteten Ermittlungsdatensätze gelöscht werden. Wenn dieser Task an einem Standort ausgeführt wird, werden Daten auf allen Standorten in der Hierarchie aus der Datenbank gelöscht. Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> Wenn Sie diesen Task aktivieren, legen Sie als Ausführungsintervall einen höheren Wert fest als beim Zeitplan für die **Frequenzermittlung**. Mit dieser Konfiguration können aktive Clients einen Frequenzermittlungsdatensatz senden, um Ihre Clientdatensätze als aktiv zu kennzeichnen, sodass sie von diesem Task nicht gelöscht werden.  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Nicht aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-obsolete-alerts"></a>Veraltete Warnungen löschen

Verwenden Sie diesen Task, um abgelaufene Warnungen aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und Statussystem](use-alerts-and-the-status-system.md).

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-obsolete-client-discovery-data"></a>Veraltete Clientermittlungsdaten löschen

Verwenden Sie diesen Task, um veraltete Clientdatensätze aus der Datenbank zu löschen. Ein als veraltet markierter Datensatz wurde normalerweise durch einen neueren Datensatz für den gleichen Client ersetzt. Der neue Datensatz wird als aktiver Datensatz des Clients übernommen. Informationen zur Ermittlung finden Sie unter [Ausführen der Ermittlung für System Center Configuration Manager](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> Wenn Sie diesen Task aktivieren, legen Sie als Ausführungsintervall einen höheren Wert fest als beim Zeitplan für die Frequenzermittlung. Mit dieser Konfiguration kann der Client einen Frequenzermittlungsdatensatz senden, um den Status „Veraltet“ ordnungsgemäß festzulegen.  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Nicht aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Veraltete Standorte und Subnetze der Gesamtstrukturermittlung löschen

Verwenden Sie diesen Task, um Daten zu Active Directory-Standorten, Subnetzen und Domänen zu löschen. Es werden Daten entfernt, die der Standort in den letzten 30 Tagen nicht mit der Active Directory-Gesamtstrukturermittlung ermittelt hat. Dieser Task entfernt zwar die Ermittlungsdaten, jedoch werden Grenzen, die Sie mithilfe dieser Ermittlungsdaten erstellen, nicht beeinträchtigt. Weitere Informationen finden Sie unter [Run discovery (Ausführen der Ermittlung)](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="delete-orphaned-client-deployment-state-records"></a>Verwaiste Datensätze zum Clientbereitstellungsstatus löschen

Verwenden Sie diesen Task, um in regelmäßigen Abständen die Tabelle zu löschen, die Statusinformationen zur Clientbereitstellung enthält. Dieser Task bereinigt Datensätze, die veralteten oder außer Betrieb genommenen Geräten zugeordnet sind.  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="evaluate-collection-members"></a>Sammlungsmitglieder auswerten

Sie konfigurieren die Auswertung der Sammlungsmitgliedschaft als Standortkomponente. Weitere Informationen finden Sie unter [Standortkomponenten](../deploy/configure/site-components.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="monitor-keys"></a>Schlüssel überwachen

Verwenden Sie diesen Task, um die Integrität der primären Schlüssel der Configuration Manager-Datenbank zu überwachen. Ein Primärschlüssel ist eine Spalte, die eine Zeile eindeutig identifiziert, oder eine Kombination von Spalten. Mit dem Schlüssel wird die Zeile von jeder anderen Zeile in einer Microsoft SQL Server-Datenbanktabelle unterschieden.

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Aktiviert|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="rebuild-indexes"></a>Indizes neu erstellen

Verwenden Sie diesen Task, um die Configuration Manager-Datenbankindizes neu zu erstellen. Ein Index ist eine Datenbankstruktur, die für eine Datenbanktabelle erstellt wird, um das Abrufen von Daten zu beschleunigen. So führt das Suchen in einer indizierten Spalte häufig wesentlich schneller zum Ziel als das Suchen in einer nicht indizierten Spalte.

Zur Verbesserung der Leistung werden die Configuration Manager-Datenbankindizes häufig aktualisiert, damit sie mit den sich ständig verändernden Daten in der Datenbank synchronisiert bleiben. Dieser Task:

- Erstellt Indizes für Datenbankspalten, die zu mindestens 50 Prozent eindeutig sind.
- Löscht Indizes für Spalten, die zu weniger als 50 Prozent eindeutig sind.
- Erstellt alle vorhandenen Indizes neu, die die Kriterien der Dateneindeutigkeit erfüllen.

|||
|---------|---------|
|**Standort der zentralen Verwaltung**|Nicht aktiviert|
|**Primärer Standort**|Nicht aktiviert|
|**Sekundärer Standort**|Nicht aktiviert|

### <a name="summarize-file-usage-metering-data"></a>Softwaremessungsdaten der Dateinutzung zusammenfassen

Verwenden Sie diesen Task, um die Softwaremessungsdaten für die Dateinutzung aus mehreren Datensätzen in einem allgemeinen Datensatz zusammenzufassen. Mithilfe der Datenzusammenfassung kann die Datenmenge in der Configuration Manager-Datenbank komprimiert werden.

Um Softwaremessungsdaten zusammenzufassen und die Speicherplatznutzung in der Datenbank zu verringern, verwenden Sie diesen Task in Kombination mit dem Task **Softwaremessungsdaten der monatlichen Nutzung zusammenfassen**. Weitere Informationen finden Sie unter [Softwaremessung](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="summarize-installed-software-data"></a>Daten installierter Software zusammenfassen

Verwenden Sie diesen Task, um die Daten aus mithilfe der Hardwareinventur gesammelten Asset Intelligence-Softwareinformationen zusammenzufassen, um mehrere Datensätze zu einem allgemeinen Datensatz zusammenzuführen. Mithilfe der Datenzusammenfassung kann die Datenmenge in der Configuration Manager-Datenbank komprimiert werden. Weitere Informationen finden Sie unter [Konfigurieren von Asset Intelligence-Wartungstasks](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="summarize-monthly-usage-metering-data"></a>Messungsdaten der monatlichen Nutzung zusammenfassen

Verwenden Sie diesen Task, um die Softwaremessungsdaten für die monatliche Nutzung aus mehreren Datensätzen in einem allgemeinen Datensatz zusammenzufassen. Mithilfe der Datenzusammenfassung kann die Datenmenge in der Configuration Manager-Datenbank komprimiert werden.

Um Softwaremessungsdaten zusammenzufassen und die Speicherplatznutzung in der Datenbank zu verringern, verwenden Sie diesen Task in Kombination mit dem Task **Softwaremessungsdaten der Dateinutzung zusammenfassen**. Weitere Informationen finden Sie unter [Softwaremessung](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="update-application-available-targeting"></a>In der Anwendung verfügbare Ziele aktualisieren

Verwenden Sie diesen Task, um Configuration Manager die Zuordnung von Richtlinien und Anwendungsbereitstellungen zu Ressourcen in Sammlungen neu berechnen zu lassen. Beim Bereitstellen von Richtlinien oder Anwendungen in einer Sammlung erstellt Configuration Manager eine anfängliche Zuordnung zwischen den Objekten, die Sie bereitstellen, und den Mitgliedern der Sammlung.

Diese Zuordnungen werden zur schnellen Bezugnahme in einer Tabelle gespeichert. Wenn sich die Mitgliedschaft von Sammlungen ändert, aktualisiert der Standort diese gespeicherten Zuordnungen entsprechend dieser Änderungen. Es ist jedoch möglich, dass diese Zuordnungen ihre Synchronität verlieren. Wenn z. B. der Standort eine Benachrichtigungsdatei nicht ordnungsgemäß verarbeiten kann, wird diese Änderung ggf. nicht als Änderung an den Zuordnungen wiedergegeben. Dieser Task aktualisiert diese Zuordnung basierend auf der aktuellen Mitgliedschaft in der Sammlung.  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|

### <a name="update-application-catalog-tables"></a>Tabellen für Anwendungskatalog-Updates

Verwenden Sie diesen Task, um den Datenbankcache der Anwendungskatalog-Website mit den aktuellen Anwendungsinformationen zu synchronisieren. Wenn Sie die Konfiguration dieses Wartungstasks ändern, wirkt sich dies auf alle primären Standorte der Hierarchie aus.  

|||
|---------|---------|
|Standort der zentralen Verwaltung|Nicht verfügbar|
|**Primärer Standort**|Aktiviert|
|Sekundärer Standort|Nicht verfügbar|


## <a name="see-also"></a>Weitere Informationen:

[Wartungstasks](maintenance-tasks.md)
