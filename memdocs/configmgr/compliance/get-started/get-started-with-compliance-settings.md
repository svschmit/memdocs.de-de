---
title: Erste Schritte mit Konformitätseinstellungen
titleSuffix: Configuration Manager
description: Lernen Sie wichtige Konzepte kennen, und erfahren Sie mehr zur Funktionsweise von Konformitätseinstellungen
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d5e042980a1fa6fb8a92abcff6d3938874cf6b38
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694592"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Erste Schritte mit Konformitätseinstellungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie Configuration Manager-Konformitätseinstellungen erstellen, sollten sie erst die grundlegenden Konzepte kennen und ihre Funktionsweise verstehen.  



## <a name="how-compliance-settings-work"></a>So funktionieren Konformitätseinstellungen  
Mit den Kompatibilitätseinstellungen können Sie die Clients in Ihrer Organisation verwalten.  

Konfigurationselemente werden in zwei Hauptkategorien unterteilt:  

- **Einstellungen für Geräte, die mit dem Configuration Manager-Client verwaltet werden**: Diese Geräte sind üblicherweise Geräte, auf denen Sie Configuration Manager-Clientsoftware installiert haben, mit der Sie das jeweilige Gerät verwalten können.  

- **Einstellungen für Geräte, die ohne den Configuration Manager-Client verwaltet werden**: Diese Geräte sind üblicherweise Geräte, die mit Microsoft Intune oder lokaler Configuration Manager-Geräteverwaltung verwaltet werden.  



## <a name="what-devices-are-supported"></a>Welche Geräte werden unterstützt?  

| Gerätetyp | Weitere Informationen |  
|------------|----------------------|  
| Windows-PCs (mit dem Configuration Manager-Client) | Erstellen Sie benutzerdefinierte Konfigurationselemente, um Objekte wie Registrierungsschlüssel, Dateien und Active Directory-Attribute zu bewerten.<br /><br /> Wenn Sie den Windows 10-Konfigurationselementtyp verwenden, wählen Sie Einstellungen aus einer vordefinierten Liste aus. |  
| Windows-PCs (mithilfe von lokalem MDM registriert) | Sie wählen Einstellungen aus einer vordefinierten Liste aus. |  
| Windows Phone-Geräte (mithilfe von lokalem MDM registriert) | Sie wählen Einstellungen aus einer vordefinierten Liste aus. |  
| Macintosh-Computer (mit dem Configuration Manager-Client) | Erstellen Sie Konfigurationselemente, um Objekte wie macOS-Einstellungen und von einem Skript zurückgegebene Ergebnisse zu bewerten. |  



## <a name="what-is-a-configuration-item"></a>Was ist ein Konfigurationselement?  
Ein Konfigurationselement ist ein Container, der bestimmte Informationen speichert. Die von Ihnen festgelegte Konfiguration hängt vom Konfigurationselementtyp ab. Folgende Konfigurationselemente können die folgenden Informationen enthalten:

- **Informationen zur Erkennungsmethode** steht nur für Windows-Konfigurationselemente zur Verfügung, die Anwendungseinstellungen enthalten. Dabei wird erkannt, ob eine Anwendung installiert ist. Diese Erkennung verwendet die Windows Installer-Datei der Anwendung oder ein benutzerdefiniertes Skript.  

- **Einstellungen** repräsentiert die geschäftlichen oder technischen Maßnahmen, die zur Bewertung der Kompatibilität auf Clientcomputern verwendet werden. Konfigurieren Sie eine neue Einstellung, oder navigieren Sie zu einer bestehenden Einstellung auf einem Referenzcomputer.  

- Mit **Konformitätsregeln** werden die Bedingungen angegeben, mit denen die Konformität einer Konfigurationselementeinstellung definiert wird. Damit ein Client eine Einstellung auf Kompatibilität prüfen kann, muss sie über mindestens eine Kompatibilitätsregel verfügen. Einige Einstellungen korrigieren nicht kompatible Werte. Erstellen Sie neue Regeln, oder navigieren Sie zu einer vorhandenen Einstellung innerhalb eines beliebigen Konfigurationselements, und wählen Sie dort Regeln aus.  

- **Unterstützte Plattformen** sind die von Ihnen definierten Geräteplattformen, auf denen das Konfigurationselement auf Kompatibilität geprüft wird. Wenn Sie ein Konfigurationselement auf einem Gerät bereitstellen, das nicht in der Liste der unterstützten Plattformen enthalten ist, wird das Gerät nicht auf Kompatibilität bewertet.  



## <a name="what-is-a-configuration-baseline"></a>Was ist eine Konfigurationsbasislinie?  
Definieren Sie eine Konfigurationsbaseline, die die zu prüfenden Konfigurationselemente einbezieht. Beziehen Sie außerdem die Einstellungen und Regeln ein, die den erforderlichen Konformitätsgrad beschreiben. Importieren Sie diese Konfigurationsdaten aus den Configuration Manager-Konfigurationspaketen. Diese Konfigurationspakete werden von Microsoft und anderen Vendoren festgelegt. Alternativ können Sie neue Konfigurationselemente und Konfigurationsbaselines erstellen.  

