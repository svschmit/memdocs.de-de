---
title: Wartung für Softwareupdates
titleSuffix: Configuration Manager
description: Um die Softwareupdates in Configuration Manager zu gewährleisten, können Sie den WSUS-Bereinigungstask planen oder manuell ausführen.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 560b432bb90f99207fd15bc07e7aff98ffd59ebf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703008"
---
# <a name="software-updates-maintenance"></a>Wartung für Softwareupdates

*Gilt für: Configuration Manager (Current Branch)*

Sie können die WSUS-Cleanuptasks von der Configuration Manager-Konsole aus über die Eigenschaften der Softwareupdatepunktkomponente planen und ausführen. Wenn Sie zuerst die erste Ausführung des WSUS-Cleanuptasks auswählen, wird er nach der nächsten Softwareupdatesynchronisierung ausgeführt.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>So wird die WSUS-Bereinigungsaufgabe geplant und ausgeführt

Planen Sie den WSUS-Cleanupauftrag durch Ausführen der folgenden Schritte:

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie den Standort an der obersten Ebene Ihrer Configuration Manager-Hierarchie aus.

3. Klicken Sie in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren** , und klicken Sie dann auf **Softwareupdatepunkt** , um die Eigenschaften der Softwareupdatepunkt-Komponente zu öffnen.  

4. Überprüfen Sie das **Verhalten bei Ablösung**. Ändern Sie das Verhalten bei Bedarf.

   ![Screenshot – Verhalten bei Ablösung](media/supersedence-behavior.png)

5. Klicken Sie auf die Registerkarte **Ablösungsregeln**, und wählen Sie die Option zum **Ausführen des WSUS-Bereinigungsassistenten** aus. Ab Version 1806 wurde diese Option in **Nach der Synchronisierung WSUS-Bereinigung ausführen** umbenannt.

