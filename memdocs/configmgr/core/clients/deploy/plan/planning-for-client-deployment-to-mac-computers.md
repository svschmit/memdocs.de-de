---
title: Planen der Clientbereitstellung auf Macintosh-Computern
titleSuffix: Configuration Manager
description: Planen Sie die Clientbereitstellung auf Macintosh-Computern in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693718"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Planen der Clientbereitstellung auf Macintosh-Computern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können den Configuration Manager-Client auf Macintosh-Computern installieren, auf denen Mac OS X ausgeführt wird, und die folgenden Verwaltungsfunktionen verwenden:  

- **Hardwareinventur**  

   Mit der Configuration Manager-Hardwareinventur können Sie Informationen über die Hardware und die installierten Anwendungen auf Macintosh-Computern sammeln. Diese Informationen können dann in der Configuration Manager-Konsole im Ressourcen-Explorer angezeigt und zum Erstellen von Sammlungen, Abfragen und Berichten verwendet werden. Weitere Informationen finden Sie unter [Anzeigen der Hardwareinventur mit dem Ressourcen-Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Die folgenden Hardwareinformationen über Macintosh-Computer werden von Configuration Manager gesammelt:  

  -   Prozessor  

  -   Computersystem  

  -   Laufwerk  

  -   Datenträgerpartition  

  -   Netzwerkkarte  

  -   Betriebssystem  

  -   Dienst  

  -   Prozess  

  -   Installierte Software  

  -   Computersystemprodukt  

  -   USB-Controller  

  -   USB-Gerät  

  -   CD-ROM-Laufwerk  

  -   Videocontroller  

  -   Desktopmonitor  

  -   Tragbare Batterie  

  -   Physischer Speicher  

  -   Drucker  

  > [!IMPORTANT]  
  >  Die Hardwareinformationen, die bei der Hardwareinventur über Macintosh-Computer gesammelt werden, können nicht erweitert werden.  

- **Kompatibilitätseinstellungen**  

   Mit den Configuration Manager-Kompatibilitätseinstellungen können Sie die Kompatibilität von Mac OS X-Einstellungen (PLIST) anzeigen und diese Einstellungen wiederherstellen. Beispielsweise können Sie Einstellungen für die Startseite im Safari-Webbrowser erzwingen oder sicherstellen, dass die Apple-Firewall aktiviert ist. Sie können Einstellungen in Mac OS X auch mit Shellskripts überwachen und wiederherstellen.  

- **Anwendungsverwaltung**  

   Configuration Manager kann Software für Macintosh-Computer bereitstellen. Sie können die folgenden Softwareformate auf Macintosh-Computern bereitstellen:  

  -   Apple Disk Image (.DMG)  

  -   Meta Package-Datei (.MPKG)  

  -   Mac OS X Installer-Paket (.PKG)  

  -   Mac OS X-Anwendung (.APP)  

  Wenn Sie den Configuration Manager-Client auf Macintosh-Computern installieren, können Sie die folgenden Verwaltungsfunktionen nicht verwenden, die vom Configuration Manager-Client auf Windows-basierten Computern unterstützt werden:  

- Clientpushinstallation  

- Betriebssystembereitstellung  

- Softwareupdates  

  > [!NOTE]  
  >  Mit der Configuration Manager-Anwendungsverwaltung können Sie erforderliche Mac OS X-Softwareupdates auf Macintosh-Computern bereitstellen. Darüber hinaus können Sie mithilfe von Kompatibilitätseinstellungen sicherstellen, dass auf Computern alle erforderlichen Softwareupdates verfügbar sind.  

- Wartungsfenster  

- Remotesteuerung  

- Energieverwaltung  

- Clientprüfung des Clientstatus und Wiederherstellung  

  Weitere Informationen zum Installieren und Konfigurieren des Configuration Manager-Macintosh-Clients finden Sie unter [Bereitstellen von Clients auf Macintosh-Computern](../../../../core/clients/deploy/deploy-clients-to-macs.md).
