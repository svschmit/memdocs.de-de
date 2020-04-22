---
title: Auswählen der zu migrierenden Elemente
titleSuffix: Configuration Manager
description: Erfahren Sie, welche Daten migriert werden können und welche Daten Sie nicht zu Current Branch von Configuration Manager migrieren können.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701768"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Bestimmen, ob Daten zu Current Branch von Configuration Manager migriert werden sollen

*Gilt für: Configuration Manager (Current Branch)*

In Current Branch von Configuration Manager bezeichnet „Migration“ einen Prozess zum Übertragen vorhandener Daten und Konfigurationen, die Sie erstellt haben, aus unterstützten Versionen von Configuration Manager in Ihre neue Hierarchie.  Damit können die folgenden Zwecke erfüllt werden:  

-   Kombinieren mehrerer Hierarchien zu einer.  

-   Verschieben von Daten und Konfigurationen aus einer Testbereitstellung in Ihre Produktionsbereitstellung.

-   Verschieben von Daten und Konfigurationen aus einer früheren Configuration Manager-Version, z. B. Configuration Manager 2007, die über keinen Upgradepfad zu Current Branch von Configuration Manager verfügt, oder aus System Center 2012 Configuration Manager (unterstützt keinen Upgradepfad zu Current Branch von Configuration Manager).  

Mit Ausnahme der Standortsystemrolle Verteilungspunkt und der Computer, auf denen Verteilungspunkte gehostet werden, kann keine Infrastruktur (z. B. Standorte, Standortsystemrollen oder Computer, auf denen eine Standortsystemrolle gehostet wird) migriert, übertragen oder zwischen Hierarchien freigegeben werden.  

 Obwohl Sie keine Serverinfrastrukturen migrieren können, können Sie Configuration Manager-Clients zwischen Hierarchien migrieren. Die Clientmigration umfasst das Migrieren der von Clients verwendeten Daten aus der Quell- in die Zielhierarchie und die anschließende Installation oder Neuzuweisung der Clientsoftware, wobei der Client der neuen Hierarchie unterstellt wird.

Sobald ein Client nach seiner Installation in der neuen Hierarchie seine Daten übermittelt, kann Configuration Manager mithilfe dessen eindeutiger Configuration Manager-ID den Bezug zwischen den Daten, die Sie zuvor migriert haben, und den einzelnen Clients herstellen.  

 Mithilfe dieser Migrationsfunktionalität können Sie nicht nur weiterhin von Investitionen profitieren, die bereits in Konfigurationen und Bereitstellungen erfolgt sind, sondern auch von allen wesentlichen Produktänderungen (die zuerst in System Center 2012 Configuration Manager und dann in Configuration Manager eingeführt wurden). Zu den Änderungen gehören eine vereinfachte Configuration Manager-Hierarchie, die weniger Standorte und Ressourcen benötigt, und eine verbesserte Verarbeitung durch Verwenden von nativem 64-Bit-Code, der auf 64-Bit-Hardware läuft.  

 Informationen zu den Versionen von Configuration Manager, in denen die Migration unterstützt wird, finden Sie unter [Voraussetzungen für die Migration](../../core/migration/prerequisites-for-migration.md).  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a> Daten, die zu Current Branch von Configuration Manager migriert werden können

Die meisten Objekte können zwischen unterstützten Configuration Manager-Hierarchien migriert werden. Die migrierten Instanzen einiger Objekte einer unterstützten Version von Configuration Manager2007 müssen geändert werden, um dem Schema- und Objektformat von System Center 2012 Configuration Manager zu entsprechen.

Diese Änderungen haben keine Auswirkungen auf die Daten in der Datenbank des Quellstandorts. Objekte, die aus einer unterstützten Version von System Center 2012 Configuration Manager oder Current Branch von Configuration Manager migriert wurden, erfordern keine Änderungen.  

