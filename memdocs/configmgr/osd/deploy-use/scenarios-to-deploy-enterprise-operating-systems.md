---
title: Szenarien für die Bereitstellung von Unternehmensbetriebssystemen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Szenarios zur Bereitstellung von Unternehmensbetriebssystemen mit Configuration Manager.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8304ba7384eba2fc7bfa41d4caf5a256380931c5
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546636"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Szenarios zur Bereitstellung von Unternehmensbetriebssystemen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die folgenden OS-Bereitstellungsszenarios sind im Configuration Manager verfügbar:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Upgrade von Windows auf die neueste Version
Dieses Szenario aktualisiert das BS auf Computern, auf denen derzeit Windows 7, Windows 8.1 oder Windows 10 ausgeführt wird. Bei dem Upgradevorgang werden die Anwendungen, Einstellungen und Benutzerdaten auf dem Computer beibehalten. Es gibt keine externen Abhängigkeiten, wie z. B. das Windows ADK. Dieser Prozess kann schneller und stabiler als herkömmliche BS-Bereitstellungen sein.  

Weitere Informationen finden Sie unter [Aktualisieren von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md).

#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot für vorhandene Geräte
<!--3607717, fka 1358333-->
Ab Version 1810 ist Windows Autopilot für vorhandene Geräte mit Windows 10, Version 1809 oder höher verfügbar. Mit dieser Funktion können Sie ein Reimaging für ein Windows 7-Gerät für den benutzergesteuerten Windows Autopilot-Modus mit einer einzigen Configuration Manager-Tasksequenz durchführen und das Gerät bereitstellen.

Weitere Informationen finden Sie unter [Windows Autopilot für vorhandene Geräte](../../../autopilot/existing-devices.md).

#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows
In diesem Szenario wird ein vorhandener Computer partitioniert und formatiert (zurückgesetzt), und ein neues BS wird auf dem Computer installiert. Sie können Einstellungen und Benutzerdaten nach der Installation des BS migrieren.  

Weitere Informationen finden Sie unter [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)
In diesem Szenario wird ein BS auf einem neuen Computer installiert. Dies ist eine Neuinstallation des BS ohne Migration von Einstellungen oder Benutzerdaten.  

Weitere Informationen finden Sie unter [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen
In diesem Szenario wird ein BS auf einem neuen Computer installiert. Optional können Sie Einstellungen und Benutzerdaten vom alten Computer auf den neuen Computer migrieren.  

Weitere Informationen finden Sie unter [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md).


