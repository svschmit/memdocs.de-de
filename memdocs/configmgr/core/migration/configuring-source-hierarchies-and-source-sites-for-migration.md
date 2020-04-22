---
title: Migrationsquellhierarchien
titleSuffix: Configuration Manager
description: Konfigurieren Sie eine Quellhierarchie und Quellstandorte, damit Daten zu Ihrer Umgebung mit Current Branch von Configuration Manager migriert werden können.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701778"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Konfigurieren von Quellhierarchien und Quellstandorten für die Migration zu Current Branch von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zur Migration von Daten zu Ihrer Umgebung mit Current Branch von Configuration Manager müssen Sie eine unterstützte Configuration Manager-Quellhierarchie konfigurieren sowie mindestens einen Quellstandort in dieser Hierarchie, der zu migrierende Daten enthält.  

> [!NOTE]  
>  Vorgänge für die Migration werden am Standort der obersten Ebene in der Zielhierarchie ausgeführt. Bei der Konfiguration einer Migration mittels einer Configuration Manager-Konsole, die mit einem untergeordneten primären Standort verbunden ist, müssen Sie Zeit für die folgenden Vorgänge einplanen: die Replikation der Konfiguration zum Standort der zentralen Verwaltung, den Start sowie die Replikation des Status zurück zum primären Standort, mit dem Sie verbunden sind.  

 Anhand der Informationen und Verfahren in den folgenden Abschnitten können Sie die Quellhierarchie angeben, und zusätzliche Quellstandorte hinzufügen. Nachdem Sie diese Verfahren durchgeführt haben, können Sie Migrationsaufträge erstellen, und mit der Migration von Daten aus der Quell- zur Zielhierarchie beginnen.  

