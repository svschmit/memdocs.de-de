---
title: Unterstützung für Virtualisierung
titleSuffix: Configuration Manager
description: Die Anforderungen für die Installation der Configuration Manager-Client- und Standortsystemrollen in einer Virtualisierungsumgebung.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688548"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Unterstützung für Virtualisierungsumgebungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt die Installation von Client- und Standortsystemrollen auf unterstützten Betriebssystemen, die als virtueller Computer in den in diesem Artikel beschriebenen Virtualisierungsumgebungen ausgeführt werden. Dies gilt auch, wenn der Host für virtuelle Computer (Virtualisierungsumgebung) nicht als Client- oder Standortserver unterstützt wird.  

Verwenden Sie z.B. Microsoft Hyper-V Server 2012, um einen virtuellen Computer zu hosten, auf dem Windows Server 2012 ausgeführt wird. Sie können die Client- oder Standortsystemrollen auf dem virtuellen Computer unter Windows Server 2012 installieren. Der Client kann nicht auf dem Host installiert werden, auf dem Microsoft Hyper-V Server 2012 ausgeführt wird.  

## <a name="virtualization-environments"></a>Unterstützte Virtualisierungsumgebungen

- Windows Server 2019  
- Windows Server 2016 <sup>[Hinweis 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Hinweis 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a> Hinweis 1: Geschachtelte Virtualisierung

Configuration Manager unterstützt keine [geschachtelte Virtualisierung](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), die in Windows Server 2016 neu eingeführt wurde.

### <a name="virtualization-environment-support"></a>Unterstützung von Virtualisierungsumgebungen

Für jeden virtuellen Computer gelten die gleichen oder höhere Anforderungen für Hardware und Software wie für einen physischen Configuration Manager-Computer.  

Verwenden Sie das Programm zur Validierung der Servervirtualisierung, um zu überprüfen, ob Ihre Virtualisierungsumgebung für Configuration Manager unterstützt wird. Das Programm umfasst einen Online-Assistenten für Richtlinien zur Unterstützung von Virtualisierungsprogrammen. Weitere Informationen finden Sie unter [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programm zur Validierung der Servervirtualisierung).  

> [!NOTE]  
> Configuration Manager unterstützt keine auf Mac-Computern ausgeführten Virtual PC- oder Virtual Server-Gastbetriebssysteme.  

Mit Configuration Manager ist die Verwaltung virtueller Computer nicht möglich, wenn diese offline sind. Ein virtueller Computer im Offlinemodus kann weder aktualisiert noch können Inventurdaten mithilfe des Configuration Manager-Clients auf dem Hostcomputer gesammelt werden.  

Für virtuelle Computer werden keine speziellen Vorkehrungen getroffen. Beispielsweise erkennt Configuration Manager möglicherweise nicht, ob auf das Image eines virtuellen Computers, auf den ein Update angewendet wurde, das Update erneut angewendet werden muss, wenn der virtuelle Computer ohne vorheriges Speichern seines Status heruntergefahren und neu gestartet wird.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Virtuelle Microsoft Azure-Computer  

Configuration Manager kann auf virtuellen Microsoft Azure-Computern genau wie auf lokalen Computern innerhalb Ihres Rechenzentrums ausgeführt werden. Verwenden Sie Configuration Manager mit virtuellen Microsoft Azure-Computern in den folgenden Szenarios:  

- **Szenario 1**: Führen Sie Configuration Manager auf einem virtuellen Azure-Computer aus. Verwenden Sie ihn zum Verwalten von Clients auf anderen virtuellen Azure-Computern.  

- **Szenario 2**: Führen Sie Configuration Manager auf einem virtuellen Azure-Computer aus. Verwenden Sie ihn zum Verwalten von Clients, die nicht in Azure ausgeführt werden.  

- **Szenario 3**: Führen Sie verschiedene Configuration Manager-Standortsystemrollen auf virtuellen Azure-Computern aus. Führen Sie andere Rollen in Ihrem lokalen Rechenzentrum aus, das ordnungsgemäß mit Azure verbunden ist.  

Für die Installation auf virtuellen Azure-Computern gelten die gleichen Configuration Manager-Anforderungen für Netzwerke, unterstützte Konfigurationen und Hardwareanforderungen wie für die lokale Installation.  

Weitere Informationen finden Sie unter [Configuration Manager in Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]  
> Für Configuration Manager-Standorte und -Clients, die auf virtuellen Azure-Computern ausgeführt werden, gelten die gleichen Lizenzanforderungen wie für lokale Installationen.  

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) ist eine Previewfunktion von Microsoft Azure und Microsoft 365. Verwenden Sie ab Version 1906 Configuration Manager zum Verwalten dieser unter Windows ausgeführten virtuellen Geräte in Azure. Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte](supported-operating-systems-for-clients-and-devices.md).
