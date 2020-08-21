---
title: Entfernen des Standorts der zentralen Verwaltung (Central Administration Site, CAS)
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie den Standort der zentralen Verwaltung entfernen können, um Ihre Configuration Manager-Infrastruktur auf einen einzelnen, eigenständigen primären Standort zu vereinfachen.
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a1d9d4ce8cdd19efb440d4d73fafdc96a514bcd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699159"
---
# <a name="remove-the-central-administration-site"></a>Entfernen des Standorts der zentralen Verwaltung

*Gilt für: Configuration Manager (Current Branch)*

<!-- 3607277 -->

Wenn Ihre Hierarchie aus einem Standort der zentralen Verwaltung (Central Administration Site, CAS) und einem einzelnen untergeordneten primären Standort besteht, können Sie ersteren ab der Version 2002 entfernen. Dadurch wird Ihre Configuration Manager-Infrastruktur vereinfacht und auf einen einzelnen, eigenständigen primären Standort reduziert. Die komplexe Replikation zwischen Standorten wird beseitigt, und Ihre Verwaltungsaufgaben werden an einem einzelnen Standort zusammengeführt.

> [!IMPORTANT]
> In dieser Configuration Manager-Version handelt es sich um ein Vorabfeature, das standardmäßig nicht aktiviert ist. Aktuell steht es für Premier-Kunden von Microsoft zur Verfügung.
>
> Wenden Sie sich an Ihren technischen Kontomanager, wenn Sie dieses Feature aktivieren möchten:
>
> - Ihr TAM öffnet einen Beratungsfall, für den Ihre Microsoft Azure Premier Support-Stunden angewendet werden.
> - Sie können den Schweregrad des Falls nicht ändern.
> - Der Microsoft-Support hilft Ihnen bei diesen Beratungsfällen während der regulären wöchentlichen Geschäftszeiten.

## <a name="plan"></a>Plan

