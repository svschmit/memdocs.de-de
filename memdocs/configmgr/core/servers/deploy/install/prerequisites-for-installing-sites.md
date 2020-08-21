---
title: Voraussetzungen für Standorte
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Voraussetzungen für die Installation der verschiedenen Typen von Configuration Manager-Standorten.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bf9ad15266c4e6615ba100d5ea5270e23b93ece7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699125"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Voraussetzungen für die Installation von Configuration Manager-Standorten

*Gilt für: Configuration Manager (Current Branch)*

Informieren Sie sich über die Voraussetzungen für die Installation der verschiedenen Typen von Configuration Manager-Standorten, bevor Sie einen Standort installieren.


## <a name="primary-sites-and-the-central-administration-site"></a>Primäre Standorte und Standort der zentralen Verwaltung

Für die Installation eines der folgenden Typen gelten die folgenden Voraussetzungen:

- Ein Standort der zentralen Verwaltung als erster Standort einer Hierarchie
- Ein eigenständiger primärer Standort
- Ein untergeordneter primärer Standort

Wenn Sie einen Standort der zentralen Verwaltung im Rahmen einer Hierarchieerweiterung installieren, lesen Sie mehr über das [Erweitern eines eigenständigen primären Standorts](#bkmk_expand).

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Voraussetzungen für die Installation eines primären Standorts oder eines Standorts der zentralen Verwaltung  

- Die erforderlichen Windows Server-Rollen, Features und Windows-Komponenten müssen installiert sein. Weitere Informationen finden Sie unter [Site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq) (Standortsystemanforderungen).  

- Das Benutzerkonto, über das der Standort installiert wird, muss über die folgenden Rechte verfügen:  

    - **Administrator** auf den folgenden Servern:  
        - Der Standortserver  
        - Jedem Server, der die **Standortdatenbank** hostet  
        - Jeder Instanz des **SMS-Anbieters** für den Standort  

    - **Sysadmin** für die SQL Server-Instanz, die die Standortdatenbank hostet  

        > [!IMPORTANT]  
        > Nach Abschluss des Configuration Manager-Setups muss das Standortserver-Computerkonto die Systemadministratorrechte für SQL Server beibehalten. Entfernen Sie nicht die SQL-Systemadministratorrechte aus diesem Konto.  

    > [!NOTE]
    > Weitere Informationen zur Notwendigkeit dieser Berechtigungen nach Abschluss des Setups finden Sie unter [Erweiterte Berechtigungen](../../../plan-design/hierarchy/accounts.md#elevated-permissions).

- Wenn Sie einen primären Standort installieren, benötigen Sie die folgenden zusätzlichen Berechtigungen:  

    - **Administrator** auf weiteren Servern, auf denen Sie den ersten Verwaltungspunkt und Verteilungspunkt installieren, falls dies nicht auf dem Standortserver erfolgt  

- Wenn Sie einen neuen untergeordneten primären Standort unter einem Standort der zentralen Verwaltung installieren, benötigen Sie die folgenden zusätzlichen Berechtigungen:  

    - **Administrator** auf dem Server, der den Standort der zentralen Verwaltung hostet  

    - Rollenbasierte Administratorrechte innerhalb von Configuration Manager, die der Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** entsprechen  

- Verwenden Sie die richtigen Installationsquelldateien, und führen Sie das Setup an diesem Standort aus. Weitere Informationen zu den richtigen Quelldateien zum Installieren der unterschiedlichen Standorttypen finden Sie unter [Optionen für die Installation verschiedener Standorttypen](prepare-to-install-sites.md#bkmk_options).  

- Der Standortserver muss auf eine der folgenden Arten Zugriff auf aktualisierte Setupdateien von Microsoft haben:  

    - Bevor Sie mit der Installation beginnen, laden Sie eine Kopie dieser Dateien herunter, und speichern Sie sie in Ihrem lokalen Netzwerk. Weitere Informationen finden Sie unter [Setup Downloader (Setup-Downloadprogramm)](setup-downloader.md).  

    - Wenn eine lokale Kopie dieser Dateien nicht verfügbar ist, benötigt der Standortserver Internetzugang. Er lädt diese Dateien dann beim Installieren bei Microsoft herunter.  

- Der Standortserver und der Standortdatenbankserver müssen alle Konfigurationsvoraussetzungen erfüllen. Führen Sie vor dem Beginn der Configuration Manager-Einrichtung [manuell eine Voraussetzungsprüfung](prerequisite-checker.md) aus, um Probleme zu erkennen und zu beheben.  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Voraussetzungen für die Erweiterung eines eigenständigen primären Standorts

Die folgenden Voraussetzungen müssen erfüllt sein, damit ein eigenständiger primärer Standort in eine Hierarchie mit einem Standort der zentralen Verwaltung erweitert werden kann:

#### <a name="source-file-version-matches-site-version"></a>Übereinstimmen der Quelldatei- und Standortversion

Installieren Sie den neuen Standort der zentralen Verwaltung mit Medien aus einem CD.Latest-Ordner, die der Version des eigenständigen primären Standorts entsprechen. Um eine Versionsübereinstimmung sicherzustellen, verwenden Sie die Quelldateien aus dem [CD.Latest-Ordner](../../manage/the-cd.latest-folder.md) am eigenständigen primären Standort.

Weitere Informationen zu den richtigen Quelldateien zum Installieren der unterschiedlichen Standorttypen finden Sie unter [Optionen für die Installation verschiedener Standorttypen](prepare-to-install-sites.md#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Beenden der aktiven Migration aus einer anderen Hierarchie

Der eigenständige primäre Standort kann nicht dahingehend konfiguriert werden, dass Daten aus einer anderen Configuration Manager-Hierarchie migriert werden. Beenden Sie die aktive Migration zum eigenständigen primären Standort aus anderen Configuration Manager-Hierarchien, und entfernen Sie alle Migrationskonfigurationen. Dazu gehören:

- Noch nicht abgeschlossene Migrationsaufträge  
- Datensammlung  
- Konfiguration der aktiven Quellhierarchie  

Diese Konfiguration ist notwendig, da Configuration Manager Daten aus dem Standort auf oberster Hierarchieebene migriert. Wenn Sie einen eigenständigen primären Standort erweitern, werden die Konfigurationen für die Migration nicht an den Standort der zentralen Verwaltung übertragen.  

Wenn Sie nach der Erweiterung des eigenständigen primären Standorts die Migration am primären Standort erneut konfigurieren, führt der Standort der zentralen Verwaltung die Migrationsvorgänge aus.

Weitere Informationen zum Konfigurieren der Migration finden Sie unter [Konfigurieren von Quellhierarchien und Quellstandorten für die Migration](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

#### <a name="computer-account-as-administrator"></a>Computerkonto als Administrator

Das Computerkonto des Servers, auf dem der neue Standort der zentralen Verwaltung gehostet wird, muss der Gruppe **Administratoren** am eigenständigen primären Standort angehören.

Das Computerkonto des neuen Standorts der zentralen Verwaltung muss am eigenständigen primären Standort **Administrator**rechte haben. Anderenfalls kann der eigenständige primäre Standort nicht erfolgreich erweitert werden. Dies ist nur während der Standorterweiterung erforderlich. Wenn die Standorterweiterung abgeschlossen ist, können Sie das Konto aus der Benutzergruppe am primären Standort entfernen.  

#### <a name="installation-account-permissions"></a>Berechtigungen für das Installationskonto

Das Benutzerkonto, das das Configuration Manager-Setup zur Installation des neuen Standorts der zentralen Verwaltung ausführt, muss über rollenbasierte Administrationsrechte am eigenständigen primären Standort verfügen.

Zum Installieren eines Standorts der zentralen Verwaltung im Rahmen einer Standorterweiterung muss das Benutzerkonto, das das Setup zur Installation des Standorts der zentralen Verwaltung ausführt, in der rollenbasierten Verwaltung am eigenständigen primären Standort entweder als **Hauptadministrator** oder als **Infrastrukturadministrator** definiert sein.

Weitere Informationen, einschließlich der kompletten Liste der erforderlichen Berechtigungen finden Sie unter [Standortsystem-Installationskonto](../../../plan-design/hierarchy/accounts.md#site-installation-account).

#### <a name="top-level-site-roles"></a>Rollen auf oberster Hierarchieebene

Bevor Sie den Standort erweitern, deinstallieren Sie die folgenden Standortsystemrolle am eigenständigen primären Standort:

- Asset Intelligence-Synchronisierungspunkt  
- Endpoint Protection-Punkt  
- Dienstverbindungspunkt  

Configuration Manager unterstützt nur diese Rollen auf der obersten Hierarchieebene. Deinstallieren Sie diese Standortsystemrollen, bevor Sie den eigenständigen primären Standort erweitern. Installieren Sie diese Standortsystemrollen nach der Standorterweiterung erneut am Standort der zentralen Verwaltung.  

Alle anderen Standortsystemrollen können am primären Standort installiert bleiben.  

#### <a name="open-the-sql-server-service-broker-port"></a>Öffnen des SQL Server Service Broker-Ports

Der Netzwerkport muss für den SQL Server Service Broker zwischen dem eigenständigen primären Standort und dem Server des Standorts der zentralen Verwaltung geöffnet sein.  

Für die erfolgreiche Replikation von Daten zwischen einem Standort der zentralen Verwaltung und einem primären Standort muss in Configuration Manager ein Port zwischen den beiden Standorten für die Nutzung durch SSB offen sein. Beim Installieren eines Standorts der zentralen Verwaltung und beim Erweitern eines eigenständigen primären Standorts verifiziert die Voraussetzungsprüfung nicht, ob der von Ihnen für den Service Broker angegebene Port am primären Standort offen ist.  

#### <a name="known-issues-with-azure-services"></a>Bekannte Probleme mit Azure-Diensten

Nachdem Sie den Standort erweitert haben, müssen Sie die folgenden Azure-Dienste mit Configuration Manager neu konfigurieren:

- [Log Analytics](/azure/azure-monitor/platform/collect-sccm)  
- [Microsoft Store für Unternehmen](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Cloudverwaltungsgateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

Die einfachste Methode besteht darin, den geheimen Schlüssel des Azure Active Directory-Mandanten zu erneuern. Weitere Informationen finden Sie unter [Geheimen Schlüssel erneuern](../configure/azure-services-wizard.md#bkmk_renew).

Alternativ können Sie die Verbindung mit diesem Dienst entfernen und dann wieder erstellen:

1. Löschen Sie in der Configuration Manager-Konsole den Azure-Dienst aus dem Knoten der **Azure-Dienste**.  

2. Löschen Sie im Azure-Portal den Mandanten, der dem Dienst im Knoten des Azure Active Directory-Mandanten zugeordnet ist. Dadurch wird auch die Azure AD-Web-App gelöscht, die dem Dienst zugeordnet ist.  

3. Konfigurieren Sie die Verbindung mit dem Azure-Dienst für die Verwendung mit Configuration Manager neu.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a> Sekundäre Standorte

Im Folgenden werden die Voraussetzungen für die Installation von sekundären Standorten aufgeführt:  

- Die erforderlichen Windows Server-Rollen, Features und Windows-Komponenten müssen installiert sein. Weitere Informationen finden Sie unter [Site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq) (Standortsystemanforderungen).  

- Der Administrator, der die Installation des sekundären Standorts in der Configuration Manager-Konsole konfiguriert, muss über rollenbasierte Administratorrechte verfügen, die der Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** entsprechen.  

- Das Computerkonto des übergeordneten primären Standorts muss auf dem sekundären Standortserver über **Administratorrechte** verfügen.  

- Vom sekundären Standort wird zum Hosten der Datenbank des sekundären Standorts eine zuvor installierte SQL Server-Instanz verwendet:  

    - Das Computerkonto des übergeordneten primären Standorts muss über **Systemadministratorrechte** für die SQL Server-Instanz auf dem sekundären Standortserver verfügen.  

    - Das **lokale Systemkonto** des Servercomputers des sekundären Standorts muss über **Systemadministratorrechte** für die SQL Server-Instanz auf dem sekundären Standortserver verfügen.  

        > [!IMPORTANT]  
        > Nach Abschluss des Configuration Manager-Setups müssen beide Konten die Systemadministratorrechte für SQL Server beibehalten. Entfernen Sie nicht die Systemadministratorrechte aus diesen Konten.  

- Der sekundäre Standortserver muss alle Konfigurationsvoraussetzungen erfüllen. Diese Konfigurationen umfassen SQL Server und die standardmäßigen Standortsystemrollen des Verwaltungs- sowie des Verteilungspunkts.  


## <a name="next-steps"></a>Nächste Schritte

Nach dem Bestätigen der Voraussetzungen können Sie das Setup ausführen. Weitere Informationen finden Sie unter [Verwenden des Setup-Assistenten zum Installieren von Configuration Manager-Standorten](use-the-setup-wizard-to-install-sites.md).