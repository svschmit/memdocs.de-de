---
title: SQL Server-Cluster
titleSuffix: Configuration Manager
description: Hosten der Standortdatenbank von Configuration Manager mit einem SQL Server-Cluster
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e731ef2d133c2187eb9eaa98c07afeed37645fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700848"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Hosten der Standortdatenbank mit einem SQL Server-Cluster

*Gilt für: Configuration Manager (Current Branch)*

Sie können mit einem SQL Server-Failovercluster die Standortdatenbank von Configuration Manager hosten. Ein Cluster bietet Failoverunterstützung und verbessert die Zuverlässigkeit der Standortdatenbank. Er bietet allerdings keine zusätzlichen Vorteile in puncto Verarbeitung oder Lastenausgleich. Darüber hinaus verwendet ein SQL Server-Failovercluster freigegebenen Speicher und führt einen Single Point of Failure ein. Die Leistung kann beeinträchtigt werden, da der Standortserver den aktiven Knoten des SQL Server-Clusters suchen muss, bevor eine Verbindung mit der Standortdatenbank hergestellt werden kann.  

> [!IMPORTANT]  
> Erfolgreiche Einrichtung von SQL Server-Clustern beruht auf Dokumentation und Verfahren in der SQL Server-Dokumentationsbibliothek.  


