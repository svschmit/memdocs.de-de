---
title: Clientinstallationsmethoden
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu unterschiedlichen Installationsmethoden für den Configuration Manager-Client.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693838"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Clientinstallationsmethoden in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können andere Methoden verwenden, um Configuration Manager-Clientsoftware zu installieren. Dabei ist sowohl eine einzelne Methode als auch eine Kombination mehrerer Methoden denkbar. In diesem Artikel werden alle Methoden beschrieben, damit Sie die für Ihre Organstation geeignete auswählen können.  

## <a name="client-push-installation"></a>Clientpushinstallation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Kann für die Installation des Clients auf einem einzelnen Computer, einer Sammlung von Computern oder den Ergebnissen einer Abfrage verwendet werden.  

-   Kann zum automatischen Installieren des Clients auf allen ermittelten Computern verwendet werden.  

-   Verwendet automatisch die Clientinstallationseigenschaften, die im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** definiert sind.  

#### <a name="disadvantages"></a>Nachteile  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn mithilfe von Push auf große Sammlungen übertragen wird.  

-   Kann nur auf Computern verwendet werden, die von Configuration Manager ermittelt wurden.  

-   Kann nicht verwendet werden, um Clients in einer Arbeitsgruppe zu installieren.  

-   Es muss ein Clientpushinstallationskonto angegeben werden, das über Administratorrechte für den betreffenden Clientcomputer verfügt.  

-   Für die Windows-Firewall müssen Ausnahmen auf den Clientcomputern konfiguriert werden.   

-   Sie können die Clientpushinstallation nicht abbrechen. Configuration Manager versucht, den Client auf allen ermittelten Ressourcen zu installieren. Bei Fehlern wird bis zu sieben Tage lang versucht, die Installation durchzuführen.  

Weitere Informationen finden Sie unter [Installieren von Clients mittels Clientpush](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Auf einem Softwareupdatepunkt basierende Installation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Kann die vorhandene Softwareupdateinfrastruktur für die Verwaltung der Clientsoftware verwenden.  

-   Wenn WSUS (Windows Server Update Services) und Gruppenrichtlinieneinstellungen in Active Directory Domain Services ordnungsgemäß konfiguriert sind, kann die Clientsoftware automatisch auf neuen Computern installiert werden.  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Wenn der Client entfernt wird, wird er durch diese Methode erneut installiert.  

-   Keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer erforderlich.  

#### <a name="disadvantages"></a>Nachteile  

-   Erfordert eine funktionsfähige Softwareupdateinfrastruktur als Voraussetzung.  

-   Für die Clientinstallation und für Softwareupdates muss derselbe Server verwendet werden. Dieser Server muss sich an einem primären Standort befinden.  

-   Sie müssen ein Gruppenrichtlinienobjekt in Active Directory Domain Services mit dem aktiven Softwareupdatepunkt des Clients und dem Port konfigurieren, um neue Clients zu installieren.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie Gruppenrichtlinieneinstellungen zur Bereitstellung von Computern mit Clientinstallationseigenschaften verwenden.  

Weitere Informationen finden Sie unter [How to install clients with software update-based installation (Installieren von Clients mithilfe einer auf einem Softwareupdate basierenden Installation)](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Gruppenrichtlinieninstallation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer erforderlich.  

#### <a name="disadvantages"></a>Nachteile  

-   Wenn eine große Anzahl von Clients installiert wird, kann dies beträchtlichen Netzwerkdatenverkehr verursachen.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie die Clientinstallationseigenschaften mithilfe von Gruppenrichtlinieneinstellungen den Computern des Standorts hinzufügen.  

Weitere Informationen finden Sie unter [Installieren von Clients mit einer Gruppenrichtlinie](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Anmeldeskriptinstallation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

#### <a name="disadvantages"></a>Nachteile  

-   Wenn in kurzer Zeit eine große Anzahl von Clients installiert wird, kann dies beträchtlichen Netzwerkdatenverkehr verursachen.  

-   Wenn Benutzer sich nicht regelmäßig beim Netzwerk anmelden, kann die Installation auf allen Clientcomputern sehr lange dauern.  

Weitere Informationen finden Sie unter [Installieren von Clients mithilfe von Anmeldeskripts](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Manuelle Installation  

**Unterstützte Clientplattform:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Kann zu Testzwecken verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

#### <a name="disadvantages"></a>Nachteile  

-   Keine Automatisierung, daher zeitaufwändig.  

Weitere Informationen zum manuellen Installieren des Clients auf unterschiedlichen Plattformen finden in den folgenden Artikeln:  

-   [Bereitstellen von Clients auf Windows-Computern](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Bereitstellen von Clients auf UNIX- und Linux-Servern](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Bereitstellen von Clients auf Macintosh-Computern](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Installation von Microsoft Intune-MDM

**Unterstützte Clientplattform:** Windows 10

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer erforderlich.  

-   Authentifizierung mit Azure Active Directory ist möglich.  

-   Computer im Internet können installiert und zugewiesen werden.  

-   Automatische Verwendung mit Windows Autopilot und Microsoft Intune für die Co-Verwaltung möglich.  

#### <a name="disadvantages"></a>Nachteile  

-   Zusätzliche Technologien, die nicht in Configuration Manager verfügbar sind, sind erforderlich.  

-   Ein Gerät muss auch dann auf das Internet zugreifen können, wenn es nicht internetbasiert ist.  

Weitere Informationen finden Sie in den folgenden Artikeln:  

-   [Installieren von Clients für mit Intune MDM verwaltete Windows-Geräte](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Installieren und Zuweisen von Windows 10-Clients in Configuration Manager mit Authentifizierung über Azure AD](../deploy-clients-cmg-azure.md)  

