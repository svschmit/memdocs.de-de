---
title: Deinstallieren von Standorten
titleSuffix: Configuration Manager
description: Dieser Leitfaden enthält Informationen zum Entfernen von Rollen sowie zum Deinstallieren von Standorten und Hierarchien.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700528"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Deinstallieren von Rollen, Standorten und Hierarchien in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erfahren Sie, wie Sie Standortsystemrollen, Standorte oder Hierarchien in Configuration Manager deinstallieren.

Ab Version 2002 können Sie auch den Standort der zentralen Verwaltung (Central Administration Site, CAS) aus einer Hierarchie entfernen und gleichzeitig den primären Standort beibehalten.

## <a name="site-system-role"></a><a name="bkmk_role"></a> Standortsystemrolle

Aus folgenden Gründen kann es sinnvoll sein, eine Rolle von einem Standortsystemserver zu entfernen:

- Sie nehmen eine größere Infrastrukturänderung vor, z. B. am Netzwerk oder an physischen Standorten.
- Sie setzen den zugrunde liegenden Server außer Betrieb.
- Sie konsolidieren Rollen, um Kosten zu senken und die Komplexität zu verringern.
- Sie konfigurieren oder entwerfen die Standortrollen neu.
- Sie beenden die Verwendung des Features, das die Rolle unterstützt.

Beantworten Sie vor dem Entfernen einer Rolle zunächst die folgenden Fragen:

- Wird die Rolle am Standort noch benötigt? Wenn ja: Ist diese Rolle bereits in einem anderen Standortsystem vorhanden?

- Verfügen die anderen Standortsysteme mit dieser Rolle über ausreichend Kapazität, um Ihre Geschäftsanforderungen hinsichtlich Leistung und Verfügbarkeit zu unterstützen?

- Wurden bereits alle Clients für die Verwendung einer anderen Rolle neu konfiguriert? Verlassen Sie sich auf Standardclientverhalten, um auf einen anderen Server zurückzugreifen oder einen solchen zu ermitteln?

### <a name="procedure-to-remove-a-site-system-role"></a>Vorgehensweise zum Entfernen einer Standortsystemrolle

Gehen Sie folgendermaßen vor, um eine Rolle zu entfernen:

1. Wechseln Sie in der **Configuration Manager**-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie anschließend auf den Knoten **Server und Standortsystemrollen**.

1. Wählen Sie den Standortsystemserver mit der Rolle aus, die Sie entfernen möchten. Wählen Sie im Detailbereich **Standortsystemrollen** die Zielrolle aus.

1. Klicken Sie im Menüband auf der Registerkarte **Standortrolle** in der Gruppe **Standortrolle** auf **Rolle entfernen**. Bestätigen Sie, dass Sie die Rolle entfernen möchten.

### <a name="additional-information-for-specific-roles"></a>Zusätzliche Informationen zu bestimmten Rollen

Einige Rollen erfordern möglicherweise zusätzliche Schritte und Überlegungen.

#### <a name="software-update-point"></a>Softwareupdatepunkt

Nachdem Sie den Softwareupdatepunkt entfernt haben, aktualisiert Configuration Manager die Clientrichtlinie, um den Softwareupdatepunkt aus der Liste zu entfernen. Wenn Sie den letzten Softwareupdatepunkt des Standorts entfernen, enthält die Liste der Softwareupdatepunkte keine Einträge mehr. Ohne verfügbare Rollen ist die Verwaltung von Softwareupdates am Standort praktisch deaktiviert.

Wählen Sie einen anderen Softwareupdatepunkt an diesem Standort als neue Synchronisierungsquelle aus, wenn an einem primären Standort mehr als ein Softwareupdatepunkt vorhanden ist und Sie den Softwareupdatepunkt entfernen, der die Synchronisierungsquelle darstellt.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a> Sekundärer Standort  