Die folgenden Objekte auf Grundlage der Configuration Manager-Version in der Quellhierarchie migriert werden können. Einige Objekte, wie z. B. Abfragen, werden nicht migriert. Wenn Sie diese Objekte, die nicht migriert werden, weiterhin verwenden möchten, müssen Sie sie in der neuen Hierarchie neu erstellen. Andere Objekte, z.B. einige Clientdaten, werden in der neuen Hierarchie automatisch neu erstellt, wenn Sie Clients in der Hierarchie verwalten.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Folgende Objekte können Sie von System Center 2012 Configuration Manager oder Current Branch von Configuration Manager migrieren:

-   Anwendungen für System Center 2012 Configuration Manager und höhere Versionen  

-   Virtuelle App-V-Umgebung für System Center 2012 Configuration Manager und höhere Versionen  

-   Asset Intelligence-Anpassungen  

-   Standortgrenzen  

-   Sammlungen: Verwenden Sie einen Objektmigrationsauftrag, um Sammlungen von einer unterstützten Version von System Center 2012 Configuration Manager oder Current Branch von Configuration Manager zu migrieren.  

-   Kompatibilitätseinstellungen:  

    -   Konfigurationsbasislinien  

    -   Konfigurationselemente  

-   Bereitstellungen  

-   Betriebssystembereitstellung:  

    -   Startabbilder  

    -   Treiberpakete  

    -   Treiber  

    -   Bilder  

    -   Pakete  

    -   Tasksequenzen  

-   Suchergebnisse: Gespeicherte Suchkriterien  

-   Softwareupdates:  

    -   Bereitstellungen  

    -   Bereitstellungspakete  

    -   Vorlagen  

    -   Softwareupdatelisten  

-   Softwareverteilungspakete  

-   Softwaremessungsregeln  

-   Virtuelle Anwendungspakete  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Folgende Objekte können von Configuration Manager 2007 SP2 migriert werden:

-   Ankündigungen  

-   Anwendungen für System Center 2012 Configuration Manager und höhere Versionen  

-   Virtuelle App-V-Umgebung für System Center 2012 Configuration Manager und höhere Versionen  

-   Asset Intelligence-Anpassungen  

-   Standortgrenzen  

-   Sammlungen: Verwenden Sie einen Sammlungsmigrationsauftrag, um Sammlungen von einer unterstützten Version von Configuration Manager 2007 zu migrieren.  

-   Kompatibilitätseinstellungen (in Configuration Manager 2007 als Verwaltung gewünschter Konfigurationen bezeichnet)  

    -   Konfigurationsbasislinien  

    -   Konfigurationselemente  

-   Betriebssystembereitstellung:  

    -   Startabbilder  

    -   Treiberpakete  

    -   Treiber  

    -   Bilder  

    -   Pakete  

    -   Tasksequenzen  

-   Suchergebnisse: Suchordner  

-   Softwareupdates:  

    -   Bereitstellungen  

    -   Bereitstellungspakete  

    -   Vorlagen  

    -   Softwareupdatelisten  

-   Softwareverteilungspakete  

-   Softwaremessungsregeln  

-   Virtuelle Anwendungspakete  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a> Daten, die nicht zu Current Branch von Configuration Manager migriert werden können

Folgende Objekttypen können nicht migriert werden:  

-   AMT-Client-Bereitstellungsinformationen  

-   Dateien auf Clients, einschließlich:  

    -   Clientinventur- und -verlaufsdaten  

    -   Dateien im Clientcache  

-   Abfragen  

-   Configuration Manager 2007-Sicherheitsrechte und -Instanzen für den Standort und Objekte  

-   Configuration Manager 2007-Berichte von SQL Server Reporting Services  

-   Configuration Manager 2007-Webberichte  

-   System Center 2012 Configuration Manager-Berichte und Berichte aus Current Branch von Configuration Manager  

-   Rollenbasierte Verwaltung in System Center 2012 Configuration Manager und Current Branch von Configuration Manager:  

    -   Sicherheitsrollen  

    -   Sicherheitsbereichen  