6. Klicken Sie auf **OK** (oder auf **Schließen** in Version 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>WSUS-Cleanupverhalten in Version 1802 und früher

Vor Configuration Manager Version 1806 führt die WSUS-Cleanupoption das folgende Element aus:

- Die Option **Abgelaufene Updates** des WSUS-Cleanupassistenten für nur die oberste Ebene des Standorts des WSUS-Servers.

  ![Screenshot – WSUS-Bereinigung abgelaufener Updates](media/wsus-cleanup-expired.PNG)

- Ein Cleanup für Konfigurationselemente des Softwareupdates in der Configuration Manager-Datenbank wird alle sieben Tage ausgeführt und entfernt nicht benötigte Updates aus der Konsole.
  - Dieses Cleanup entfernt keine abgelaufenen Updates aus der Configuration Manager-Konsole, wenn sie derzeit bereitgestellt werden.

Für die WSUS-Datenbank der obersten Ebene und alle anderen WSUS-Datenbanken in der Umgebung wird trotzdem noch zusätzliche Wartung benötigt. Weitere Informationen und Anweisungen finden Sie im Blogbeitrag [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (Vollständige Anleitung für die Wartung von WSUS und Configuration Manager-SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>WSUS-Cleanupverhalten ab Version 1806

Ab Version 1806 wird die WSUS-Cleanupoption nach jeder Synchronisierung ausgeführt und bereinigt die folgenden Elemente:
<!--1357898 -->

- Die Option **Abgelaufene Updates** für WSUS-Server unter CAS und an primären Standorten.
  - WSUS-Server für sekundäre Standorte führen kein WSUS-Cleanup für abgelaufene Updates aus.
- Configuration Manager erstellt eine Liste abgelöster Updates aus der Datenbank. Die Liste basiert auf abgelöstem Verhalten in den Eigenschaften der Softwareupdatepunktkomponente.
  - Die Update-Konfigurationselemente, die den Kriterien für Verhalten bei Ablösung entsprechen, sind in der Configuration Manager-Konsole abgelaufen.
  - Die Updates werden in WSUS für CAS und primäre Standorte abgelehnt, aber nicht für sekundäre Standorte.
- Ein Cleanup für Konfigurationselemente des Softwareupdates in der Configuration Manager-Datenbank wird alle sieben Tage ausgeführt und entfernt nicht benötigte Updates aus der Konsole.
  - Dieses Cleanup entfernt keine abgelaufenen Updates aus der Configuration Manager-Konsole, wenn sie derzeit bereitgestellt werden.

> [!NOTE]
> Die Anzahl der Monate, bevor ein abgelöstes Update abgelaufen ist werden nach dem Erstellungsdatum des ablösenden Updates berechnet. Wenn Sie für diese Einstellung z.B. zwei Monate verwenden, werden abgelöste Updates in WSUS abgelehnt und sind in Configuration Manager abgelaufen, wenn das ablösende Update zwei Monate alt ist.

Alle WSUS-Wartungsvorgänge müssen manuell auf WSUS-Datenbanken des sekundären Standorts ausgeführt werden. Die folgenden Optionen des **WSUS-Assistenten für Server-Cleanup** werden nicht unter CAS und primären Standorten ausgeführt:

- Nicht verwendete Updates und Updaterevisionen
- Computer, die keine Verbindung mit dem Server herstellen
- Nicht benötigte Updatedateien

  Weitere Informationen und Anweisungen finden Sie im Blogbeitrag [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (Vollständige Anleitung für die Wartung von WSUS und Configuration Manager-SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>WSUS-Cleanupverhalten ab Version 1810

Ab Version 1810 können Sie in den Eigenschaften der Softwareupdatepunktkomponente Ablösungsregeln für Featureupdates getrennt von Nicht-Featureupdates festlegen. Die WSUS-Cleanupoption wird nach jeder Synchronisierung ausgeführt und bereinigt die folgenden Elemente:
<!--2839349,3098809, 2977644-->

- Die Option **Abgelaufene Updates** für WSUS-Server an CAS-Standorten und an primären und sekundären Standorten.
- Configuration Manager erstellt eine Liste abgelöster Updates aus der Datenbank. Die Liste basiert auf abgelöstem Verhalten in den Eigenschaften der Softwareupdatepunktkomponente.
  - Die Update-Konfigurationselemente, die den Kriterien für Verhalten bei Ablösung entsprechen, sind in der Configuration Manager-Konsole abgelaufen.
  - Die Updates werden in WSUS für CAS-, primäre und sekundäre Standorte abgelehnt.
- Ein Cleanup für Konfigurationselemente des Softwareupdates in der Configuration Manager-Datenbank wird alle sieben Tage ausgeführt und entfernt nicht benötigte Updates aus der Konsole.
  - Dieses Cleanup entfernt keine abgelaufenen Updates aus der Configuration Manager-Konsole, wenn sie derzeit bereitgestellt werden.

> [!NOTE]
> Die Anzahl der Monate, bevor ein abgelöstes Update abgelaufen ist werden nach dem Erstellungsdatum des ablösenden Updates berechnet. Wenn Sie für diese Einstellung z.B. zwei Monate verwenden, werden abgelöste Updates in WSUS abgelehnt und sind in Configuration Manager abgelaufen, wenn das ablösende Update zwei Monate alt ist.

Die folgenden Optionen des **WSUS-Assistenten für das Servercleanup** werden nicht an den CAS- oder primären und sekundären Standorten ausgeführt:

- Nicht verwendete Updates und Updaterevisionen
- Computer, die keine Verbindung mit dem Server herstellen
- Nicht benötigte Updatedateien

  Weitere Informationen und Anweisungen finden Sie im Blogbeitrag [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (Vollständige Anleitung für die Wartung von WSUS und Configuration Manager-SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).

## <a name="wsus-cleanup-starting-in-version-1906"></a>WSUS-Bereinigung ab Version 1906
<!--41101009-->

 Sie verfügen über zusätzliche WSUS-Wartungstasks, die Configuration Manager ausführen kann, um die Fehlerfreiheit von Softwareupdatepunkten zu gewährleisten. Zusätzlich zum Ablehnen abgelaufener Updates in WSUS kann Configuration Manager den WSUS-Datenbanken nicht gruppierte Indizes hinzufügen und veraltete Updates aus den WSUS-Datenbanken entfernen. Die WSUS-Wartung erfolgt nach jeder Synchronisierung.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Abgelaufene Updates in WSUS gemäß Ablösungsregeln ablehnen

Durch Ablehnen von Updates in WSUS lässt sich die Leistung verbessern, da diese Updates aus den an die Clients gesendeten Katalogen entfernt werden. Das Ablehnen von Updates, die von Configuration Manager als abgelöst gekennzeichnet werden, minimiert die Kataloggröße und verbessert die Leistung.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie den Standort an der obersten Ebene Ihrer Configuration Manager-Hierarchie aus.
3. Klicken Sie in der Gruppe „Einstellungen“ auf **Standortkomponenten konfigurieren** und anschließend auf **Softwareupdatepunkt**, um die Eigenschaften der Softwareupdatepunkt-Komponente zu öffnen.
4. Wählen Sie auf der Registerkarte **WSUS-Wartung** die Option **Abgelaufene Updates in WSUS gemäß Ablösungsregeln ablehnen** aus.

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Hinzufügen nicht gruppierter Indizes zur WSUS-Datenbank, um die WSUS-Bereinigungsleistung zu verbessern

Durch das Hinzufügen von nicht gruppierten Indizes wird die WSUS-Bereinigungsleistung von Configuration Manager verbessert.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie den Standort an der obersten Ebene Ihrer Configuration Manager-Hierarchie aus.
3. Klicken Sie in der Gruppe „Einstellungen“ auf **Standortkomponenten konfigurieren** und anschließend auf **Softwareupdatepunkt**, um die Eigenschaften der Softwareupdatepunkt-Komponente zu öffnen.
4. Wählen Sie auf der Registerkarte **WSUS Maintenance** (WSUS-Wartung) die Option **Add non-clustered indexes to the WSUS database** (Nicht gruppierte Indizes zur WSUS-Datenbank hinzufügen) aus.
5. Indizes werden für jede von Configuration Manager verwendete SUSDB-Datenbank den folgenden Tabellen hinzugefügt:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>SQL-Berechtigungen zum Erstellen von Indizes

Wenn sich die WSUS-Datenbank auf einem Remotecomputer mit SQL Server befindet, müssen Sie möglicherweise in SQL Berechtigungen zum Erstellen von Indizes hinzufügen. Das Konto, mit dem die Verbindung mit der WSUS-Datenbank hergestellt und die Indizes erstellt werden können, kann variieren. Wenn Sie in den [Eigenschaften des Softwareupdatepunkts ein WSUS-Server-Verbindungskonto](../get-started/install-a-software-update-point.md#wsus-server-connection-account) angeben, stellen Sie sicher, dass das Verbindungskonto über die SQL-Berechtigungen verfügt. Wenn Sie kein Verbindungskonto für WSUS-Server angeben, benötigt das Computerkonto des Standortservers die SQL-Berechtigungen.

- Das Erstellen eines Indexes erfordert die Berechtigung `ALTER` für die Tabelle oder Sicht. Das Konto muss ein Mitglied der festen Serverrolle `sysadmin` oder der festen Datenbankrollen `db_ddladmin` und `db_owner` sein. Weitere Informationen zum Erstellen eines Indexes und den erforderlichen Berechtigungen finden Sie unter [CREATE INDEX (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions).
- Dem Konto muss die Serverberechtigung `CONNECT SQL` erteilt werden. Weitere Informationen finden Sie unter [GRANT (Serverberechtigungen) (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

> [!NOTE]  
>  Wenn sich die WSUS-Datenbank auf einem Remotecomputer mit SQL Server und nicht standardmäßigem Port befindet, werden möglicherweise keine Indizes hinzugefügt. Für dieses Szenario können Sie einen [Serveralias mit dem SQL Server-Konfigurations-Manager](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017) erstellen. Indizes werden hinzugefügt, sobald der Alias hinzugefügt wurde und Configuration Manager eine Verbindung mit der WSUS-Datenbank herstellen kann.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Entfernen veralteter Updates aus der WSUS-Datenbank

Veraltete Updates sind nicht verwendete Updates und Updaterevisionen in der WSUS-Datenbank. Im Allgemeinen wird ein Update als veraltet eingestuft, sobald es nicht mehr im [Microsoft Update-Katalog](https://www.catalog.update.microsoft.com/) ist und von anderen Updates nicht mehr als Voraussetzung oder Abhängigkeit benötigt wird.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie den Standort an der obersten Ebene Ihrer Configuration Manager-Hierarchie aus.
3. Klicken Sie in der Gruppe „Einstellungen“ auf **Standortkomponenten konfigurieren** und anschließend auf **Softwareupdatepunkt**, um die Eigenschaften der Softwareupdatepunkt-Komponente zu öffnen.
4. Wählen Sie auf der Registerkarte **WSUS Maintenance** (WSUS-Wartung) **Remove obsolete updates from the WSUS database** (Veraltete Updates aus der WSUS-Datenbank entfernen) aus.
   - Das Entfernen veralteter Updates darf maximal 30 Minuten dauern, bevor es beendet wird. Es beginnt erneut, nachdem die nächste Synchronisierung erfolgt ist.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>SQL-Berechtigungen zum Entfernen veralteter Updates

Wenn sich die WSUS-Datenbank in einer SQL Server-Remoteinstanz befindet, benötigt das Computerkonto des Standortservers die folgenden SQL Server-Berechtigungen:

- Die festen Datenbankrollen `db_datareader` und `db_datawriter`. Weitere Informationen finden Sie unter [Rollen auf Datenbankebene](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles).
- Die Serverberechtigung `CONNECT SQL` muss dem Computerkonto des Standortservers gewährt werden. Weitere Informationen finden Sie unter [GRANT (Serverberechtigungen) (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

#### <a name="wsus-cleanup-wizard"></a>Assistent für die WSUS-Bereinigung

Ab Version 1906 werden die folgenden Optionen des **WSUS-Assistenten für das Servercleanup** nicht an den CAS- oder primären und sekundären Standorten ausgeführt:

- Computer, die keine Verbindung mit dem Server herstellen
- Nicht benötigte Updatedateien

  Weitere Informationen und Anweisungen finden Sie im Blogbeitrag [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance (Vollständige Anleitung für die Wartung von WSUS und Configuration Manager-SUP)](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/).


### <a name="known-issues-for-version-1906"></a>Bekannte Probleme bei Version 1906

Als Beispiel dient das folgende Szenario:
<!--5418148-->
- Sie verwenden Configuration Manager Version 1906
- Sie verfügen über Remote-Softwareupdatepunkte, die eine interne Windows-Datenbank verwenden.
- In den **Eigenschaften der Softwareupdatepunkt-Komponente** können Sie auf der Registerkarte **WSUS-Wartung** eine der folgenden Optionen auswählen:
   - Hinzufügen von nicht gruppierten Indizes zur WSUS-Datenbank
   - Entfernen veralteter Updates aus der WSUS-Datenbank

In diesem Szenario kann Configuration Manager die oben genannten WSUS-Wartungstasks für die Remote-Softwareupdatepunkte nicht mithilfe einer internen Windows-Datenbank ausführen. Dieses Problem tritt auf, weil die interne Windows-Datenbank keine Remoteverbindungen zulässt. Die folgenden Fehler werden im `WSyncMgr.log` auf dem Standortserver angezeigt:

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

Sie können die WSUS-Wartung für die Remote-Softwareupdatepunkte mithilfe einer internen Windows-Datenbank automatisieren. Weitere Informationen und detaillierte Schritte finden Sie unter [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint) (Vollständige Anleitung für die Wartung von WSUS und Configuration Manager-SUP).

## <a name="updates-cleanup-log-entries"></a>Protokolleinträge des Updatecleanups

Sie können dieses Cleanup überprüfen, indem Sie die Datei „wSyncMgr.log“ für die folgenden Einträge bewerten:

- Die Ablehnung abgelöster Updates in WSUS ist abgeschlossen, wenn dieser Protokolleintrag angezeigt wird: `Cleanup processed <number> total updates and declined <number>`
- Das WSUS-Cleanup wird gestartet, wenn der folgende Eintrag angezeigt wird: `Calling WSUS Cleanup.`
- Das WSUS-Cleanup für abgelaufene Updates ist abgeschlossen, wenn dieser Eintrag angezeigt wird: `Successfully completed WSUS Cleanup.`
- Das Cleanup für abgelaufene Update-Konfigurationselemente in Configuration Manager wird gestartet, wenn der folgende Eintrag angezeigt wird: `Deleting old expired updates...`
- Das Cleanup für abgelaufene Update-Konfigurationselemente in Configuration Manager ist abgeschlossen, wenn der folgende Eintrag angezeigt wird: `Deleted <number> expired updates total`
