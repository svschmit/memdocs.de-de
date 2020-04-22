---
title: Sicherheit und Datenschutz für die Remotesteuerung
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu Sicherheit und Datenschutz für die Remotesteuerung in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696398"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Sicherheit und Datenschutz für die Remotesteuerung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erhalten Sie Informationen zu Sicherheit und Datenschutz für die Remotesteuerung in Configuration Manager.  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Bewährte Sicherheitsmethoden für die Remotesteuerung  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden an, wenn Sie Clientcomputer mithilfe von Remotesteuerung verwalten:  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Wenn Sie eine Verbindung mit einem Remotecomputer herstellen, dann fahren Sie nicht fort, wenn NTLM-Authentifizierung statt Kerberos-Authentifizierung verwendet wird.|Wenn von Configuration Manager festgestellt wird, dass die Remotesteuerungssitzung mithilfe von NTLM statt Kerberos authentifiziert wird, erhalten Sie eine Warnmeldung, dass die Identität des Remotecomputers nicht überprüft werden kann. Setzen Sie die Remotesteuerungssitzung nicht fort. Das NTLM-Authentifizierungsprotokoll ist schwächer als Kerberos und anfällig für Replay sowie Identitätsvortäuschung.|  
|Aktivieren Sie nicht die Freigabe der Zwischenablage im Remotesteuerungsviewer.|Die Zwischenablage unterstützt neben Text auch Objekte wie ausführbare Dateien und kann während der Remotesteuerungssitzung vom Benutzer des Hostcomputers zum Ausführen von Programmen auf dem Quellcomputer verwendet werden.|  
|Geben Sie bei der Remoteverwaltung von Computern keine Kennwörter für privilegierte Konten ein.|Eine Software, die Tastatureingaben überwacht, kann das Kennwort möglicherweise ermitteln. Wenn das auf dem Clientcomputer ausgeführte Programm nicht das Programm ist, das der Remotesteuerungsbenutzer erwartet, kann dieses Programm das Kennwort unrechtmäßig erfassen. Sind Konten und Kennwörter erforderlich, sollte der Endbenutzer diese eingeben.|  
|Sperren Sie während der Remotesteuerungssitzung Tastatur und Maus.|Wenn von Configuration Manager erkannt wird, dass die Remotesteuerungsverbindung beendet wurde, werden Tastatur und Maus automatisch von Configuration Manager gesperrt, sodass kein Benutzer die offene Remotesteuerungssitzung übernehmen kann. Diese Erkennung findet u. U. jedoch nicht sofort statt, und sie erfolgt gar nicht, wenn der Remotesteuerungsdienst beendet wurde.<br /><br /> Wählen Sie die Aktion **Remotetastatur und -maus sperren** im Fenster **ConfigMgr-Remotesteuerung** aus.|  
|Gestatten Sie Benutzern nicht das Konfigurieren der Remotesteuerungseinstellungen im Softwarecenter.|Aktivieren Sie nicht die Clienteinstellung **Benutzer können Richtlinien- oder Benachrichtigungseinstellungen im Softwarecenter ändern** , um zu vermeiden, dass Benutzer ausspioniert werden können. Wenn sie von einem Benutzer geändert wird, können andere Benutzer auf demselben Computer diesen über eine Remoteverbindung anzeigen. <br /><br />**Diese Einstellung gilt für den Computer, nicht für den angemeldeten Benutzer.**|  
|Aktivieren Sie das Windows-Firewall-Profil **Domäne** .|Aktivieren Sie die Clienteinstellung **Remotesteuerung auf Clients aktivieren - Firewallausnahmeprofile** und wählen Sie die Windows-Firewall **Domäne** für die Computer im Intranet.|  
|Wenn Sie sich während einer Remotesteuerungssitzung abmelden und als anderer Benutzer wieder anmelden, dann achten Sie darauf, sich abzumelden, bevor Sie die Remotesteuerungssitzung beenden.|Wenn Sie sich nicht wie beschrieben abmelden, bleibt die Sitzung geöffnet.|  
|Gewähren Sie Benutzern keine lokalen Administratorrechte.|Wenn Sie Benutzern lokale Administratorrechte gewähren, könnten sie Ihre Remotesteuerungssitzung übernehmen oder Ihre Anmeldeinformationen gefährden.|  
|Verwenden Sie zum Konfigurieren von Remoteunterstützungseinstellungen entweder Gruppenrichtlinien oder Configuration Manager, aber nicht beide zusammen.|Sie können Configuration Manager oder Gruppenrichtlinien verwenden, um Konfigurationsänderungen an den Remoteunterstützungseinstellungen vorzunehmen. Wenn Gruppenrichtlinien auf dem Client aktualisiert werden, wird der Prozess standardmäßig optimiert, indem nur die Richtlinien geändert werden, die auf dem Server geändert wurden. Configuration Manager ändert die Einstellungen in der lokalen Sicherheitsrichtlinie, die nicht überschrieben werden darf, es sei denn, das Gruppenrichtlinienupdate wird erzwungen.<br /><br /> Das Festlegen der Richtlinien an beiden Orten kann jedoch zu inkonsistenten Ergebnissen führen. Wählen Sie eine dieser Methoden aus, um die Remoteunterstützungseinstellungen zu konfigurieren.|  
|Aktivieren Sie die Clienteinstellung **Benutzer zur Vergabe der Berechtigung für Remotesteuerung auffordern**.|Auch wenn es Möglichkeiten gibt, diese Clienteinstellung zu umgehen, die den Benutzer auffordert, die Remotesteuerungssitzung zu bestätigen, aktivieren Sie die Einstellung dennoch, um die Risiken zu reduzieren, dass Benutzer bei der Arbeit an vertraulichen Aufgaben ausgespäht werden.<br /><br /> Halten Sie zusätzlich die Benutzer dazu an, den Kontennamen zu überprüfen, der während der Remotesteuerungssitzung angezeigt wird, und die Verbindung zu trennen, wenn sie den Verdacht haben, dass das Konto nicht autorisiert ist.|  
|Begrenzen Sie die Liste der zugelassenen Viewer.|Benutzer benötigen keine lokalen Administratorrechte, um die Remotesteuerung zu verwenden.|  

