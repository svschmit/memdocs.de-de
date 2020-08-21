---
title: Verwenden eigenständiger Medien zum Bereitstellen von Windows
titleSuffix: Configuration Manager
description: Verwenden Sie eigenständige Medien in Configuration Manager, um Windows bei eingeschränkter Bandbreite als Option für die Aktualisierung, Installation oder das Upgrade von Computern bereitzustellen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124651"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks

*Gilt für: Configuration Manager (Current Branch)*

Eigenständige Medien in Configuration Manager enthalten alle Elemente, die zur Bereitstellung eines Betriebssystems auf einem Computer erforderlich sind. Die Medien enthalten das Startimage, das Betriebssystemimage, die Tasksequenzrichtlinie sowie Anwendungen, Treiber und vieles mehr. Mithilfe eigenständiger Medien können Sie unter folgenden Umständen Betriebssysteme bereitstellen:

- In Umgebungen, in denen es nicht praktikabel ist, ein Betriebssystemimage oder andere große Pakete über das Netzwerk zu kopieren.

- In Umgebungen ohne Netzwerkverbindung oder mit geringer Netzwerkbandbreite.

Verwenden Sie eigenständige Medien in folgenden Szenarien für die Betriebssystembereitstellung:

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Upgraden von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)

Führen Sie die Schritte in einem dieser Szenarien für die Betriebssystembereitstellung aus. Bereiten Sie dann anhand der folgenden Abschnitte die eigenständigen Medien vor und erstellen Sie sie.

## <a name="unsupported-task-sequence-actions"></a>Nicht unterstützte Tasksequenzaktionen

Wenn Sie eigenständige Medien verwenden, unterstützt Configuration Manager die folgenden Aktionen in der Tasksequenz nicht:

- Schritt [Treiber automatisch anwenden](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers). Die automatische Anwendung von Gerätetreibern aus dem Treiberkatalog wird nicht unterstützt. Um eine bestimmten Gruppe von Treibern für Windows Setup verfügbar zu machen, verwenden Sie den Schritt [Treiberpaket anwenden](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage).

- Installieren von Softwareupdates

- Installieren von Software vor dem Bereitstellen des Betriebssystems

- Zuweisen von Benutzern zum Zielcomputer, um die Affinität zwischen Benutzer und Gerät zu unterstützen.

- Dynamische Paketinstallationen mit dem Schritt [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage).

- Dynamische Anwendungsinstallationen mit dem Schritt [Anwendung installieren](../understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!NOTE]
> Wenn die Tasksequenz zum Bereitstellen eines Betriebssystems den Schritt **Paket installieren** enthält und Sie die eigenständigen Medien an einem Standort der zentralen Verwaltung (Central Administration Site, CAS) erstellen, kann ein Fehler auftreten. Dem Standort der zentralen Verwaltung fehlen die erforderlichen Clientkonfigurationsrichtlinien, um den Softwareverteilungs-Agent zu aktivieren, wenn die Tasksequenz ausgeführt wird. In der Datei **CreateTsMedia.log** wird möglicherweise der folgenden Fehler angezeigt:
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> Wenn Sie eigenständige Medien verwenden, die den Schritt **Paket installieren** enthalten, erstellen Sie das eigenständige Medium an einem primären Standort, bei dem der Softwareverteilungs-Agent aktiviert ist.
>
> Alternativ dazu können Sie die Tasksequenz bearbeiten und den Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) nach dem Schritt [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) hinzufügen. Im Schritt **Befehlszeile ausführen** wird der folgende WMI-Befehl ausgeführt, um den Softwareverteilungs-Agent vor dem ersten Schritt **Paket installieren** zu aktivieren:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen

Wenn Sie eigenständige Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, konfigurieren Sie die Bereitstellung, um das Betriebssystem für die Medien zur Verfügung zu stellen. Wählen Sie auf der Seite **Bereitstellungseinstellungen** der Bereitstellung für die Einstellung **Verfügbar machen für** eine der folgenden Optionen aus:

- Configuration Manager-Clients, Medien und PXE

- Nur Medien und PXE

- Nur Medien und PXE (ausgeblendet)

## <a name="create-the-standalone-media"></a>Erstellen der eigenständigen Medien

Sie können angeben, ob das eigenständige Medium ein USB-Flashlaufwerk oder ein Satz CDs/DVDs ist. Der Computer, auf dem die Medien gestartet werden, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](create-stand-alone-media.md).

## <a name="install-the-os-from-standalone-media"></a>Installieren des Betriebssystems von eigenständigen Medien

Um das Betriebssystem zu starten, legen Sie das eigenständige Medium im Computer ein, und starten Sie den Computer.

## <a name="next-steps"></a>Nächste Schritte

[Benutzererfahrungen bei der Betriebssystembereitstellung](../understand/user-experience.md#task-sequence-wizard)
