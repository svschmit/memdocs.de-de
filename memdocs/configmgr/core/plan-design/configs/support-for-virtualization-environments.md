---
title: Unterstützung für Virtualisierung
titleSuffix: Configuration Manager
description: Die Anforderungen für die Installation der Configuration Manager-Client- und Standortsystemrollen in einer Virtualisierungsumgebung.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f7d774d620916f3d735a3545db5fe1e41988731d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126680"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Unterstützung für Virtualisierungsumgebungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt die Installation von Client- und Standortsystemrollen auf unterstützten Betriebssystemen, die als virtueller Computer (VM) in bestimmten Virtualisierungsumgebungen ausgeführt werden. Dies gilt auch, wenn der virtuelle Host (Virtualisierungsumgebung) nicht als Client- oder Standortserver unterstützt wird.

Verwenden Sie z. B. Microsoft Hyper-V Server 2016, um eine VM zu hosten, auf der Windows Server 2019 ausgeführt wird. Sie können die Client- oder Standortsystemrollen auf der VM unter Windows Server 2019 installieren. Der Client kann nicht auf dem Host installiert werden, auf dem Microsoft Hyper-V Server 2016 ausgeführt wird.

## <a name="virtualization-environments"></a>Unterstützte Virtualisierungsumgebungen

- Windows Server 2019  
- Windows Server 2016 <sup>[Hinweis 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Hinweis 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager unterstützt keine [geschachtelte Virtualisierung](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), die in Windows Server 2016 neu eingeführt wurde.

### <a name="virtualization-environment-support"></a>Unterstützung von Virtualisierungsumgebungen

Für jeden virtuellen Computer gelten die gleichen oder höhere Anforderungen für Hardware und Software wie für einen physischen Configuration Manager-Computer.

Verwenden Sie das Programm zur Validierung der Servervirtualisierung, um zu überprüfen, ob Configuration Manager Ihre Virtualisierungsumgebung unterstützt. Das Programm umfasst einen Online-Assistenten für Richtlinien zur Unterstützung von Virtualisierungsprogrammen. Weitere Informationen finden Sie unter [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programm zur Validierung der Servervirtualisierung).

Mit Configuration Manager ist die Verwaltung von VMs nicht möglich, wenn diese offline sind. Der Configuration Manager-Client auf dem Hostcomputer kann ein Offline-VM-Image nicht verwalten. Beispielsweise können keine Softwareupdates installiert oder Hardwareinventur erfasst werden.

Im Allgemeinen werden VMs vom Configuration Manager nicht besonders berücksichtigt. Wenn Sie z. B. eine VM anhalten und ihren Status nicht speichern, wird Configuration Manager möglicherweise nicht feststellen, ob ein Softwareupdate erneut installiert werden muss.

Zur Unterstützung der Configuration Manager-Clientleistung in virtuellen Umgebungen, die mehrere Benutzersitzungen unterstützen, wird die Benutzerrichtlinie standardmäßig deaktiviert. Ab Version 1910 können Sie die Benutzerrichtlinie in diesem Szenario aktivieren. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen in Configuration Manager – Aktivieren der Benutzerrichtlinie für mehrere Benutzersitzungen](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Microsoft Azure-VMs

Configuration Manager kann auf VMs in Azure genau wie auf lokalen Computern innerhalb Ihres Rechenzentrums ausgeführt werden. Verwenden Sie Configuration Manager mit Azure-VMs in den folgenden Szenarios:

- **Szenario 1**: Ausführen von Configuration Manager auf einer Azure-VM. Verwenden Sie ihn, um Clients auf anderen Azure-VMs zu verwalten.

- **Szenario 2**: Ausführen von Configuration Manager auf einer Azure-VM. Verwenden Sie ihn zum Verwalten von Clients, die nicht in Azure ausgeführt werden.

- **Szenario 3**: Ausführen verschiedener Configuration Manager-Standortsystemrollen auf Azure-VMs. Führen Sie andere Rollen in Ihrem lokalen Rechenzentrum aus, das ordnungsgemäß mit Azure verbunden ist.

Die gleichen Configuration Manager-Anforderungen für Netzwerke, unterstützte Konfigurationen und Hardwareanforderungen gelten auch für Azure-VMs.

Weitere Informationen finden Sie unter [Configuration Manager in Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]
> Für Configuration Manager-Standorte und -Clients, die auf Azure-VMs ausgeführt werden, gelten die gleichen Lizenzanforderungen wie für lokale Installationen.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) ist ein Desktop- und App-Virtualisierungsdienst, der auf Microsoft Azure ausgeführt wird. Verwenden Sie ab Version 1906 Configuration Manager zum Verwalten dieser unter Windows ausgeführten virtuellen Geräte in Azure. Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur (Virtual Desktop Infrastructure, VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)