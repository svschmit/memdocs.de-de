---
title: Konsoleninterne Updates
titleSuffix: Configuration Manager
description: Installieren von Configuration Manager-Updates über die Microsoft-Cloud
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0d7f36c921f782c0baad740d8e643f54cee0309
ms.sourcegitcommit: 5e339c07001e911cf75ef922e6c66a7efdeab6f1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/10/2020
ms.locfileid: "84637668"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Installieren konsoleninterner Updates für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager ruft Updates durch die Synchronisierung mit dem Microsoft-Clouddienst ab. Installieren Sie diese Updates anschließend aus der Configuration Manager-Konsole.

## <a name="get-available-updates"></a>Abrufen aller verfügbaren Updates

Der Standort lädt nur Updates herunter, die für Ihre Infrastruktur und Version relevant sind. Diese Synchronisierung kann automatisch oder manuell erfolgen, je nachdem, wie Sie den Dienstverbindungspunkt für Ihre Hierarchie konfigurieren:

- Im **Onlinemodus**stellt der Dienstverbindungspunkt automatisch eine Verbindung mit dem Microsoft-Clouddienst her und lädt relevante Updates herunter.  

    Configuration Manager sucht standardmäßig alle 24 Stunden nach neuen Updates. Suchen Sie in der Configuration Manager-Konsole manuell nach Updates. Wechseln Sie zum Arbeitsbereich **Verwaltung**, wählen Sie den Knoten **Updates und Wartung** und dann im Menüband **Auf Updates prüfen** aus.  

- Im **Offlinemodus** stellt der Dienstverbindungspunkt keine Verbindung mit dem Microsoft-Clouddienst her. Verwenden Sie zum Herunterladen und anschließenden Importieren verfügbarer Updates [das Dienstverbindungstool](use-the-service-connection-tool.md).  

> [!NOTE]  
> Importieren Sie wenn nötig Out-of-band-Fixes in Ihre Konsole. Verwenden Sie hierzu das [Tool zur Updateregistrierung](use-the-update-registration-tool-to-import-hotfixes.md). Diese Out-of-band-Fixes ergänzen die Updates, die Sie beim Synchronisieren mit dem Microsoft-Clouddienst erhalten.  

Nach der Synchronisierung der Updates können Sie diese in der Configuration Manager-Konsole anzeigen. Gehen Sie zum Arbeitsbereich **Verwaltung**, und klicken Sie dann auf den Knoten **Updates und Wartung**.  

- Nicht installierte Updates werden als **Verfügbar** angezeigt.  

- Installierte Updates werden als **Installiert** angezeigt. Nur die aktuellsten Updates werden angezeigt. Wenn zuvor installierte Updates angezeigt werden sollen, wählen Sie im Menüband **Verlauf** aus.  

Bevor Sie den Dienstverbindungspunkt konfigurieren, sollten Sie die zusätzlichen Anwendungsbereiche verstehen und entsprechend planen. Folgende Verwendungen können Auswirkungen auf Ihre Konfiguration dieser Standortsystemrolle haben:  

- Der Standort verwendet den Dienstverbindungspunkt, um Nutzungsinformationen zu Ihrem Standort hochzuladen. Diese Informationen helfen dem Microsoft-Clouddienst bei der Identifizierung von Updates, die für die aktuelle Version Ihrer Infrastruktur verfügbar sind. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Wenn Sie sich ausführlicher über die Vorgänge bei einem Update informieren möchten, können Sie sich folgende Flussdiagramme ansehen:  

- [Flussdiagramm: Herunterladen von Updates](download-updates-flowchart.md)  