- Die Hierarchie muss aus dem CAS und einem einzelnen untergeordneten primären Standort bestehen. Der primäre Standort kann über sekundäre Standorte verfügen. Sehen Sie sich die Planungsschritte und Voraussetzungen für das [Deinstallieren eines primären Standorts](uninstall-sites-and-hierarchies.md#bkmk_primary) an, um weitere untergeordnete primäre Standorte aus der Hierarchie zu entfernen.

- Sorgen Sie dafür, dass Ihr untergeordneter primärer Standort den Größen- und Skalierungsanforderungen eines [eigenständigen primären Standorts](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri) entspricht.

- Verschieben Sie Standortrollen am CAS, oder ziehen Sie sie zurück, mit Ausnahme des Dienstverbindungspunkts und des Softwareupdatepunkts. Das Configuration Manager-Setup übernimmt diese beiden Rollen, wenn Sie den CAS entfernen.

  Die folgenden Rollen werden am CAS am häufigsten verwendet. Ziehen Sie diese Rollen zurück, oder verschieben Sie sie zum primären Standort:

  - Asset Intelligence-Synchronisierungspunkt
  - Endpoint Protection-Punkt
  - Reporting Services-Punkt
  - Data Warehouse-Dienstpunkt
  - Cloudverwaltungsgateway (Cloud Management Gateway, CMG)

    > [!NOTE]
    > Wenn Sie das CMG für Inhalte aktiviert haben, planen Sie die Neuverteilung des Inhalts, nachdem Sie das CMG am primären Standort neu erstellt haben.<!-- 6608659 -->

- Deaktivieren verteilter Ansichten

- Configuration Manager verarbeitet Quellstandorte für integrierte Pakete automatisch, z. B. den Konfigurations-Manager-Client. Sehen Sie sich die anderen Inhaltsquellstandorte an, um dafür zu sorgen, dass sie keine Freigabe am CAS verwenden.

- Halten Sie alle aktiven Migrationsaufträge an, und entfernen Sie alle Migrationskonfigurationen. Weitere Informationen finden Sie unter [Beenden der aktiven Migration aus einer anderen Hierarchie](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Wenn Sie Regeln für die automatische Bereitstellung für Softwareupdates verwenden, erstellen Sie sie für den untergeordneten primären Standort neu.

- Wenn Sie Configuration Manager oder System Center Updates Publisher verwenden, um [Softwareupdates von Drittanbietern](../../../../sum/deploy-use/third-party-software-updates.md) zu verwalten, exportieren Sie die WSUS-Signaturzertifikate vom Softwareupdatepunkt zum CAS.

  - Bevor Sie den CAS entfernen, sollten Sie gegebenenfalls die Fristen für erforderliche Bereitstellungen von Softwareupdates von Drittanbietern abwarten. Clients laden Inhalte für erforderliche Bereitstellungen vorab herunter, und wenn Sie den Softwareupdatepunkt ändern, ändert sich der Inhaltshashwert mit der *lokalen Veröffentlichung* von Softwareupdates. (Dieses Verhalten hat keinen Einfluss auf andere Inhaltstypen, nur auf die lokale Veröffentlichung von Softwareupdates von Drittanbietern.) Wenn Sie den CAS entfernen, während diese erforderlichen Bereitstellungen noch nicht abgeschlossen sind, schlagen sie auf Clients aufgrund des Fehlers eines nicht übereinstimmenden Hashwerts fehl.

- Sehen Sie sich gegebenenfalls Drittanbietersoftware an, die eine Abhängigkeit vom CAS aufweisen könnte.

## <a name="prerequisites"></a>Voraussetzungen

- Der Administrator, der das Configuration Manager-Setup ausführt, muss über die folgenden Sicherheitsrechte verfügen:

  - **Lokale Administratorrechte** auf dem CAS-Server

  - **Lokale Administratorrechte** für den CAS-Datenbankserver des Remotestandorts, wenn sich der CAS-Datenbankserver nicht auf dem Standortserver befindet

  - **Systemadministratorrechte** für die Datenbank des CAS

  - **Lokale Administratorrechte** auf dem primären Standortserver

  - **Lokale Administratorrechte** für den Datenbankserver des Remotestandorts, wenn sich der Datenbankserver des primären Standorts nicht auf dem primären Standortserver befindet.

  - **Systemadministratorrechte** für die Datenbank des primären Standorts

  - Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** am CAS und am primären Standort

- Nur ein untergeordneter primärer Standort in der Hierarchie. Weitere Informationen finden Sie unter [Primärer Standort](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Prozess

1. Starten Sie das Configuration Manager-Setup auf dem CAS-Server mithilfe eines der folgenden Verfahren:

    - Klicken Sie im Menü **Start** auf **Setup für Configuration Manager**.

    - Öffnen Sie im Verzeichnis der *Installationsmedien* für Configuration Manager die Datei `\SMSSETUP\BIN\X64\setup.exe`. Stellen Sie sicher, dass diese Version mit der Version des Standorts übereinstimmt.

    - Öffnen Sie in dem Verzeichnis, in dem Configuration Manager *installiert* ist, die Datei `\BIN\X64\setup.exe`.

1. Lesen Sie die Informationen auf der Seite **Vorbereitung**.

1. Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus.

1. Klicken Sie auf der Seite **Standortwartung** auf die Option **Remove central administration site** (Standort der zentralen Verwaltung entfernen). <!-- or is it still "delete"? -->

1. Führen Sie auf der Seite **Vorhandene Standortsystemrollen werden neu konfiguriert** Folgendes aus:

    - **Dienstverbindungspunkt:** Geben Sie den vollqualifizierten Domänenname des Standortsystems am primären Standort ein, um diese erforderliche Rolle zu hosten. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../configure/about-the-service-connection-point.md).

    - **Softwareupdatepunkt:** Wählen Sie einen Softwareupdatepunkt am primären Standort aus. Das Setup konfiguriert diesen Softwareupdatepunkt so, dass dieselbe Synchronisierung durchgeführt wird wie bei der CAS-Konfiguration.

    Das Setup überprüft, ob die angegebenen Server den Voraussetzungen entsprechen. Klicken Sie auf **Installation starten**, wenn Sie bereit sind, fortzufahren.

Wenn beim Setup ein Problem auftritt, verwenden Sie den Assistenten, um zu versuchen, den Prozess erneut auszuführen.

Wenn das Setup abgeschlossen ist, wird der primäre Standort zurückgesetzt. Weitere Informationen finden Sie unter [Ausführen einer Standortrücksetzung](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>Überwachen und Überprüfen

Sehen Sie sich die folgenden Protokolle während des Setupprozesses an:

- `C:\ConfigMgrSetup.log` auf dem CAS-Server

- **hman.log** im Configuration Manager-Protokollverzeichnis auf dem Server des primären Standorts

Verwenden Sie den Knoten **Standorthierarchie** im Arbeitsbereich **Überwachung**, um die Änderungen an der Hierarchie visuell darzustellen. Die folgende Abbildung zeigt beispielsweise einen Vergleich der Hierarchie vom **SHY**-CAS, dem primären **HAW**-Standort und dem sekundären **VWT**-Standort, bevor und nachdem Änderungen vorgenommen wurden:

| Vorher  | Danach   |
|---------|---------|
|![Beispielansicht einer Standorthierarchie eines CAS, eines primären Standorts und eines sekundären Standorts](media/3607277-cas-primary-secondary.png)|![Beispielansicht einer Standorthierarchie eines primären Standorts und eines sekundären Standorts](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Aufgaben nach dem Setup

Nachdem Sie den CAS entfernt haben, sollten Sie sich die folgenden Schritte ansehen, die gegebenenfalls auf Ihre Umgebung zutreffen.

- Entfernen Sie das Servercomputerkonto des CAS manuell aus den lokalen Gruppen des primären Standorts.

- Der vertrauenswürdige Stammschlüssel wurde geändert. Dies erfordert möglicherweise die folgenden Aktionen:

  - Aktualisieren Sie die Betriebssystembereitstellungsstartimages, sodass die neuesten Configuration Manager-Binärdateien eingeschlossen werden.

  - Erstellen Sie [Betriebssystembereitstellungsmedien](../../../../osd/deploy-use/create-task-sequence-media.md) neu.

- Wenn Sie Configuration Manager mit [Azure Monitor](/azure/azure-monitor/platform/collect-sccm?context=/mem/configmgr/core/context/core-context) verbinden, müssen Sie die Verbindung zurücksetzen. Der erste Schritt für eine Problembehebung ist das [Erneuern des geheimen Schlüssels](../configure/azure-services-wizard.md#bkmk_renew). Wenn dies das Problem nicht behebt, stellen Sie die Verbindung neu her.<!-- 5584635 -->

- Wenn Sie in der Version 2002 die Synchronisierung von Surface-Treibern aktivieren, müssen Sie dieses Feature neu konfigurieren, nachdem Sie den CAS entfernt haben. Weitere Informationen finden Sie im Abschnitt [Microsoft Surface-Treiber und Firmwareupdates](../../../../sum/deploy-use/surface-drivers.md).<!-- 5728727 -->

- Wenn Sie Softwareupdates von Drittanbietern verwalten, ist Folgendes erforderlich:

  1. Exportieren Sie das WSUS-Signaturzertifikat vom Softwareupdatepunkt am CAS, wenn dies nicht bereits geschehen ist.

  1. Bevor Sie neue Bereitstellungen erstellen, entfernen Sie das Update für vorhandene Bereitstellungs- und Softwareupdatepakete.

  1. Synchronisieren Sie abonnierte Kataloge neu, um die Metadaten des Softwareupdates in einen nutzbaren Zustand wiederherzustellen. Sie können auch warten, bis Configuration Manager automatisch eine neue Synchronisierung durchführt.

  1. Starten Sie einen Softwareupdatesynchronisierungsprozess, oder warten Sie auf einen regulär stattfindenden, um Configuration Manager mit dem aktuellen WSUS-Status zu aktualisieren. Verwenden Sie optional die SCUP- oder WSUS-PowerShell-Cmdlets, um Updates zu entfernen und neu hinzuzufügen.

  1. Veröffentlichen Sie Inhalte für Updates neu, die Sie bereitstellen müssen.