-   [Angeben einer Quellhierarchie für die Migration](#BKBM_ConfigSrcHierarchy)  

-   [Identifizieren von zusätzlichen Quellstandorten der Quellhierarchie](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a> Angeben einer Quellhierarchie für die Migration  
 Zur Migration von Daten zur Zielhierarchie müssen Sie eine unterstützte Quellhierarchie angeben, die die zu migrierenden Daten enthält. Standardmäßig wird der Standort der obersten Ebene dieser Hierarchie zu einem Quellstandort der Quellhierarchie. Bei der Migration einer Configuration Manager 2007-Hierarchie können Sie nach Abschluss der Datensammlung vom ersten Quellstandort weitere Quellstandorte für die Migration konfigurieren. Bei der Migration einer System Center 2012 Configuration Manager-Hierarchie oder einer Hierarchie mit Current Branch von Configuration Manager müssen Sie keine weiteren Quellstandorte einrichten, um die Daten aus der Quellhierarchie zu überführen. Dies liegt daran, dass in diesen Versionen von Configuration Manager eine freigegebene Datenbank verwendet wird, die am Standort der obersten Ebene der Quellhierarchie verfügbar ist. Die freigegebene Datenbank enthält alle Informationen, die Sie migrieren können.  

 Verwenden Sie folgende Verfahren zum Angeben einer Quellhierarchie zur Migration und zum Identifizieren zusätzlicher Quellstandorte in einer Configuration Manager 2007-Hierarchie.  

 Führen Sie diese Schritte mit einer Configuration Manager-Konsole aus, die mit der Zielhierarchie verbunden ist:  

### <a name="to-configure-a-source-hierarchy"></a>So konfigurieren Sie eine Quellhierarchie   

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2. Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Quellhierarchie**.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Migration** auf **Quellhierarchie angeben**.  

4. Wählen Sie im Dialogfeld **Quellhierarchie angeben** für **Quellhierarchie**die Option **Neue Quellhierarchie**aus.  

5. Geben Sie unter **Configuration Manager-Standortserver auf oberster Ebene** den Namen oder die IP-Adresse des Standortservers der obersten Ebene einer unterstützten Quellhierarchie ein.  

6. Geben Sie Zugriffskonten des Quellstandorts an, die über die folgenden Berechtigungen verfügen:  

   - Konto des Quellstandorts: **Leseberechtigung** für den SMS-Anbieter für den angegebenen Standort auf oberster Ebene in der Quellhierarchie. Für die Freigabe und Upgrades von Verteilungspunkten sind in der Quellhierarchie die Berechtigungen **Ändern** und **Löschen** für den Standort erforderlich.

   - Konto der Datenbank des Quellstandorts: Berechtigungen zum **Lesen** und **Ausführen** für die SQL Server-Datenbank für den angegebenen Standort auf oberster Ebene in der Quellhierarchie.  

     Wenn Sie die Verwendung des Computerkontos aktivieren, wird von Configuration Manager das Computerkonto des Standorts der obersten Ebene der Zielhierarchie verwendet. Für diese Option müssen Sie sicherstellen, dass das betreffende Konto ein Mitglied der Sicherheitsgruppe **Distributed COM-Benutzer** in der Domäne ist, in der sich der Standort der obersten Ebene der Quellhierarchie befindet.  

7. Für das Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien aktivieren Sie das Kontrollkästchen **Gemeinsame Verwendung des Verteilungspunkts für den Quellstandortserver aktivieren** . Wenn Sie die gemeinsame Verwendung des Verteilungspunkts zu diesem Zeitpunkt nicht aktivieren, können Sie dies auch nach Abschluss der Datensammlung vornehmen, indem Sie die Anmeldeinformationen des Quellstandorts bearbeiten.  

8. Klicken Sie auf **OK** , um die Konfiguration zu speichern. So wird das Dialogfeld **Status des Sammelns von Daten** geöffnet, und das Sammeln von Daten wird automatisch gestartet.  

9. Klicken Sie nach Abschluss der Datensammlung auf **Schließen** , um das Dialogfeld **Status des Sammelns von Daten** zu schließen und die Konfiguration abzuschließen.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a> Identifizieren von zusätzlichen Quellstandorten der Quellhierarchie  
 Beim Konfigurieren einer unterstützten Quellhierarchie wird der Standort der obersten Ebene dieser Hierarchie automatisch als Quellstandort konfiguriert, und die Daten werden automatisch von diesem Standort gesammelt. Welche Aktion Sie als nächstes durchführen, hängt von der Configuration Manager-Version ab, die von der Quellhierarchie ausgeführt wird:  

-   Für eine Configuration Manager 2007-Quellhierarchie können Sie nach Abschluss der Datensammlung für den ersten Quellstandort die Migration nur von diesem ersten Quellstandort aus starten, oder Sie können weitere Quellstandorte aus der Quellhierarchie konfigurieren. Richten Sie zum Migrieren von Daten, die nur an einem untergeordneten Standort verfügbar sind, zusätzliche Quellstandorte für eine Configuration Manager 2007-Hierarchie ein. Beispielsweise können Sie zusätzliche Quellstandorte zum Sammeln von Daten über Inhalte verwenden, die Sie migrieren möchten, wenn die betreffenden Inhalte an einem untergeordneten Standort in der Quellhierarchie erstellt wurden und am Standort der obersten Ebene der Quellhierarchie nicht zur Verfügung stehen.  

-   Für eine System Center 2012 Configuration Manager-Quellhierarchie oder eine Quellhierarchie mit Current Branch von Configuration müssen Sie keine weiteren Quellstandorte konfigurieren. Dies liegt daran, dass in diesen Versionen von Configuration Manager eine freigegebene Datenbank verwendet wird, die am Standort der obersten Ebene der Quellhierarchie verfügbar ist. Die freigegebene Datenbank enthält alle Informationen, die Sie von allen Standorten der Quellhierarchie migrieren können. Dadurch werden migrierbare Daten am Standort der obersten Ebene der Quellhierarchie verfügbar.  

Wenn Sie für eine Configuration Manager 2007-Quellhierarchie zusätzliche Quellstandorte konfigurieren, müssen Sie dabei in der Quellhierarchie von oben nach unten vorgehen. Sie müssen einen übergeordneten Standort als Quellstandort konfigurieren, bevor Sie einen seiner untergeordneten Standorte als Quellstandort konfigurieren können.  

Verwenden Sie das folgende Verfahren für die Konfiguration zusätzlicher Quellstandorte für Configuration Manager 2007-Quellhierarchien:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>So konfigurieren Sie zusätzliche Quellstandorte in der Quellhierarchie 

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und klicken Sie dann auf **Quellhierarchie**.  

3.  Wählen Sie den Standort aus, den Sie als Quellstandort konfigurieren möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Quellstandort** auf **Konfigurieren**.  

5.  Geben Sie im Dialogfeld **Anmeldeinformationen des Quellstandorts** für die Zugriffskonten des Quellstandorts Konten mit folgenden Berechtigungen ein:  

    -   Konto des Quellstandorts: **Leseberechtigung** für den SMS-Anbieter für den angegebenen Standort auf oberster Ebene in der Quellhierarchie. Für die Freigabe und Upgrades von Verteilungspunkten sind in der Quellhierarchie die Berechtigungen **Ändern** und **Löschen** für den Standort erforderlich.  

    -   Konto der Datenbank des Quellstandorts: Berechtigungen zum **Lesen** und **Ausführen** für die SQL Server-Datenbank für den angegebenen Standort auf oberster Ebene in der Quellhierarchie.  

    Wenn Sie die Verwendung des Computerkontos aktivieren, wird von Configuration Manager das Computerkonto des Standorts der obersten Ebene der Zielhierarchie verwendet. Für diese Option müssen Sie sicherstellen, dass das betreffende Konto ein Mitglied der Sicherheitsgruppe **Distributed COM-Benutzer** in der Domäne ist, in der sich der Standort der obersten Ebene der Quellhierarchie befindet.  

6.  Für das Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien aktivieren Sie das Kontrollkästchen **Gemeinsame Verwendung des Verteilungspunkts für den Quellstandortserver aktivieren** . Wenn Sie die gemeinsame Verwendung des Verteilungspunkts zu diesem Zeitpunkt nicht aktivieren, können Sie dies auch nach Abschluss der Datensammlung vornehmen, indem Sie die Anmeldeinformationen für den Quellstandort bearbeiten.  

7. Klicken Sie auf **OK** , um die Konfiguration zu speichern. So wird das Dialogfeld **Status des Sammelns von Daten** geöffnet, und das Sammeln von Daten wird automatisch gestartet.  

8.  Klicken Sie nach Abschluss der Datensammlung auf **Schließen** , um die Konfiguration abzuschließen.  