Im Gegensatz zur [Außerbetriebsetzung einer Hierarchie](#bkmk_hierarchy) besteht der Hauptgrund für das Entfernen eines sekundären Standorts in einer größeren Änderung der Infrastruktur, wie etwa des Netzwerks oder physischer Standorte. Überprüfen Sie zudem die Gründe für die [Verwendung eines sekundären Standorts](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

Beantworten Sie vor dem Entfernen eines sekundären Standorts zunächst die folgenden Fragen:

- Haben Sie alle Standortsystemrollen vom Standortserver entfernt?

- Sind dem sekundären Standort Grenzen oder Begrenzungsgruppen zugeordnet? Konfigurieren Sie die Standortgrenzen neu, bevor Sie den Standort entfernen.

- Befinden sich am Standort noch Clients?

- Haben Sie andere Optionen für die Inhaltsverwaltung wie [Peercaching](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies) konfiguriert?

### <a name="options-to-delete-secondary-sites"></a>Optionen zum Löschen sekundärer Standorte

Sie können einen sekundären Standort nicht an einen anderen primären Standort verschieben oder diesem neu zuweisen. Wenn Sie einen sekundären Standort vom direkt übergeordneten Standort entfernen möchten, müssen Sie ihn deinstallieren oder löschen.

#### <a name="uninstall-the-secondary-site"></a>Deinstallieren des sekundären Standorts

Mit dieser Option können Sie einen funktionsfähigen sekundären Standort entfernen, auf den über das Netzwerk zugegriffen werden kann. Mit dieser Option wird Configuration Manager vom Server des sekundären Standorts deinstalliert. Anschließend werden alle Informationen über den Standort und dessen Ressourcen vom Configuration Manager-Standort gelöscht.

Wurde SQL Server Express für den sekundären Standort installiert, deinstalliert Configuration Manager auch SQL Server Express. Wurde SQL Server Express vor der Installation des sekundären Standorts installiert, wird SQL Server Express von Configuration Manager nicht deinstalliert.

#### <a name="delete-the-secondary-site"></a>Löschen des sekundären Standorts

Verwenden Sie diese Option in den folgenden Situationen:

- Bei der Installation tritt ein Fehler auf.

- Nach der Deinstallation wird der sekundäre Standort weiterhin in der Configuration Manager-Konsole angezeigt.

    Mit dieser Option werden alle Informationen über den Standort und dessen Ressourcen aus der Configuration Manager-Hierarchie gelöscht. Es werden jedoch keine Änderungen auf dem Standortserver vorgenommen.

    > [!TIP]
    >  Ein sekundärer Standort kann auch mit der Option **/DELSITE** des Hierarchieverwaltungstools gelöscht werden. Weitere Informationen finden Sie unter [Hierarchieverwaltungstool (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>Voraussetzungen für das Löschen eines sekundären Standorts

Der Administrator, der das Configuration Manager-Setup ausführt, muss über die folgenden Sicherheitsrechte verfügen:

- Lokale **Administrator**rechte auf dem sekundären Standortserver

- **Lokale Administratorrechte** für den Datenbankserver des Remotestandorts, wenn sich der Datenbankserver des primären Standorts nicht auf dem primären Standortserver befindet.

- Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** am übergeordneten primären Standort

- **Systemadministratorrechte** für die Datenbank des sekundären Standorts

### <a name="procedure-to-delete-a-secondary-site"></a>Vorgehensweise zum Löschen eines sekundären Standorts

Gehen Sie folgendermaßen vor, um einen sekundären Standort zu deinstallieren oder zu löschen:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Standortkonfiguration**, und klicken Sie dann auf den Knoten **Standorte**.

1. Wählen Sie den sekundären Standortserver aus, der entfernt werden soll. Klicken Sie im Menüband auf der Registerkarte **Start** in der Gruppe **Standort** auf **Löschen**.

1. Wählen Sie auf der Seite **Allgemein** aus, ob der sekundäre Standort deinstalliert oder gelöscht werden soll.

1.  Schließen Sie den Assistenten ab.

## <a name="primary-site"></a><a name="bkmk_primary"></a> Primärer Standort  

Aus folgenden Gründen kann es sinnvoll sein, einen primären Standort aus der Hierarchie zu deinstallieren:

- Sie konsolidieren Standorte, um Kosten zu senken und die Komplexität zu verringern.
- Sie konfigurieren oder entwerfen die Standorte der Hierarchie neu.

Deaktivieren Sie die [verteilten Ansichten](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) in der Hierarchie, bevor Sie einen untergeordneten primären Standort deinstallieren, für dessen Replikationslink zum Standort der zentralen Verwaltung (CAS) verteilte Ansichten verwendet werden. Weitere Informationen finden Sie unter [Deinstallieren eines primären Standorts, der mit verteilten Ansichten konfiguriert ist](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a> Planung für die Deinstallation eines primären Standorts

Überprüfen Sie vor der Deinstallation eines primären Standorts folgende Punkte:

- Überprüfen Sie die Standortgrenzen, Begrenzungsgruppen und Fallbackbeziehungen. Wenn Sie Clients einem neuen Standort zuweisen, ohne die Standortgrenzen zu ändern, wird dies möglicherweise als Roaming angesehen. Weitere Informationen finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen](../configure/define-site-boundaries-and-boundary-groups.md).

- Stellen Sie sicher, dass alle aktiven Clients einem anderen primären Standort in der Hierarchie neu zugewiesen werden. Andernfalls werden die Clients nach der Deinstallation des Standorts nicht mehr verwaltet. Weitere Informationen finden Sie unter [Zuweisen von Clients zu einem Standort](../../../clients/deploy/assign-clients-to-a-site.md).

  - Überprüfen Sie die Liste der Standortrollen, um sicherzustellen, dass der neue Standort dasselbe Servicelevel bereitstellt.

  - Stellen Sie sicher, dass die anderen Standortsysteme mit dieser Rolle am neuen Standort über ausreichend Kapazität verfügen. Diese müssen in der Lage sein, Ihre Geschäftsanforderungen hinsichtlich Leistung und Verfügbarkeit mit den zusätzlichen Clients zu unterstützen.

  - Verfügt dieser Standort über eine große Anzahl von Clients, führen Sie die Neuzuweisung in Phasen aus. Überwachen Sie die Datenbankreplikation bei der Aktualisierung der vollständigen Inventur und anderer standortspezifischer Daten durch die Clients. Bei der Verwaltung von Softwareupdates werden die Clients einem neuen Softwareupdatepunkt zugewiesen. Dieses Verhalten führt zu einer vollständigen Überprüfung der Kompatibilität von Updates.

  - Die Neuzuweisung von Clients wirkt sich möglicherweise auf Berichte und Abfragen aus, die auf Inventurdaten und zustandsbasierter Kompatibilität basieren. Erwägen Sie daher während des Übergangs eine vorübergehende Anpassung aller Clientzyklen.

  - Überprüfen Sie alle Zuweisungsmethoden für Clients, um sicherzustellen, dass keine auf diesen primären Standort verweist.

- Überprüfen Sie, ob aktiv verwendete Objekte in der Hierarchie statische Verweise auf den Standortcode aufweisen. Dazu zählen Sammlungsabfragen, Tasksequenzen oder administrative Skripts.

- Verwendet die Hierarchie einen [Fallbackstandort](../configure/boundary-group-procedures.md#bkmk_site-fallback) für die automatische Standortzuweisung, stellen Sie sicher, dass nicht auf diesen primären Standort verwiesen wird.

- Konfigurieren Sie alle [Clientinstallationsmethoden](../../../clients/deploy/plan/client-installation-methods.md) neu, die möglicherweise auf einen statischen Standortcode verweisen.

- Sollte der primäre Standort über standortspezifische cloudgestützte Dienste verfügen, entfernen Sie diese. Wenn Sie diese Cloudressourcen weiterhin benötigen, verschieben Sie sie an einen anderen primären Standort in der Hierarchie. Entfernen Sie die Dienste vom primären Standort, den Sie deinstallieren möchten, und fügen Sie sie einem anderen primären Standort hinzu.

- Verfügt der primäre Standort über [Ermittlungsmethoden](../configure/run-discovery.md) für die Hierarchie, verschieben Sie diese an einen anderen Standort.

- Setzen Sie alle standortbasierten [Medien für die Bereitstellung des Betriebssystems](../../../../osd/deploy-use/create-task-sequence-media.md) außer Kraft.

- Deinstallieren Sie alle Standortsystemrollen vom Standort und Standortserver. Weitere Informationen finden Sie unter [Deinstallieren von Standortsystemrollen](#bkmk_role). Dieser Vorbereitungsschritt ist zwar nicht erforderlich, doch mit ihm können Sie vor der Deinstallation des Standorts zusätzliche Abhängigkeiten identifizieren.

- Deinstallieren Sie alle sekundären Standorte unter diesem primären Standort. Weitere Informationen hierzu finden Sie im Abschnitt [Sekundärer Standort](#bkmk_secondary).

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a> Voraussetzungen für das Deinstallieren eines primären Standorts

Der Administrator, der das Configuration Manager-Setup ausführt, muss über die folgenden Sicherheitsrechte verfügen:

- **Lokale Administratorrechte** auf dem CAS-Server

- **Lokale Administratorrechte** für den CAS-Datenbankserver des Remotestandorts, wenn sich der CAS-Datenbankserver nicht auf dem Standortserver befindet

- **Systemadministratorrechte** für die Datenbank des CAS

- **Lokale Administratorrechte** auf dem primären Standortserver

- **Lokale Administratorrechte** für den Datenbankserver des Remotestandorts, wenn sich der Datenbankserver des primären Standorts nicht auf dem primären Standortserver befindet.

- Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** für den Standort der zentralen Verwaltung

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a> Vorgehensweise zum Deinstallieren eines primären Standorts

Führen Sie das Configuration Manager-Setup aus, um einen primären Standort zu deinstallieren, dem kein sekundärer Standort zuwiesen ist. Gehen Sie folgendermaßen vor, um einen primären Standort zu deinstallieren:

> [!TIP]
> Sollte der primäre Standortserver nicht mehr verfügbar sein, verwenden Sie zum Löschen des primären Standorts aus der Standortdatenbank das Hierarchieverwaltungstool am Standort der zentralen Verwaltung. Weitere Informationen finden Sie unter [Hierarchieverwaltungstool (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Starten Sie das Configuration Manager-Setup auf dem primären Standortserver, indem Sie einen der folgenden Schritte ausführen:

    - Klicken Sie im Menü **Start** auf **Setup für Configuration Manager**.

    - Öffnen Sie im Verzeichnis der *Installationsmedien* für Configuration Manager die Datei `\SMSSETUP\BIN\X64\setup.exe`. Stellen Sie sicher, dass diese Version mit der Version des Standorts übereinstimmt.

    - Öffnen Sie in dem Verzeichnis, in dem Configuration Manager *installiert* ist, die Datei `\BIN\X64\setup.exe`.

1. Lesen Sie die Informationen auf der Seite **Vorbereitung**.

1. Wählen Sie auf der Seite **Erste Schritte** die Option **Configuration Manager-Standort deinstallieren** aus.

    > [!IMPORTANT]  
    >  Wenn dem primären Standort ein sekundärer Standort zugeordnet ist, müssen Sie den sekundären Standort entfernen, bevor Sie den primären Standort deinstallieren können.  

1. Auf der Seite **Configuration Manager-Standort deinstallieren** sind die beiden folgenden Optionen standardmäßig aktiviert:

    - Standortdatenbank vom primären Standortserver entfernen
    - Configuration Manager-Konsole entfernen

1. Klicken Sie auf **Ja**, um zu bestätigen, dass der primäre Configuration Manager-Standort deinstalliert werden soll.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a> Deinstallieren eines primären Standorts, der die verteilten Ansichten verwendet

1. Deaktivieren Sie vor der Deinstallation eines untergeordneten primären Standorts die verteilten Ansichten für alle Links der Hierarchie zwischen dem Standort der zentralen Verwaltung und einem primären Standort.

1. Stellen Sie nach der Deaktivierung der verteilten Ansichten für alle Links sicher, dass die Neuinitialisierung der Daten des primären Standorts am Standort der zentralen Verwaltung ausgeführt wurde. Informationen zur Überwachung der Dateninitialisierung finden Sie unter [Überwachen der Replikation](../../manage/monitor-replication.md).

1. Nachdem die Daten am Standort der zentralen Verwaltung neu initialisiert wurden, können Sie den [primären Standort deinstallieren](#bkmk_pri-process).

1. Nach der Deinstallation des primären Standorts können Sie die verteilten Ansichten für Links vom Standort der zentralen Verwaltung zu anderen primären Standorten neu konfigurieren.

    > [!IMPORTANT]
    > Wenn Sie den primären Standort vor dem Deaktivieren der verteilten Ansichten an allen Standorten oder vor der erfolgreichen Neuinitialisierung der Daten am Standort der zentralen Verwaltung deinstallieren, kann bei der Replikation der Daten ein Fehler auftreten.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a> Außer Betrieb setzen einer Hierarchie

Manche Organisationen verfügen aufgrund von Fusionen, Übernahmen, Testumgebungen oder anderen Geschäftsanforderungen über mehrere Hierarchien. Durch Konsolidieren der Verwaltung in einer einzelnen Hierarchie können Kosten gesenkt und die Komplexität verringert werden. Ein weiterer Aspekt, der für die Außerbetriebsetzung einer Hierarchie spricht, ist die Tatsache, dass Sie zu einem reinen Cloudverwaltungsdienst migrieren (wie etwa Microsoft Intune) und daher die Bereitschaft, Ihre lokale Infrastruktur zu entfernen, bereits vorhanden ist.

Um eine Hierarchie mit mehreren Standorten aufzuheben, müssen die Standorte in einer bestimmten Reihenfolge entfernt werden. Beginnen Sie bei der Deinstallation von Standorten am unteren Ende der Hierarchie, und arbeiten Sie sich zum oberen Ende vor:

1. Entfernen Sie die mit den primären Standorten verbundenen sekundären Standorte.
2. Deinstallieren Sie die primären Standorte.
3. Wenn Sie alle primären Standorte deinstalliert haben, können Sie den Standort der zentralen Verwaltung deinstallieren.

Weitere Informationen finden Sie in den folgenden Abschnitten:

- [Entfernen eines sekundären Standorts](#bkmk_secondary)
- [Deinstallieren eines primären Standorts](#bkmk_primary)
- [Deinstallieren des Standorts der zentralen Verwaltung](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a> Deinstallieren des Standorts der zentralen Verwaltung

Der letzte Schritt der Außerbetriebsetzung einer Hierarchie ist die Deinstallation des Standorts der zentralen Verwaltung (Central Administration Site, CAS). Verfügt der Standort der zentralen Verwaltung über keine untergeordneten primären Standorte, führen Sie für die CAS-Deinstallation das Configuration Manager-Setup aus.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Voraussetzungen für das Deinstallieren des Standorts der zentralen Verwaltung

Der Administrator, der das Configuration Manager-Setup ausführt, muss über die folgenden Sicherheitsrechte verfügen:

- **Lokale Administratorrechte** auf dem CAS-Server

- **Lokale Administratorrechte** für den CAS-Datenbankserver des Remotestandorts, wenn sich der CAS-Datenbankserver nicht auf dem Standortserver befindet

#### <a name="procedure-to-uninstall-the-cas"></a>Vorgehensweise zum Deinstallieren des Standorts der zentralen Verwaltung

1. Starten Sie das Configuration Manager-Setup auf dem CAS-Server, indem Sie einen der folgenden Schritte ausführen:

    - Klicken Sie im Menü **Start** auf **Setup für Configuration Manager**.

    - Öffnen Sie im Verzeichnis der *Installationsmedien* für Configuration Manager die Datei `\SMSSETUP\BIN\X64\setup.exe`. Stellen Sie sicher, dass diese Version mit der Version des Standorts übereinstimmt.

    - Öffnen Sie in dem Verzeichnis, in dem Configuration Manager *installiert* ist, die Datei `\BIN\X64\setup.exe`.

1. Lesen Sie die Informationen auf der Seite **Vorbereitung**.

1. Wählen Sie auf der Seite **Erste Schritte** die Option **Configuration Manager-Standort deinstallieren** aus.

    > [!IMPORTANT]  
    >  Entfernen Sie vor der CAS-Deinstallation alle untergeordneten primären Standorte.  

1. Auf der Seite **Configuration Manager-Standort deinstallieren** sind die beiden folgenden Optionen standardmäßig aktiviert:

    - Standortdatenbank vom CAS-Server entfernen
    - Configuration Manager-Konsole entfernen

1. Klicken Sie auf **Ja**, um zu bestätigen, dass der Configuration Manager-Standort der zentralen Verwaltung (CAS) deinstalliert werden soll.

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a> Entfernen des Standorts der zentralen Verwaltung

<!-- 3607277 -->

Wenn Ihre Hierarchie aus dem Standort der zentralen Verwaltung und einem einzelnen untergeordneten primären Standort besteht, können Sie ab Version 2002 den Standort der zentralen Verwaltung entfernen. Dadurch wird Ihre Configuration Manager-Infrastruktur vereinfacht und auf einen einzelnen, eigenständigen primären Standort reduziert. Die komplexe Replikation zwischen Standorten wird beseitigt, und Ihre Verwaltungsaufgaben werden an einem einzelnen Standort zusammengeführt.

Weitere Informationen finden Sie unter [Entfernen des Standorts der zentralen Verwaltung](remove-central-administration-site.md).