Nachdem Sie eine Konfigurationsbaseline definiert haben, können Sie sie in Benutzer- und Gerätesammlungen bereitstellen. Dann prüft der Client gemäß eines Zeitplans die Baselineeinstellungen auf Konformität. Sie können auf einem Gerät mehrere Konfigurationsbaselines bereitstellen. Diese Granularität führt zu einer höheren Steuerbarkeit der Konformität. 

Von Clientgeräten wird die Konformität anhand jeder zugewiesenen Konfigurationsbasislinie ausgewertet. Die Ergebnisse werden dem Standort sofort über Zustands- und Statusmeldungen gemeldet. Wenn ein Gerät aktuell nicht mit dem Netzwerk verbunden ist, darauf aber die Konfigurationsbaseline heruntergeladen wurde, wird die Konformität der Konfigurationselemente trotzdem geprüft. Sobald das Gerät wieder über eine Verbindung zum Netzwerk verfügt, sendet es die Konformitätsinformationen.  

### <a name="monitoring-configuration-baselines"></a>Überwachen von Konfigurationsbaselines
- Überwachen Sie die Ergebnisse der Konformitätsprüfung in der Configuration Manager-Konsole (unter **Bereitstellungen** > **Überwachung**). Beispiel:
  - Häufige Gründe für eine Nicht-Konformität
  - Fehler
  - Die Zahl der betroffenen Benutzer und Geräte
- Führen Sie Berichte zu Konformitätseinstellungen mit zusätzlichen Informationen durch. Beispiel:
  - Welche Geräte sind konform bzw. nicht konform?
  - Welches Element der Konfigurationsbaseline verursacht die Nicht-Konformität eines Computers?
- Sehen Sie sich die Ergebnisse der Konformitätsprüfung von Windows-Computern an, auf denen der Configuration Manager-Client ausgeführt wird. Öffnen Sie die **Configuration Manager**-Einstellungen, und wechseln Sie zur Registerkarte **Konfiguration**.  



## <a name="user-data-and-profiles-configuration-items"></a>Konfigurationselemente für Benutzerdaten und Profile  
Konfigurationselemente für Benutzerdaten und -profile enthalten Einstellungen, die die Verwaltung von Folgendem auf Windows 8-Computern steuern:  
- Umleitung des Ordners
- Offlinedateien
- Roamingprofile  

Stellen Sie diese Konfigurationselement in Benutzersammlungen bereit. Überwachen Sie die Konformität in der Configuration Manager-Konsole im Knoten **Überwachung**. Im Gegensatz zu anderen Konfigurationselementen fügen Sie diese nicht zu Konfigurationsbaselines hinzu, bevor Sie sie bereitstellen. Stellen Sie sie über **Bereitstellen** im Menüband direkt bereit.  

Ausführlichere Informationen finden Sie unter [Erstellen von Konfigurationselementen für Benutzerdaten und -profile](../deploy-use/create-user-data-and-profiles-configuration-items.md).  



## <a name="remote-connection-profiles"></a>Remoteverbindungsprofile  
Remoteverbindungsprofile stellen eine Reihe von Tools und Ressourcen zur Verfügung, mit deren Hilfe Sie Remoteverbindungeinstellungen erstellen, bereitstellen und überwachen können. Durch Bereitstellen dieser Einstellungen auf Geräten erleichtern Sie den Endbenutzern das Herstellen einer Verbindung mit dem Unternehmensnetzwerk.  

Weitere Informationen finden Sie unter [Erstellen von Remoteverbindungsprofilen](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Upgrade von Windows-Edition
Die Upgraderichtlinie für die Edition ermöglicht das automatische Upgrade von Geräten, die bestimmte Versionen von Windows 10 ausführen, auf eine neuere Version. Diese Richtlinie stellt einen neuen Product Key oder eine neue Lizenzdatei zur Verfügung, die vom Gerät für das Upgrade verwendet wird.

Ausführlichere Informationen finden Sie unter [Aktualisieren von Windows-Geräten mit der Editionsupgraderichtlinie in System Center Configuration Manager](../deploy-use/upgrade-windows-version.md).

## <a name="microsoft-edge-legacy-browser-profiles"></a>Browserprofile für Microsoft Edge Legacy
<!-- 1357310 -->
Kunden, die den Webbrowser [Microsoft Edge Legacy](/microsoft-edge/deploy/) auf Windows 10-Clients nutzen, erstellen eine Configuration Manager-Konformitätsrichtlinie, um die Browsereinstellungen zu konfigurieren.

Weitere Informationen finden Sie unter [Browserprofile für Microsoft Edge Legacy](../deploy-use/browser-profiles.md).