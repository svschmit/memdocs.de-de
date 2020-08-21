---
title: Verwalten von VDI-Clients
titleSuffix: Configuration Manager
description: Verwalten Sie Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur (Virtual Desktop Infrastructure, VDI).
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d79edb5ad1a60c5876163281ec5c1d1c17eff0a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692807"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Verwalten von Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur (Virtual Desktop Infrastructure, VDI)

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt die Installation des Configuration Manager-Clients in den folgenden Szenarien einer virtuellen Desktopinfrastruktur (VDI):

- **Persönliche virtuelle Computer**: Der virtuelle Computer (VM) verwaltet die Benutzerdaten und Einstellungen zwischen den Sitzungen.

- **Remotedesktopdienste-Sitzungen**: Hosten Sie mehrere gleichzeitige Clientsitzungen auf einem zentralisierten Server. Benutzer stellen eine Verbindung mit einer Sitzung her und führen Anwendungen auf diesem Server aus.

- **Gepoolte virtuelle Computer**: Der virtuelle Computer wird nicht zwischen Sitzungen beibehalten. Wenn ein Benutzer eine Sitzung schließt, verwirft die virtuelle Umgebung alle Daten und Einstellungen. Gepoolte virtuelle Computer sind nützlich, wenn Sie Remotedesktopdienste nicht verwenden können. Beispielsweise, wenn eine erforderliche Anwendung nicht auf dem Windows-Server ausgeführt werden kann, der die Clientstzungen hostet.

- **Windows Virtual Desktop**: En Desktop- und App-Virtualisierungsdienst, der auf Microsoft Azure ausgeführt wird. Verwenden Sie ab Version 1906 Configuration Manager zum Verwalten dieser unter Windows ausgeführten virtuellen Geräte in Azure.

## <a name="personal-vms"></a>Persönliche VMs

Persönliche VMs werden von Configuration Manager wie physische Computer behandelt. Sie können den Configuration Manager-Client auf dem VM-Image vorinstallieren oder nach der Bereitstellung installieren.

Weitere Informationen finden Sie unter [Unterstützung für Virtualisierungsumgebungen](../../../plan-design/configs/support-for-virtualization-environments.md).

## <a name="remote-desktop-services"></a>Remotedesktopdienste

Sie installieren den Configuration Manager-Client nicht für einzelne Remotedesktopsitzungen. Installieren Sie ihn einmal auf dem Server, der Remotedesktopdienste hostet. Sie können alle Configuration Manager-Clientfunktionen auf dem Remotedesktopdienste-Server verwenden.

Weitere Informationen finden Sie unter [Willkommen bei den Remotedesktopdiensten](/windows-server/remote/remote-desktop-services/welcome-to-rds).

## <a name="pooled-vms"></a>Gepoolte VMs

Wenn Sie einen gepoolten virtuellen Computer außer Betrieb nehmen, gehen alle von Configuration Manager vorgenommenen Änderungen verloren.

Da die VM möglicherweise nur für einen kurzen Zeitraum funktionstüchtig ist, geben einige Configuration Manager-Features vielleicht keine relevanten Daten zurück. Dazu zählen beispielsweise Hardware- und Softwareinventur sowie Softwaremessungen. Erwägen Sie, gepoolte VMs von Inventurtasks auszuschließen.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="other-considerations"></a>Weitere Überlegungen

Bei der Virtualisierung ist die Ausführung mehrerer Configuration Manager-Clients auf dem gleichen physischen Computer möglich. Aus diesem Grund haben viele Clientvorgänge eine integrierte zufällige Verzögerung für geplante Aktionen. Das sind z. B. Hardware- und Softwareinventur, Antischadsoftwareüberprüfungen, Softwareinstallationen und Softwareupdateüberprüfungen. Hierdurch lassen sich die Prozessorauslastung und die Datenübertragung für einen Server mit mehreren virtuellen Computer, auf denen der Configuration Manager-Client ausgeführt wird, leichter verteilen.

Diese zufällige Verzögerung wird auch von Configuration Manager-Clients verwendet, die sich nicht in virtualisierten Umgebungen befinden, ausgenommen Windows Embedded-Clients im Wartungsmodus. Dieses Verhalten trägt dazu bei, Netzwerkbandbreiten-Spitzen zu vermeiden. Außerdem wird die CPU-Verarbeitung auf Standortsystemen reduziert, z. B. auf Verwaltungspunkt und Standortserver. Das Verzögerungsintervall hängt von der Configuration Manager-Funktionalität ab. Ein Beispiel hierzu finden Sie unter [Informationen zu Clienteinstellungen – Zufällige Stichtaganordnung deaktivieren](../about-client-settings.md#disable-deadline-randomization).

Zur Unterstützung der Configuration Manager-Clientleistung in virtuellen Umgebungen, die mehrere Benutzersitzungen unterstützen, wird die Benutzerrichtlinie standardmäßig deaktiviert. Ab Version 1910 können Sie die Benutzerrichtlinie in diesem Szenario aktivieren. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen in Configuration Manager – Aktivieren der Benutzerrichtlinie für mehrere Benutzersitzungen](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).