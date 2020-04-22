---
title: Grundlagen der Clientverwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Tasks, die Sie für die Verwaltung von Configuration Manager-Clients ausführen können.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707098"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>Grundlagen der Clientverwaltungstasks für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nach der Installation von Configuration Manager-Clients können Sie verschiedene Tasks zur Verwaltung der Clients ausführen.  Einige dieser Tasks werden über die Configuration Manager-Konsole ausgeführt. Andere Tasks werden über die Configuration Manager-Clientanwendung ausgeführt. Die Configuration Manager-Clientanwendung wird mit der Configuration Manager-Clientsoftware installiert.

## <a name="configuration-manager-console-tasks"></a>Tasks der Configuration Manager-Konsole
 In der Configuration Manager-Konsole können Sie verschiedene Clientverwaltungstasks ausführen:  

-   Bereitstellen von Anwendungen, Softwareupdates, Wartungsskripts und Betriebssystemen. Konfigurieren der Installation zur Ausführung zu einem bestimmten Termin, Bereitstellen der Software für die Installation an Benutzer auf Anforderung, oder Konfigurieren von Anwendungen zur Deinstallation.  

-   Schutz der Computer vor Schadsoftware und Sicherheitsrisiken sowie Ausgeben einer Warnung, wenn Probleme erkannt werden  

-   Definieren von Clientkonfigurationseinstellungen, die Sie überwachen und bei fehlender Konformität wiederherstellen möchten.  

-   Sammeln von Hardware- und Softwareinventurinformationen, darunter die Überwachung und Abstimmung von Lizenzinformationen von Microsoft  

-   Problembehandlung auf Computern mit der Remotesteuerung.  

-   Implementieren von Energieverwaltungseinstellungen zum Verwalten und Überwachen des Stromverbrauchs von Computern  

Die Configuration Manager-Konsole überwacht die vorherigen Tasks nahezu in Echtzeit. In der Configuration Manager-Konsole sind Benachrichtigungen und Statusinformationen zu jedem Task verfügbar. Verwenden Sie zum Erfassen von Daten und Auswerten historischer Trends die integrierten Berichterstattungsfunktionen von SQL Reporting Services. Clients senden Informationen als Clientstatus an den Standort.  Clientstatusinformationen liefern Daten über die Integrität des Clients sowie die Clientaktivität, und werden in der Konsole oder mithilfe der integrierten Berichte für Configuration Manager angezeigt. Mithilfe dieser Daten können Sie Computer identifizieren, die nicht reagieren, und in einigen Fällen Probleme automatisch beheben.  

 Weitere Informationen zu Verwaltungstasks für Clients finden Sie unter [Verwalten von Clients](../../core/clients/manage/manage-clients.md) und [Verwalten von Clients für Linux- und UNIX-Server](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Informationen zur Verwendung von Berichten finden Sie unter   
            [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Configuration Manager-Clientanwendung  
 Wenn Sie die Configuration Manager-Clientsoftware installieren, wird die Configuration Manager-Clientanwendung ebenfalls installiert. Im Gegensatz zum Softwarecenter ist die Configuration Manager-Clientanwendung nicht für Endbenutzer bestimmt, sondern für den Helpdesk. Einige Konfigurationsoptionen erfordern lokale Administratorberechtigungen, und für die meisten Optionen sind technische Kenntnisse der Funktionsweise der Configuration Manager-Clientanwendung erforderlich. Sie können diese Anwendung verwenden, um auf einem Client die folgenden Aufgaben auszuführen:  

-   Anzeigen von Eigenschaften des Clients, z.B. die Buildnummer, der zugewiesene Standort, mit welchem Verwaltungspunkt der Client kommuniziert, und ob ein Public Key Infrastructure-Zertifikat (PKI) oder ein selbstsigniertes Zertifikat verwendet wird.  

-   Bestätigen Sie, dass der Client erfolgreich eine Clientrichtlinie heruntergeladen hat, nachdem der Client zum ersten Mal installiert wurde. Bestätigen Sie ebenfalls, dass die Clienteinstellungen wie erwartet aktiviert oder deaktiviert sind, entsprechend den Clienteinstellungen, die in der Configuration Manager-Konsole konfiguriert wurden.  

-   Starten Sie die Clientaktionen. Laden Sie z.B. die Clientrichtlinie herunter, wenn eine Änderung der Konfiguration in der Configuration Manager-Konsole vorgenommen wurde, und Sie nicht auf den nächsten geplanten Download warten möchten.  

-   Weisen Sie manuell einen Client zu einem Configuration Manager-Standort zu, oder suchen Sie nach einem Standort. Geben Sie dann das Domain Name System-Suffix (DNS) für Verwaltungspunkte an, die in DNS veröffentlichen.  

-   Konfigurieren Sie den Clientcache, in dem Dateien vorübergehend gespeichert werden. Löschen Sie anschließend Dateien im Cache, wenn Sie mehr Speicherplatz zum Installieren von Software benötigen.  

-   Konfigurieren von Einstellungen für die internetbasierte Clientverwaltung  

-   Anzeigen von Konfigurationsbasislinien, die auf dem Client bereitgestellt wurden, Initiieren der Kompatibilitätsauswertung und Anzeigen von Kompatibilitätsberichten  
