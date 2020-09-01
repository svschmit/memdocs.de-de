---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: ff48e8117437e45be42551ebffff7cdcf5bce184
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820295"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
Die folgenden Profile werden für Geräte unterstützt,die Sie mit Configuration Manager, Current Branch 2006 oder höher, verwalten. Verwendet wird das Szenario der Mandantenanfügung:
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- Plattform: **Windows 10 und Windows Server**

  - Profil: **Microsoft Defender Antivirus-Richtlinie (Configuration Manager)**
  
    Verwalten Sie die [Antivirus-Richtlinien für Configuration Manager-Geräte](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md), wenn Sie die Mandantenanfügung verwenden.

    Dieses Profil wird auf Geräten unterstützt, die mandantenbasiert angefügt wurden und die folgenden Plattformen ausführen:
    - Windows 10 und höher (x86, x64, ARM64)
    - Windows 8.1 (x84, x64)
    - Windows Server 2019 und höher (x64)
    - Windows Server 2016 (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)