- [Flussdiagramm: Aktualisieren von Replikationen](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Zuweisen von Berechtigungen zum Anzeigen und Verwalten von Updates und Funktionen

Um Updates in der Konsole anzuzeigen, muss einem Benutzer eine rollenbasierte Administratorsicherheitsrolle zugewiesen sein, die die Sicherheitsklasse **Updatepakete** enthält. Diese Klasse gewährt Zugriff auf das Anzeigen und Verwalten von Updates in der Configuration Manager-Konsole.

### <a name="about-the-update-packages-class"></a>Die Updatepakete-Klasse

In der Standardeinstellung ist die Klasse **Updatepakete** (SMS_CM_Updatepackages) Teil der folgenden integrierten Sicherheitsrollen mit den aufgeführten Berechtigungen:  

- **Hauptadministrator** mit den Berechtigungen **Ändern** und **Lesen** .  

  - Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Sicherheitsbereich **Alle** kann Updates anzeigen und installieren. Der Benutzer kann auch während der Installation Features aktivieren. Außerdem kann er einzelne Features aktivieren, nachdem der Standort aktualisiert wurde.  

  - Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Sicherheitsbereich **Standard** kann Updates anzeigen und installieren. Der Benutzer kann auch während der Installation Features aktivieren. Außerdem kann er Features anzeigen lassen, nachdem der Standort aktualisiert wurde. Dieser Benutzer kann jedoch nach Abschluss des Standortupdates keine Features mehr aktivieren.  

- **Analyst mit Leseberechtigung** mit der Berechtigung **Lesen** :  

  - Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den **Standard**bereich kann sich Updates anzeigen lassen, diese aber nicht installieren. Dieser Benutzer kann sich ebenfalls nach Aktualisierung eines Standorts Features anzeigen lassen, diese jedoch nicht aktivieren.  

### <a name="permissions-required-for-updates-and-servicing"></a>Erforderliche Berechtigungen für Updates und Wartung

- Verwenden Sie ein Konto, dem Sie eine Sicherheitsrolle zuweisen, die über die Klasse **Updatepakete** und die Berechtigungen **Ändern** und **Lesen** verfügt.  

- Weisen Sie das Konto dem **Standardbereich** zu.  

### <a name="permissions-to-only-view-updates"></a>Berechtigungen, mit denen sich Updates ausschließlich anzeigen lassen

- Verwenden Sie ein Konto, dem Sie eine Sicherheitsrolle zuweisen, die über die Klasse **Updatepakete** mit ausschließlich der Berechtigung **Lesen** verfügt.  

- Weisen Sie das Konto dem **Standardbereich** zu.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Erforderliche Berechtigungen zum Aktivieren dieser Features nach dem Standortupdate

- Verwenden Sie ein Konto, dem Sie eine Sicherheitsrolle zuweisen, die über die Klasse **Updatepakete** und die Berechtigungen **Ändern** und **Lesen** verfügt.  

- Weisen Sie das Konto dem Bereich **Alle Bereiche** zu.  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Vor der Installation eines konsoleninternen Updates  

Sehen Sie sich die folgenden Schritte an, bevor Sie ein Update in der Configuration Manager-Konsole installieren.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Schritt 1: Überprüfen der Updatecheckliste  

Überprüfen Sie die zutreffende Updatecheckliste mit vor dem Update durchzuführenden Schritten:

- [Prüfliste für die Installation von Update 2002](checklist-for-installing-update-2002.md)

- [Prüfliste für die Installation von Update 1910](checklist-for-installing-update-1910.md)  

- [Prüfliste für die Installation von Update 1906](checklist-for-installing-update-1906.md)  

- [Prüfliste für die Installation von Update 1902](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a> Schritt 2: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates  

Bevor Sie ein Update installieren, sollten Sie die Voraussetzungsprüfung für das Update ausführen. Wenn Sie vor der Installation eines Updates die Voraussetzungsprüfung ausführen, geschieht Folgendes:  

- Der Standort repliziert alle Updatedateien auf andere Standorte, bevor das Update installiert wird.  

- Die Voraussetzungsprüfung wird automatisch erneut ausgeführt, wenn Sie sich für die Installation des Updates entscheiden.  

> [!NOTE]  
> Wenn Sie eine Voraussetzungsprüfung starten und dann den Status anzeigen, wird die Phase **Installation** als aktiv angezeigt. Tatsächlich installiert der Standort das Update aber nicht. Um die Voraussetzungsprüfung auszuführen, extrahiert der Updatevorgang das Paket aus der Inhaltsbibliothek. Anschließend wird das Paket in einem Stagingordner platziert, in dem es auf die aktuellen Voraussetzungsprüfungen zugreifen kann. Der gleiche Vorgang wird ausgeführt, wenn Sie ein Update installieren. Aufgrund dieses Verhaltens wird die Installationsphase als **In Bearbeitung** angezeigt. Nur der Schritt *Updatepaket extrahieren* wird in der Kategorie „Installation“ angezeigt.  

Wenn Sie später das Update installieren, können Sie das Update so konfigurieren, das Warnungen der Voraussetzungsprüfung ignoriert werden.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>So führen Sie vor der Installation eines Updates die Voraussetzungsprüfung aus  

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Updates und Wartung** aus.  

2. Wählen Sie das Updatepaket aus, für das die Voraussetzungsprüfung ausgeführt werden soll.  

3. Wählen Sie im Menüband **Voraussetzungsprüfung ausführen** aus.  

    Beim Ausführen der Voraussetzungsprüfung wird der Inhalt für das Update auf untergeordnete Standorte repliziert. Zeigen Sie die Datei **distmgr.log** auf dem Standortserver an, um sicherzustellen, dass der Inhalt erfolgreich repliziert wird.  

4. So zeigen Sie die Ergebnisse der Voraussetzungsprüfung an:  

    1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**.  

    2. Wählen Sie den Knoten **Update- und Wartungsstatus** aus, und suchen Sie nach dem Voraussetzungsstatus.  

    3. Weitere Informationen finden Sie in der Datei **ConfigMgrPrereq.log** auf dem Standortserver.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> Installieren konsoleninterner Updates  

Wenn Sie zur Installation von Updates in der Configuration Manager-Konsole bereit sind, beginnen Sie mit dem Standort der obersten Ebene der Hierarchie. Dieser Standort ist entweder der Standort der zentralen Verwaltung oder ein eigenständiger primärer Standort.  

Installieren Sie das Update für jeden Standort außerhalb der normalen Geschäftszeiten, um die Auswirkungen auf den Geschäftsbetrieb zu minimieren. Die Updateinstallation könnte Aktionen wie das Neuinstallieren von Standortkomponenten und Standortsystemrollen umfassen.  

- An untergeordneten primären Standorten wird das Update automatisch gestartet, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Hierbei handelt es sich um den empfohlenen Standardprozess. Mithilfe von [Dienstfenster für Standortserver](service-windows.md) können Sie steuern, wann Updates an einem Standort installiert werden.  

- Aktualisieren Sie sekundäre Standorte über die Configuration Manager-Konsole manuell, nachdem das Update des primären übergeordneten Standorts abgeschlossen wurde. Das automatische Update sekundärer Standortserver wird nicht unterstützt.  

- Wenn Sie nach dem Standortupdate eine Configuration Manager-Konsole verwenden, werden Sie aufgefordert, die Konsole zu aktualisieren.  

- Nachdem der Standortserver die Installation eines Updates erfolgreich abschließt, werden automatisch alle relevanten Standortsystemrollen aktualisiert. Jedoch werden nicht alle Verteilungspunkte erneut installiert und gehen offline, um gleichzeitig aktualisiert zu werden. Stattdessen verwendet der Standortserver die Einstellungen des Standorts zur Inhaltsverteilung, um das Update nacheinander auf eine Teilmenge von Verteilungspunkten zu verteilen. Das bedeutet, dass nur manche Verteilungspunkte nach der Installation des Updates offline geschaltet werden. Verteilungspunkte, die noch nicht aktualisiert wurden oder bei denen das Update schon abgeschlossen ist, bleiben online und können Clients Inhalte bereitstellen.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Übersicht über die konsoleninterne Updateinstallation  

#### <a name="1-when-the-update-installation-starts"></a>1. Zu Beginn der Updateinstallation

Der Assistent für Updates zeigt eine Liste der vom Update betroffenen Produktbereiche an.  

- Auf der Seite **Allgemein** des Assistenten können Sie **Warnungen aus der Voraussetzungsüberprüfung** individuell konfigurieren:  

  - Bei Voraussetzungsfehlern wird Updateinstallation immer beendet. Beheben Sie die Fehler, bevor die Installation des Updates erfolgreich wiederholt werden kann. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](#bkmk_retry).  

  - Bei Voraussetzungswarnungen kann die Updateinstallation ebenfalls beendet werden. Beheben Sie die Warnungen, bevor Sie die Installation des Updates wiederholen. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](#bkmk_retry).  

  - **Alle Warnungen der Voraussetzungsüberprüfung ignorieren und das Update unabhängig von fehlenden Voraussetzungen installieren**: Legen Sie eine Bedingung für die Installation des Updates fest, damit Warnungen zu erforderlichen Komponenten ignoriert werden. Mit dieser Option kann die Installation des Updates fortgesetzt werden. Wenn Sie diese Option nicht auswählen, wird die Updateinstallation beendet, wenn eine Warnung auftritt. Verwenden Sie diese Option nicht, wenn Sie vorher keine Voraussetzungsprüfung durchgeführt und Voraussetzungswarnungen für einen Standort nicht behoben haben.  

    In den Arbeitsbereichen **Verwaltung** und **Überwachung** enthält der Knoten „Updates und Wartung“ eine Schaltfläche auf dem Menüband **Warnungen zu erforderlichen Komponenten ignorieren**. Diese Schaltfläche wird verfügbar, wenn ein Updatepaket die Installation aufgrund von Warnungen der Voraussetzungsprüfung nicht erfolgreich abschließen kann. Beispiel: Sie installieren ein Update, ohne die Option zum Ignorieren von Voraussetzungswarnungen (im Update-Assistenten) zu verwenden. Die Updateinstallation wird mit einem Status beendet, dass Voraussetzungswarnungen vorliegen, jedoch keine Fehler. Wählen Sie später im Menüband **Warnungen zu erforderlichen Komponenten ignorieren** aus. Diese Aktion löst eine automatische Fortsetzung der Updateinstallation aus, wodurch Warnungen zu Voraussetzung ignoriert werden. Wenn Sie diese Option verwenden, wird die Installation der Updates automatisch nach einigen Minuten fortgesetzt.  

- Wenn ein Update für den Konfigurations-Manager-Client relevant ist, wählen Sie aus, das Clientupdate mit einer begrenzten Clientanzahl zu testen. Weitere Informationen finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Während der Updateinstallation

Im Rahmen der Updateinstallation führt Configuration Manager folgende Aktionen aus:  

- Neuinstallation aller betroffenen Komponenten wie der Standortsystemrollen oder der Configuration Manager-Konsole.  

- Updates für Clients werden auf der Grundlage Ihrer Auswahl für Pilottests für Clients und für [automatische Clientupgrades](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) verwaltet.  

- Standortsystemserver müssen während der Installation generell nicht neu gestartet werden. Wenn eine Rolle .NET verwendet, und das Paket die erforderliche Komponente aktualisiert, muss das Standortsystem neu gestartet werden.  

> [!TIP]  
> Bei der Installation von Configuration Manager-Updates aktualisiert der Standort auch den Ordner „CD.Latest“. Weitere Informationen finden Sie unter [Der Ordner „CD.Latest“](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Überwachen des Status von Updates während der Installation

Führen Sie die folgenden Schritte aus, um den Fortschritt zu überwachen:  

- Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Updates und Wartung** aus. Dieser Knoten zeigt den Installationsstatus aller Updatepakete an.  

- Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Update- und Wartungsstatus** aus. Dieser Knoten zeigt nur den Installationsstatus des aktuellen Updatepakets an, das der Standort gerade installiert.  

    Zur einfacheren Überwachung wird die Installation der Updates in verschiedene Phasen unterteilt. Für jede der folgenden Phasen finden Sie im Installationsstatus zusätzliche Informationen dazu, in welcher Protokolldatei Sie weitere Informationen finden:  

  - **Herunterladen:** Diese Phase gilt nur für den Standort der obersten Ebene mit dem Dienstverbindungspunkt.

  - **Replikation**

  - **Prüfung der erforderlichen Komponenten**

  - **Installation**

  - **Nach der Installation:** Weitere Informationen finden Sie unter [Aufgaben nach der Installation](#post-installation-tasks).  

- Zeigen Sie die Datei **CMUpdate.log** in `<ConfigMgr_Installation_Directory>\Logs` auf dem Standortserver an.  

>[!NOTE]
> Ab Version 1906 können Sie den Zustand der Aufgabe **Upgrade für ConfigMgr-Datenbank ausführen** während der **Installationsphase** verfolgen.
>
> - Wenn das Datenbankupgrade blockiert ist, erhalten Sie die Warnmeldung **Wird ausgeführt, Eingreifen erforderlich**.
>   - In „cmupdate.log“ werden der Name des Programms und die sessionID aus SQL, die das Upgrade der Datenbank blockiert, protokolliert.
> - Wenn das Upgrade der Datenbank nicht mehr blockiert wird, wird der Status auf **Wird ausgeführt** oder **Abgeschlossen** zurückgesetzt.
>   - Wenn das Upgrade der Datenbank blockiert wird, erfolgt alle 5 Minuten eine Prüfung, um festzustellen, ob es weiterhin blockiert wird.

#### <a name="4-when-the-update-installation-completes"></a>4. Zum Abschluss der Updateinstallation

Nach dem Abschluss der Installation des ersten Standortupdates:  

- An untergeordneten primären Standorten wird das Update automatisch installiert. Es ist keine weitere Aktion erforderlich.  

- Aktualisieren Sie sekundäre Standorte in der Configuration Manager-Konsole manuell. Weitere Informationen finden Sie unter [So starten Sie die Updateinstallation an einem sekundären Standort](#bkmk_secondary).  

- Bis für alle Standorte in der Hierarchie das Update auf die neue Version durchgeführt wurde, erfolgt der Betrieb der Hierarchie im gemischten Versionsmodus. Weitere Informationen finden Sie unter [Interoperabilität zwischen verschiedenen Versionen](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. Aktualisieren von Configuration Manager-Konsolen

Nach dem Update eines Standorts der zentralen Verwaltung oder eines primären Standorts muss jede Configuration Manager-Konsole, die mit diesem Standort eine Verbindung herstellt, ebenfalls aktualisiert werden. In folgenden Fällen werden Sie zum Aktualisieren einer Konsole aufgefordert:  

- Wenn Sie die Konsole öffnen.  

- Sie navigieren in einer geöffneten Konsole zu einem neuen Knoten.  

Aktualisieren Sie die Konsole sofort nach dem Standortupdate.  

Überprüfen Sie nach Abschluss des Konsolenupdates, ob die Versionen von Konsole und Standort korrekt sind. Navigieren Sie oben links in der Konsole zu **Informationen zu Configuration Manager**.  

> [!Note]  
> Die Konsolenversion unterscheidet sich etwas von der Standortversion. Die Nebenversion der Konsole entspricht der Release-Version von Configuration Manager. In Configuration Manager Version 1802 lautet die anfängliche Standortversion beispielsweise 5.0.8634.1000 und die erste Konsolenversion 5.**1802**.1082.1700. Die Build- (1082) und Revisionsnummern (1700) können sich mit zukünftigen Hotfixes ändern.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a> So starten Sie die Updateinstallation am Standort der obersten Ebene  

Gehen Sie am Standort der obersten Ebene in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Updates und Wartung** aus. Wählen Sie ein Update mit dem Status **Verfügbar** und dann im Menüband **Updatepaket installieren** aus.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> So starten Sie die Updateinstallation an einem sekundären Standort  

Nachdem der übergeordnete primäre Standort eines sekundären Standorts aktualisiert wurde, aktualisieren Sie den sekundären Standort über die Configuration Manager-Konsole. Verwenden Sie dafür den **Assistenten für das Update von sekundären Standorten**.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie den sekundären Standort, den Sie aktualisieren möchten, und dann im Menüband **Upgrade** aus.  

2. Wählen Sie **Ja** aus, um das Update des sekundären Standorts zu starten.  

Um die Updateinstallation an einem sekundären Standort zu überwachen, wählen Sie diesen Standort und dann im Menüband **Installationsstatus anzeigen** aus. Fügen Sie außerdem dem Knoten „Standorte“ die Spalte **Version** hinzu, damit Sie die Version jedes sekundären Standorts anzeigen können.  

In manchen Fällen wird der Status in der Konsole nicht aktualisiert oder zeigt an, dass das Update fehlerhaft ist. Nachdem ein sekundärer Standort erfolgreich aktualisiert wurde, verwenden Sie die Option **Installation noch mal versuchen**. Diese Option installiert das Update für einen sekundären Standort, an dem das Update erfolgreich installiert wurde, nicht erneut, zwingt jedoch die Konsole dazu, den Status zu aktualisieren.

### <a name="post-installation-tasks"></a>Aufgaben nach der Installation

Wenn ein Standort ein Update installiert, gibt es mehrere Tasks, die erst gestartet werden können, nachdem die Installation des Updates auf dem Standortserver abgeschlossen wurde. Diese Liste enthält Tasks nach der Installation, die für Standort- und Hierarchievorgänge von entscheidender Bedeutung sind. Da sie von entscheidender Bedeutung sind, werden sie aktiv überwacht. Zu den zusätzlichen Tasks, die nicht direkt überwacht werden, gehört die erneute Installation von Standortsystemrollen. Wählen Sie zum Anzeigen des Status von kritischen Tasks nach der Installation den Task **Nach der Installation** während der Überwachung der Updateinstallation für einen Standort aus.

Nicht alle Tasks werden sofort abgeschlossen. Einige Tasks werden erst gestartet, wenn für jeden Standort die Installation des Updates abgeschlossen ist. Aus diesem Grund kann sich die Bereitstellung der erwarteten neuen Funktionen verzögern, bis diese Tasks abgeschlossen sind. Da neue Features erst aktiviert werden, wenn für alle Standorte die Updateinstallation abgeschlossen ist, werden neue Features möglicherweise einige Zeit nicht angezeigt.

Tasks nach der Installation:

- **Der SMS_EXECUTIVE-Dienst wird installiert**

  - Kritischer Dienst, der auf dem Standortserver ausgeführt wird.
  - Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.

- **Die SMS_DATABASE_NOTIFICATION_MONITOR-Komponente wird installiert**

  - Kritischer Standortkomponententhread des SMS_EXECUTIVE-Diensts.
  - Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.

- **Die SMS_HIERARCHY_MANAGER-Komponente wird installiert**

  - Kritische Standortkomponente, die auf dem Standortserver ausgeführt wird.
  - Verantwortlich für die erneute Installation von Rollen auf Servern des Standortsystems. Der Status für die erneute Installation einzelner Standortsystemrollen wird nicht angezeigt.
  - Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.

    > [!Note]
    > Einige Configuration Manager-Standortrollen nutzen das Clientframework gemeinsam. Beispielsweise Verwaltungspunkt und Pullverteilungspunkt. Wenn diese Rollen aktualisiert werden, wird die Clientversion auf diesen Servern gleichzeitig aktualisiert. Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Die SMS_REPLICATION_CONFIGURATION_MONITOR-Komponente wird installiert**

  - Kritische Standortkomponente, die auf dem Standortserver ausgeführt wird.
  - Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.

- **Die SMS_POLICY_PROVIDER-Komponente wird installiert**

  - Kritische Standortkomponente, die nur in primären Standorten ausgeführt wird.
  - Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.

- **Replikationsinitialisierung wird überwacht**

  - Dieser Task wird nur am Standort der zentralen Verwaltung und an untergeordneten primären Standorten angezeigt.
  - Hängt von SMS_REPLICATION_CONFIGURATION_MONITOR ab.
  - Sollte schnell abgeschlossen sein.

- **Das Configuration Manager-Clientpaket für die Präproduktion wird aktualisiert**

  - Dieser Task wird selbst dann angezeigt, wenn die Verwendung von Clientpaketen für die Präproduktion (sogenannte Clientpilottests) nicht aktiviert ist.
  - Wird erst gestartet, wenn für alle Standorte in der Hierarchie die Installation des Updates abgeschlossen ist.

- **Der Clientordner auf dem Standortserver wird aktualisiert**

  - Dieser Task wird nicht angezeigt, wenn Sie den Client in der Präproduktion verwenden.  
  - Sollte schnell abgeschlossen sein.

- **Das Configuration Manager-Clientpaket wird aktualisiert**

  - Dieser Task wird nicht angezeigt, wenn Sie den Client in der Präproduktion verwenden.  
  - Wird erst beendet, wenn für alle Standorte das Update installiert wurde.  

- **Features werden aktiviert**

  - Dieser Task wird nur am Standort der obersten Ebene in der Hierarchie angezeigt.
  - Wird erst gestartet, wenn für alle Standorte in der Hierarchie die Installation des Updates abgeschlossen ist.
  - Einzelne Features werden nicht angezeigt.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Wiederholen der Installation eines fehlerhaften Updates  

Wenn ein Update nicht installiert werden kann, überprüfen Sie das Feedback in der Konsole, um Lösungen für Warnungen und Fehler zu finden. Zeigen Sie für weitere Informationen die Datei **ConfigMgrPrereq.log** an. Bevor Sie die Installation eines Updates wiederholen, müssen Sie die Fehler und sollten Sie die Warnungen beheben.  

> [!TIP]  
> Wenn beim Herunterladen oder Replizieren eines Updates Probleme auftreten, Verwenden Sie das [Tool zum Zurücksetzen von Updates](update-reset-tool.md).  

Wenn Sie die Installation eines Updates wiederholen möchten, wählen Sie das fehlerhafte Update aus, und wählen Sie anschließend eine zutreffende Option aus. Das Verhalten der Wiederholung der Updateinstallation hängt vom Knoten ab, von dem aus Sie die Wiederholung starten und von der Wiederholungsoption, die Sie verwenden.  

### <a name="retry-installation-for-the-hierarchy"></a>Wiederholen der Installation für die Hierarchie

Wiederholen Sie die Installation eines Updates für die gesamte Hierarchie, wenn sich das Update in einem der folgenden Zustände befindet:  

- Voraussetzungsprüfung mit mindestens einer Warnung bestanden, und die Option zum Ignorieren von Voraussetzungswarnungen wurde im Update-Assistenten nicht festgelegt. (Der Updatewert für **Voraussetzungswarnung ignorieren** im Knoten **Updates und Wartung** ist auf **Nein** festgelegt.)

- Fehler bei der Voraussetzung.

- Fehler bei der Installation.  

- Fehler bei der Replikation des Inhalts auf den Standort.

Gehen Sie zum Arbeitsbereich **Verwaltung**, und klicken Sie dann auf den Knoten **Updates und Wartung**. Wählen Sie das Update und anschließend eine der folgenden Optionen aus:  

- **Wiederholen:** Wenn Sie **Wiederholen** über **Updates und Wartung** ausführen, wird die Installation des Updates neu gestartet, und Voraussetzungswarnungen werden automatisch ignoriert. Wenn bei der Replikation von Inhalten zuvor ein Fehler aufgetreten ist, wird der Inhalt für das Update erneut repliziert.  

- **Warnungen zu erforderlichen Komponenten ignorieren:** Wenn die Installation des Updates aufgrund einer Warnung angehalten wird, klicken Sie auf **Warnungen zu erforderlichen Komponenten ignorieren**. Dadurch kann die Installation des Updates nach wenigen Minuten fortgesetzt werden, und die Option zum Ignorieren von Voraussetzungswarnungen wird angewendet.

### <a name="retry-installation-for-the-site"></a>Wiederholen der Installation für den Standort

Wiederholen Sie die Installation eines Updates an einem bestimmten Standort, wenn sich das Update in einem der folgenden Zustände befindet:  

- Voraussetzungsprüfung mit mindestens einer Warnung bestanden, und die Option zum Ignorieren von Voraussetzungswarnungen wurde im Update-Assistenten nicht festgelegt. (Der Updatewert für **Voraussetzungswarnung ignorieren** im Knoten „Updates und Wartung“ ist auf **Nein** festgelegt.)  

- Fehler bei der Voraussetzung.

- Fehler bei der Installation.

Navigieren Sie zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Site Servicing Status** (Wartungsstatus des Standorts) aus. Wählen Sie das Update und anschließend eine der folgenden Optionen aus:  

- **Wiederholen:** Wenn Sie **Wiederholen** über **Site Servicing Status** (Wartungsstatus des Standorts) ausführen, starten Sie die Installation des Updates nur an diesem Standort neu. Im Gegensatz zur Ausführung von **Wiederholen** vom Knoten **Updates und Wartung** ignoriert diese Wiederholung Voraussetzungswarnungen nicht.  

- **Warnungen zu erforderlichen Komponenten ignorieren:** Wenn die Installation des Updates aufgrund einer Warnung angehalten wird, können Sie **Warnungen zu erforderlichen Komponenten ignorieren** auswählen. Dadurch kann die Installation des Updates nach wenigen Minuten fortgesetzt werden, und die Option zum Ignorieren von Voraussetzungswarnungen wird angewendet.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Nach der Installation eines Updates an einem Standort  

Überprüfen Sie nach dem Update an einem Standort die Checkliste, die für die entsprechende aktualisierte Version gilt:  

- [Prüfliste nach dem Update für Version 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Prüfliste nach dem Update für Version 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Post-update checklist for version 1906 (Checkliste nach dem Update für Version 1906)](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Post-update checklist for version 1902 (Checkliste nach dem Update für Version 1902)](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Aktivieren optionaler Features von Updates  

Wenn ein Update ein oder mehrere optionale Features enthält, haben Sie die Möglichkeit, diese Features in Ihrer Hierarchie zu aktivieren. Aktivieren Sie Features während der Updateinstallation, oder kehren Sie zu einem späteren Zeitpunkt zur Konsole zurück, um die optionalen Features zu aktivieren.

Um verfügbare Features und deren Status anzuzeigen, wechseln Sie in der Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Updates und Wartung**, und wählen Sie den Knoten **Features** aus.

Wenn ein Feature nicht optional ist, wird es automatisch installiert. Es wird nicht im Knoten **Features** angezeigt.  

> [!Important]  
> In einer Hierarchie mit mehreren Standorten können Sie nur optionale Features oder Features der Vorabversion vom Standort der zentralen Verwaltung aus aktivieren. Dieses Verhalten stellt sicher, dass keine Konflikte in der Hierarchie auftreten. <!--507197-->  

Wenn Sie ein neues Features oder ein Feature der Vorabversion aktivieren, muss der Hierarchie-Manager von Configuration Manager (HMAN) die Änderung verarbeiten, bevor Sie das Feature nutzen können. Die Verarbeitung der Änderungen erfolgt oft sofort. Je nach Verarbeitungszyklus des HMAN kann es bis zu 30 Minuten dauern, bis die Verarbeitung abgeschlossen ist. Starten Sie die Konsole nach Abschluss der Änderungen neu, damit Sie das Feature verwenden können.

Ab Version 2002 gilt Folgendes:<!--5834830--> Wenn neue cloudbasierte Features im Microsoft Endpoint Manager Admin Center oder in anderen angefügten Clouddiensten für Ihre lokale Configuration Manager-Installation verfügbar sind, können Sie diese neuen Features jetzt in der Configuration Manager-Konsole aktvieren.

### <a name="list-of-optional-features"></a>Liste der optionalen Features

Die folgenden Features sind in der neuesten Version von Configuration Manager optional:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Community Hub](community-hub.md)<!--3555935, C098DA03-C33C-4E15-B337-6C0FEEB3CB8A-->
- [BitLocker-Verwaltung](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Azure Active Directory-Benutzergruppenermittlung](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Anwendungsgruppen](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Debugger für Tasksequenzen](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Paketkonvertierungs-Manager](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Client-Apps für gemeinsam verwaltete Geräte](../../../comanage/workloads.md#client-apps) (zuvor bekannt als *Mobile Apps für gemeinsam verwaltete Geräte*) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Updates für Drittanbietersoftware](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Genehmigen von Anwendungsanforderungen für Benutzer pro Gerät](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Erstellen und Ausführen von Skripts](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Surface-Treiberupdates](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Cloudverwaltungsgateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [Erstellen von PFX-Dateien](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics-Connector](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender Exploit Guard-Richtlinie](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN für Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Warten einer clusterfähigen Sammlung (Servergruppen)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md) (zuvor bekannt als *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Weitere Informationen zu Features, die Zustimmung für die Aktivierung erfordern, finden Sie in den [Features der Vorabversion](pre-release-features.md).  
>
> Weitere Informationen zu Features, die nur im Technical Preview-Branch verfügbar sind, finden Sie unter [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Verwenden von vorab veröffentlichten Features von Updates

Current Branch enthält Features der Vorabversion, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Weitere Informationen finden Sie unter [Features der Vorabversion](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Häufig gestellte Fragen

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Warum werden bestimmte Updates nicht in der Konsole angezeigt?

Wenn Sie nach einer erfolgreichen Synchronisierung mit dem Microsoft-Clouddienst ein bestimmtes Update in der Konsole nicht finden, kann dieses Verhalten folgende Ursachen haben:  

- Für das Update ist eine Konfiguration erforderlich, die von Ihrer Infrastruktur nicht verwendet wird, oder eine Voraussetzung für den Empfang des Updates wird von der aktuellen Produktversion nicht erfüllt.  

    Wenn Sie Ihrer Meinung nach über alle erforderlichen Konfigurationen und Voraussetzungen für ein fehlendes Update verfügen, überprüfen Sie, ob sich Ihr Dienstverbindungspunkt im Onlinemodus befindet. Verwenden Sie anschließend unter dem Knoten **Updates und Wartung** die Option **Suchen nach Updates**, um die Prüfung zu erzwingen. Wenn sich Ihr Dienstverbindungspunkt im Offlinemodus befindet, verwenden Sie das Dienstverbindungstool, um eine manuelle Synchronisierung mit dem Clouddienst auszuführen.  

- Ihr Konto verfügt nicht über die richtigen rollenbasierten Administratorberechtigungen zum Anzeigen von Updates in der Configuration Manager-Konsole. Weitere Informationen finden Sie unter [Berechtigungen zum Verwalten von Updates](#assign-permissions-to-view-and-manage-updates-and-features).  