### <a name="security-issues-for-remote-control"></a>Sicherheitsprobleme bei der Remotesteuerung  
 Das Verwalten von Clientcomputern mit der Remotesteuerung birgt folgende Sicherheitsprobleme:  

-   Betrachten Sie Remotesteuerungs-Überwachungsmeldungen nicht als zuverlässig.  

     Wenn Sie eine Remotesteuerungssitzung starten und sich dann mit alternativen Anmeldeinformationen anmelden, werden die Überwachungsmeldungen vom ursprünglichen Konto gesendet und nicht von dem Konto mit den alternativen Anmeldeinformationen.  

     Es werden keine Überwachungsmeldungen gesendet, wenn Sie die Binärdateien zur Remotesteuerung kopieren, anstatt die Configuration Manager-Konsole zu installieren, und dann die Remotesteuerung an der Eingabeaufforderung ausführen.  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Datenschutzinformationen zur Remotesteuerung  
 Die Remotesteuerung ermöglicht das Anzeigen aktiver Sitzungen auf Configuration Manager-Clientcomputern, und möglicherweise aller auf diesen Computern gespeicherten Informationen. Die Remotesteuerung ist standardmäßig nicht aktiviert.  

 Sie können die Remotesteuerung so konfigurieren, dass Benutzer vor Beginn einer Remotesteuerungssitzung eine deutliche Ankündigung erhalten und zustimmen können. Es ist allerdings auch möglich, Benutzer ohne deren Erlaubnis oder Wissen zu überwachen. Sie können die Zugriffsstufe "Nur anzeigen" konfigurieren, sodass per Remotesteuerung nichts verändert werden kann, oder "Vollzugriff". Während der Remotesteuerungssitzung wird das Konto des Administrators angezeigt, der die Verbindung herstellt, damit die Benutzer erkennen können, wer eine Verbindung mit ihrem Computer herstellt.  

 In der Standardeinstellung von Configuration Manager werden der lokalen Administratorgruppe Remotesteuerungsberechtigungen gewährt.  

 Berücksichtigen Sie beim Konfigurieren der Remotesteuerung Ihre Datenschutzanforderungen.  
