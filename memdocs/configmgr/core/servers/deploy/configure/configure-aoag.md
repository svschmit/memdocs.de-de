---
title: Konfigurieren von Verfügbarkeitsgruppen
titleSuffix: Configuration Manager
description: Einrichten und Verwalten von SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12753b3800b3b304bd13c992b57d22bf9e1bfad8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704798"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Konfigurieren von SQL Server AlwaysOn-Verfügbarkeitsgruppen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Artikel zum Konfigurieren und Verwalten der Verfügbarkeitsgruppen, die Sie mit Configuration Manager verwenden.

Vorbereitung:  

- Machen Sie sich mit den Informationen unter [Vorbereiten der Verwendung von SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md) vertraut.
- Machen Sie sich mit der SQL Server-Dokumentation vertraut, die die Verwendung von Verfügbarkeitsgruppen und damit verbundener Verfahren behandelt. Diese Informationen ist erforderlich, um die folgenden Szenarios abzuschließen.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Erstellen und Konfigurieren einer Verfügbarkeitsgruppe

Verwenden Sie das folgende Verfahren zum Erstellen einer Verfügbarkeitsgruppe, und verschieben Sie dann eine Kopie der Standortdatenbank in diese Verfügbarkeitsgruppe.

1. Verwenden Sie den folgenden Befehl, um den Configuration Manager-Standort zu beenden:

    `preinst.exe /stopsite`

    Weitere Informationen finden Sie unter [Hierarchiewartungstool](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Ändern Sie das Sicherungsmodell der Standortdatenbank von **EINFACH** in **VOLLSTÄNDIG**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Verfügbarkeitsgruppen unterstützen nur das Sicherungsmodell VOLLSTÄNDIG. Weitere Informationen finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Verwenden Sie SQL Server, um eine vollständige Sicherung Ihrer Standortdatenbank zu erstellen. Wählen Sie eine der folgenden Optionen aus:

    - **Soll ein Mitglied der Verfügbarkeitsgruppe sein:** Wenn Sie diesen Server als das anfängliche primäre Replikationsmitglied der Verfügbarkeitsgruppe verwenden, müssen Sie keine Kopie der Standortdatenbank auf diesem oder einem anderen Server in der Gruppe wiederherstellen. Die Datenbank ist bereits auf dem primären Replikat vorhanden. SQL Server repliziert die Datenbank in einem späteren Schritt auf den sekundären Replikaten.  

    - **Soll kein Mitglied der Verfügbarkeitsgruppe sein:** Stellen Sie eine Kopie der Standortdatenbank auf dem Server wieder her, der das primäre Replikat der Gruppe hosten soll.

    Weitere Informationen finden Sie in den folgenden Artikeln der SQL Server-Dokumentation:

    - [Erstellen einer vollständigen Datenbanksicherung](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Wiederherstellen einer Datenbanksicherung mit SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Wenn Sie beabsichtigen, von einer Verfügbarkeitsgruppe zu einer eigenständigen Version auf einem vorhandenen Replikat zu wechseln, entfernen Sie zuerst die Datenbank aus der Verfügbarkeitsgruppe.

4. Verwenden Sie auf dem Server, auf dem das anfängliche primäre Replikat der Gruppe gehostet wird, den [Assistenten für neue Verfügbarkeitsgruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) zum Erstellen der Verfügbarkeitsgruppe. Gehen Sie im Assistenten so vor:

    - Wählen Sie auf der Seite **Datenbank auswählen** die Datenbank für Ihren Configuration Manager-Standort aus.  

    - Konfigurieren Sie auf der Seite **Replikate angeben** Folgendes:

        - **Replikate:** Geben Sie die Server an, die als Host für die sekundären Replikate fungieren sollen.

        - **Listener:** Geben Sie den **DNS-Namen des Listeners** als vollständigen DNS-Namen an. Beispiel: `<listener_server>.fabrikam.com`. Wenn Sie Configuration Manager für die Verwendung der Datenbank in der Verfügbarkeitsgruppe konfigurieren, wird dieser Name verwendet.

    - Wählen Sie auf der Seite **Anfängliche Datensynchronisierung auswählen** die Einstellung **Vollständig**aus. Nachdem der Assistent die Verfügbarkeitsgruppe erstellt hat, sichert er die primäre Datenbank und das Transaktionsprotokoll. Anschließend stellt der Assistent diese auf jedem Server wieder her, auf dem ein sekundäres Replikat gehostet wird.

        > [!Note]  
        > Wenn Sie diesen Schritt nicht ausführen, stellen Sie eine Kopie der Standortdatenbank auf jedem Server wieder her, auf dem ein sekundäres Replikat gehostet wird. Verknüpfen Sie dann manuell diese Datenbank mit der Gruppe.

5. Überprüfen Sie die Konfiguration auf jedem Replikat:

    1. Stellen Sie sicher, dass das Computerkonto des Standortservers Mitglied der lokalen Gruppe **Administratoren** auf allen Computern ist, die zur Verfügbarkeitsgruppe gehören.  

    2. Führen Sie das [Überprüfungsskript](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) aus, um sicherzustellen, dass die Standortdatenbank auf jedem Replikat ordnungsgemäß konfiguriert ist.

    3. Wenn auf sekundären Replikaten Konfigurationen festgelegt werden müssen, führen Sie manuell ein Failover des primären Replikats auf das sekundäre Replikat aus, bevor Sie fortfahren. Sie können nur die Datenbank eines primären Replikats konfigurieren. Weitere Informationen finden Sie unter [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) in der SQL Server-Dokumentation.

6. Wenn alle Replikate die Anforderungen erfüllen, kann die Verfügbarkeitsgruppe mit Configuration Manager verwendet werden.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Konfigurieren eines Standorts für die Verwendung der Verfügbarkeitsgruppe

Nachdem Sie [die Verfügbarkeitsgruppe erstellt und konfiguriert haben](#bkmk_create), verwenden Sie die Configuration Manager-Standortwartung, um den Standort für die Verwendung der Datenbank zu konfigurieren, die von der Verfügbarkeitsgruppe gehostet wird.

Das Installieren eines neuen Standorts mit einer Datenbank in einer Verfügbarkeitsgruppe wird nicht unterstützt. Wenn Sie beispielsweise Baseline-Medien verwenden, installieren Sie den Standort mit einer einzigen Instanz von SQL Server. Verschieben Sie nach der Installation des Standorts die Standortdatenbank in die Verfügbarkeitsgruppe.

1. Führen Sie das **Configuration Manager-Setup** über `\BIN\X64\setup.exe` im Installationsordner des Configuration Manager-Standorts aus.

2. Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus, und wählen Sie dann **Weiter** aus.

3. Wählen Sie **SQL Server-Konfiguration ändern** aus, und klicken Sie anschließend auf **Weiter**.

4. Konfigurieren Sie die folgenden Einstellungen für die Standortdatenbank neu:

    - **SQL Server-Name:** Geben Sie den virtuellen Namen für den *Verfügbarkeitsgruppenlistener* ein. Sie haben den Listener beim Erstellen der Verfügbarkeitsgruppe konfiguriert. Der virtuelle Name muss ein vollständiger DNS-Name wie `<Listener_Server>.fabrikam.com` sein.  

    - **Instanz:** Dieser Wert muss leer sein, um die Standardinstanz für den *Listener* der Verfügbarkeitsgruppe anzugeben. Wenn die aktuelle Standortdatenbank auf einer benannten Instanz ausgeführt wird, löschen Sie die aktuelle benannte Instanz.

    - **Datenbank:** Lassen Sie den angezeigten Namen unverändert. Dies ist der Name der aktuellen Standortdatenbank.

5. Nachdem Sie die Informationen zum neuen Speicherort der Datenbank bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Synchrone Replikationsmitglieder  

Wenn die Standortdatenbank in einer Verfügbarkeitsgruppe gehostet wird, verwenden Sie die folgenden Verfahren, um synchrone Replikationsmitglieder hinzuzufügen oder zu entfernen. Weitere Informationen zum unterstützten Typ und der unterstützten Anzahl von Replikaten finden Sie unter [Konfigurationen von Verfügbarkeitsgruppen](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> Hinzufügen eines neuen synchronen Replikationsmitglieds

<!--3127336-->
Ab Version 1906 führen Sie das Configuration Manager-Setup aus, um ein neues synchrones Replikationsmitglied hinzuzufügen.

1. Fügen Sie ein sekundäres Replikat mit SQL Server-Prozeduren hinzu.

    1. [Hinzufügen eines sekundären Replikats zu einer Always On-Verfügbarkeitsgruppe](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Betrachten Sie den Status in SQL Server Management Studio. Warten Sie, bis die vollständige Integrität der Verfügbarkeitsgruppe wieder erreicht wurde.

1. Führen Sie das Configuration Manager-Setup aus, und wählen Sie die Option zum Ändern des Standorts aus.

1. Geben Sie den Namen des Verfügbarkeitsgruppenlisteners als Datenbanknamen an. Wenn der Listener einen nicht standardmäßigen Netzwerkport verwendet, geben Sie diesen ebenfalls an. Diese Aktion veranlasst Setup sicherzustellen, dass jeder Knoten entsprechend konfiguriert ist. Außerdem wird dadurch ein Wiederherstellungsprozess für die Datenbank gestartet.

Das Configuration Manager-Setup verwendet den Vorgang zum Verschieben von SQL-Datenbanken und stellt sicher, dass die Knoten ordnungsgemäß konfiguriert sind.

Weitere Informationen zum manuellen Ausführen dieses Vorgangs in Version 1902 oder früher finden Sie unter [ConfigMgr 1702: Adding a new node (Secondary Replica) to an existing SQL AO AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960) (Hinzufügen eines neuen Knotens [sekundäres Replikat] zu einer vorhandenen SQL AO AG).

### <a name="remove-a-replica-member"></a>Entfernen eines Replikationsmitglieds

Ab Version 1906 können Sie ein Replikationsmitglied mithilfe von Configuration Manager-Setup entfernen. Verwenden Sie denselben Vorgang wie zum [Hinzufügen eines neuen synchronen Replikationsmitglieds](#bkmk_sync-add).

Weitere Informationen zum manuellen Ausführen dieses Vorgangs in Version 1902 oder früher finden Sie unter [Remove a secondary replica from an availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) (Entfernen eines sekundären Replikats aus einer Verfügbarkeitsgruppe).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Asynchrone Replikate

Sie können ein asynchrones Replikat in der mit Configuration Manager verwendeten Verfügbarkeitsgruppe verwenden. Sie müssen nicht die Konfigurationsskripts ausführen, die zum Konfigurieren eines synchronen Replikats benötigt werden, da ein asynchrones Replikat für die Standortdatenbank nicht unterstützt wird.

### <a name="configure-an-asynchronous-commit-replica"></a>Konfigurieren eines Replikats mit asynchronem Commit

Weitere Informationen finden Sie unter [Add a secondary replica to an availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server) (Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Wiederherstellen Ihres Standorts mithilfe des asynchronen Replikats

Sie können Ihren Standort mithilfe des asynchronen Replikats wiederherstellen.

1. Beenden Sie den aktiven primären Standort, um weitere Schreibvorgänge in die Standortdatenbank zu verhindern. Beenden Sie den Standort mit dem [Hierarchiewartungstool](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. Verwenden Sie nach dem Beenden des Standorts das asynchrone Replikat anstelle einer [manuell wiederhergestellten Datenbank](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> Beenden der Verwendung einer Verfügbarkeitsgruppe

Führen Sie das folgende Verfahren aus, wenn Sie Ihre Standortdatenbank nicht mehr in einer Verfügbarkeitsgruppe hosten möchten. Mit diesem Verfahren verschieben Sie die Standortdatenbank wieder auf eine einzelne Instanz von SQL Server.

1. Beenden Sie den Configuration Manager-Standort mithilfe des folgenden Befehls: `preinst.exe /stopsite`. Weitere Informationen finden Sie unter [Hierarchiewartungstool](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Verwenden Sie SQL Server, um eine vollständige Sicherung Ihrer Standortdatenbank anhand des primären Replikats zu erstellen. Weitere Informationen finden Sie unter [Erstellen einer vollständigen Datenbanksicherung](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Verwenden Sie SQL Server, um die Sicherung der Standortdatenbank auf dem Server wiederherzustellen, der die Standortdatenbank hostet. Weitere Informationen finden Sie unter [Wiederherstellen einer Datenbanksicherung mit SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Wenn der Server mit dem primären Replikat für die Verfügbarkeitsgruppe die einzelne Instanz der Standortdatenbank hostet, überspringen Sie diesen Schritt.

4. Ändern Sie auf dem Server, auf dem die Standortdatenbank gehostet wird, das Sicherungsmodell für die Standortdatenbank von **VOLLSTÄNDIG** in **EINFACH**. Weitere Informationen finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Führen Sie das **Configuration Manager-Setup** über `\BIN\X64\setup.exe` im Installationsordner des Configuration Manager-Standorts aus.

6. Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus, und wählen Sie dann **Weiter** aus.  

7. Wählen Sie **SQL Server-Konfiguration ändern** aus, und klicken Sie anschließend auf **Weiter**.  

8. Konfigurieren Sie die folgenden Einstellungen für die Standortdatenbank neu:

    - **SQL Server-Name:** Geben Sie den Namen des Servers ein, auf dem nun die Standortdatenbank gehostet wird.

    - **Instanz:** Geben Sie die benannte Instanz an, von der die Standortdatenbank gehostet wird. Wenn sich die Datenbank auf der Standardinstanz befindet, lassen Sie dieses Feld leer.

    - **Datenbank:** Lassen Sie den angezeigten Namen unverändert. Dies ist der Name der aktuellen Standortdatenbank.

9. Nachdem Sie die Informationen zum neuen Speicherort der Datenbank bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab. Nach Abschluss des Setups wird der Standort neu gestartet und beginnt mit der Nutzung des neuen Speicherorts der Datenbank.

10. Zur Bereinigung der Server, die Mitglied der Verfügbarkeitsgruppe waren, befolgen Sie die Anleitung unter [Entfernen einer Verfügbarkeitsgruppe](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).
