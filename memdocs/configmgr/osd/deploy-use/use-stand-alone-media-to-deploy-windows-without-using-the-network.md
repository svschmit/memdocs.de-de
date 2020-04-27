---
title: Verwenden eigenständiger Medien zum Bereitstellen von Windows
titleSuffix: Configuration Manager
description: Verwenden Sie eigenständige Medien in Configuration Manager, um Windows bei eingeschränkter Bandbreite als Option zum Aktualisieren, Installieren oder Upgraden von Computern bereitzustellen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709038"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks

*Gilt für: Configuration Manager (Current Branch)*

Eigenständige Medien in Configuration Manager enthalten alles, was zur Bereitstellung des Betriebssystems auf einem Computer erforderlich ist. Hierzu gehören das Startabbild, das Betriebssystemabbild und die Tasksequenz zum Installieren des Betriebssystems sowie von Anwendungen, Treibern usw. Mit eigenständigen Medienbereitstellungen können Sie unter folgenden Umständen Betriebssysteme bereitstellen:  

-   In Umgebungen, in denen es nicht praktikabel ist, ein Betriebssystemabbild oder anderen große Pakete über das Netzwerk zu kopieren;  

-   in Umgebungen ohne Netzwerkverbindung oder mit geringer Netzwerkbandbreite.  

Sie können eigenständige Medien in folgenden Szenarien für die Betriebssystembereitstellung verwenden:  

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Upgraden von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)  

  Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und lesen Sie dann die folgenden Abschnitte, um die eigenständigen Medien vorzubereiten und zu erstellen.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Tasksequenzaktionen, die bei Verwendung eigenständiger Medien nicht unterstützt werden  
 Wenn Sie die Schritte in einem der unterstützten Szenarien für die Betriebssystembereitstellung abgeschlossen haben, wurde die Tasksequenz zum Bereitstellen bzw. Aktualisieren des Betriebssystems erstellt, und alle dazugehörigen Inhalte wurden an einen Verteilungspunkt verteilt. Wenn Sie eigenständige Medien verwenden, werden die folgenden Aktionen in der Tasksequenz nicht unterstützt:  

-   Der Schritt „Treiber automatisch anwenden“ in der Tasksequenz. Die automatische Anwendung von Gerätetreibern aus dem Treiberkatalog wird nicht unterstützt, Sie können aber den Schritt „Treiberpaket anwenden“ auswählen, um Windows Setup eine angegebene Gruppe von Treibern verfügbar zu machen.  

-   Installieren von Softwareupdates  

-   Installieren von Software vor dem Bereitstellen des Betriebssystems  

-   Zuweisen von Benutzern zum Zielcomputer, um die Affinität zwischen Benutzer und Gerät zu unterstützen  

-   Dynamische Paketinstallationen über den Task „Pakete installieren“.  

-   Dynamische Anwendungsinstallationen über den Task „Anwendung installieren“.  

> [!NOTE]  
>  Wenn die Tasksequenz zum Bereitstellen eines Betriebssystems den Schritt [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage) enthält und Sie die eigenständigen Medien an einem Standort der zentralen Verwaltung erstellen, kann ein Fehler auftreten. Der Standort der zentralen Verwaltung verfügt nicht über die erforderlichen Clientkonfigurationsrichtlinien, die während der Ausführung der Tasksequenz zum Aktivieren des Softwareverteilungs-Agents benötigt werden. In der Datei „CreateTsMedia.log“ wird möglicherweise der folgenden Fehler angezeigt:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  Sie müssen eigenständige Medien, die den Schritt **Paket installieren** aufweisen, an einem primären Standort erstellen, für den der Softwareverteilungs-Agent aktiviert ist. Alternativ dazu können Sie den Schritt [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) nach dem Schritt [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) und vor dem ersten Schritt **Paket installieren** hinzufügen. Im Schritt **Befehlszeile ausführen** wird ein WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor der Ausführung des ersten Schritts "Paket installieren" zu aktivieren. Sie können im Tasksequenzschritt **Befehlszeile ausführen** Folgendes verwenden:  
>   
>  **Befehlszeile:** **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Wenn Sie eigenständige Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für die Medien zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :  

-   **Configuration Manager-Clients, Medien und PXE**  

-   **Nur Medien und PXE**  

-   **Nur Medien und PXE (ausgeblendet)**  

## <a name="create-the-stand-alone-media"></a>Erstellen der eigenständigen Medien  
 Sie können angeben, ob das eigenständige Medium ein USB-Flashlaufwerk oder ein CD/DVD-Satz ist. Der Computer, der die Medien startet, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Installieren des Betriebssystems von eigenständigen Medien  
 Legen Sie die eigenständigen Medien in ein startfähiges Laufwerk des Computers ein. Schalten Sie dann den Computer ein, um das Betriebssystem zu installieren.  