Bevor Sie Configuration Manager installieren, konfigurieren Sie den SQL Server-Cluster so, dass er Configuration Manager unterstützt. Weitere Informationen finden Sie unter [Vorbereiten einer gruppierten SQL Server-Instanz](#bkmk_prepare).

Beim Configuration Manager-Setup wird der Windows VSS Writer auf jedem physischen Computerknoten des Microsoft Windows Server-Clusters installiert. Dieser Dienst unterstützt die Wartungsaufgabe **Standortserver sichern**.  

Nach der Installation des Standorts überprüft Configuration Manager den Clusterknoten stündlich auf Änderungen. Configuration Manager verwaltet automatisch alle gefundenen Änderungen, die die Komponenteninstallation betreffen. Beispielsweise ein Knotenfailover oder das Hinzufügen eines neuen Knotens zum SQL Server-Cluster.  



## <a name="supported-options"></a>Unterstützte Optionen

Die folgenden Optionen werden für SQL Server-Failovercluster unterstützt, die als Standortdatenbank verwendet werden:

- Cluster mit Einzelinstanz  

- Konfigurationen mit mehreren Instanzen  

- Mehrere aktive Knoten  

- Sowohl eine benannte als auch eine Standardinstanz  



## <a name="prerequisites"></a>Voraussetzungen

Beachten Sie die folgenden Voraussetzungen:  

- Die Standortdatenbank muss remote vom Standortserver installiert werden. Der Cluster kann nicht den Standortsystemserver enthalten.  

    > [!Note]  
    > Ab Version 1810 blockiert der Einrichtungsprozess für Configuration Manager nicht mehr die Installation der Standortserverrolle auf einem Computer mit der Windows-Rolle für Failoverclustering. Bisher konnten Sie die Standortdatenbank nicht gleichzeitig auf dem Standortserver installieren. Mit dieser Änderung haben Sie die Möglichkeit, eine hochverfügbare Website mit weniger Servern zu erstellen, indem Sie einen SQL-Cluster und einen Standortserver im passiven Modus verwenden. Weitere Informationen finden Sie unter [High availability options (Optionen für Hochverfügbarkeit)](high-availability-options.md). <!--3607761, fka 1359132-->  

- Fügen Sie der lokalen Gruppe **Administratoren** jedes Servers im Cluster das Computerkonto des Standortservers hinzu.  

- Aktivieren Sie zur Unterstützung der Kerberos-Authentifizierung das **TCP/IP**-Netzwerkkommunikationsprotokoll für die Netzwerkverbindung jedes SQL Server-Clusterknotens. Das **Named Pipes**-Protokoll ist nicht erforderlich, kann jedoch zur Behandlung von Problemen bei der Kerberos-Authentifizierung verwendet werden. Die Netzwerkprotokolleinstellungen werden im **SQL Server-Konfigurations-Manager** unter **SQL Server-Netzwerkkonfiguration** konfiguriert.  

- Wenn Sie eine Public Key-Infrastruktur (PKI) verwenden, lesen Sie [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md). Es gelten bestimmte Zertifikatanforderungen, wenn Sie einen SQL Server-Cluster für die Standortdatenbank verwenden.  



## <a name="limitations"></a>Einschränkungen

Beachten Sie die folgenden Einschränkungen:  


### <a name="installation-and-configuration"></a>Installation und Konfiguration

- Sekundäre Standorte können keinen SQL Server-Cluster verwenden.  

- Wenn Sie einen SQL Server-Cluster angeben, ist die Option zur Angabe nicht standardmäßiger Dateispeicherorte für die Standortdatenbank nicht verfügbar.  


### <a name="sms-provider"></a>SMS-Anbieter

Sie können keine Instanz des SMS-Anbieters auf einem SQL Server-Cluster installieren. Die Installation wird auch nicht auf einem Computer unterstützt, der einen gruppierten SQL Server-Knoten ausführt.  


### <a name="data-replication-options"></a>Optionen für die Replikation von Daten

Wenn Sie **Verteilte Ansichten** verwenden, können Sie zum Hosten der Standortdatenbank keinen SQL Server-Cluster verwenden.  


### <a name="backup-and-recovery"></a>Sicherung und Wiederherstellung

Configuration Manager unterstützt nicht die Data Protection Manager-Sicherung (DPM) für einen SQL Server-Cluster, der eine benannte Instanz verwendet. Die Lösung unterstützt die DPM-Sicherung auf einem SQL Server-Cluster, der die Standardinstanz von SQL Server verwendet.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a> Vorbereiten einer gruppierten SQL Server-Instanz  

Hier die wichtigsten Aufgaben, um die Standortdatenbank vorzubereiten:

- Erstellen Sie den virtuellen SQL Server-Cluster, der die Standortdatenbank hosten soll, in einer vorhandenen Windows Server-Clusterumgebung. Spezifische Informationen zum Installieren und Konfigurieren eines SQL Server-Clusters finden Sie in der Dokumentation zu Ihrer SQL Server-Version. Weitere Informationen finden Sie unter [Erstellen eines neuen SQL Server-Failoverclusters (Setup)](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- Legen Sie bei jedem Computer im SQL Server-Cluster eine Datei im Stammordner jedes Laufwerks ab, auf dem Configuration Manager keine Standortkomponenten installieren soll. Benennen Sie die Datei mit `NO_SMS_ON_DRIVE.SMS`. Standardmäßig installiert Configuration Manager an jedem physischen Knoten einige Komponenten, um Vorgänge wie Sicherungen zu unterstützen.  

- Fügen Sie der Gruppe lokaler **Administratoren** jedes Windows Server-Clusterknotencomputers das Computerkonto des Standortservers hinzu.  

- Weisen Sie in der virtuellen SQL Server-Instanz dem Benutzerkonto, das das Configuration Manager-Setup ausführt, die SQL Server-Rolle **sysadmin** zu.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>So installieren Sie einen neuen Standort mithilfe eines SQL Server-Clusters  

Führen Sie zum Installieren eines Standorts, der eine gruppierte Standortdatenbank verwendet, das Configuration Manager-Setup gemäß Ihrem normalen Prozess für die Installation eines Standorts mit der folgenden Änderung durch:  

- Geben Sie auf der Seite **Datenbankinformationen** den Namen der virtuellen SQL Server-Clusterinstanz an, von der die Standortdatenbank gehostet wird. Die virtuelle Instanz ersetzt den Namen des Computers, auf dem SQL Server ausgeführt wird.  

    > [!IMPORTANT]  
    > Wenn Sie den Namen der virtuellen SQL Server-Clusterinstanz eingeben, geben Sie nicht den vom Windows Server-Cluster erstellten virtuellen Windows Server-Namen ein. Wenn Sie den virtuellen Windows Server-Namen verwenden, wird die Standortdatenbank auf der lokalen Festplatte des aktiven Windows Server-Clusterknotens installiert. Dies verhindert ein erfolgreiches Failover, sollte der Knoten ausfallen.  
