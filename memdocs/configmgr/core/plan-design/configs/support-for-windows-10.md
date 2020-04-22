---
title: Unterstützung für Windows 10
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu Windows 10-Versionen, die bei Verwendung von Configuration Manager als Clients oder für Betriebssystembereitstellungen unterstützt werden.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7241db0220bf4adf9b55341514afb03de33c2589
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688598"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Unterstützung für Windows 10 in Configuration Manager  

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erhalten Sie Informationen zu Windows 10-Versionen, die von Configuration Manager unterstützt werden. Hierzu zählen:

- [Windows 10 als Configuration Manager-Client](#windows-10-as-a-client)
- [Windows-Assessment and Deployment Kit (ADK) für Windows 10](#windows-10-adk)

> [!Tip]
> Windows Server-Builds werden auf gleiche Weise als Client wie die zugehörige Windows 10-Version unterstützt. Windows Server 2016 entspricht beispielsweise der gleichen Buildversion wie Windows 10 LTSB 2016, und Windows Server-Version 1803 entspricht der gleichen Buildversion wie Windows 10-Version 1803.
>
> Weitere Informationen zu Windows Server als Standortsystem finden Sie unter [Unterstützte Betriebssysteme für Configuration Manager-Standortsystemserver](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>Windows 10 als Client

Configuration Manager versucht, neue Windows 10-Versionen nach der Veröffentlichung möglichst schnell als Client zu unterstützen. Da die Produkte über getrennte Zeitpläne für Entwicklung und Freigabe verfügen, hängt die Unterstützung von Configuration Manager davon ab, wann sie jeweils verfügbar sind.

Eine Version von Configuration Manager, deren [Support für diese Version](../../servers/manage/current-branch-versions-supported.md) eingestellt wurde, wird aus der Kompatibilitätsmatrix gelöscht. Ebenso wird der Support für Windows 10-Versionen wie Enterprise 2015 LTSB oder 1511 aus der Kompatibilitätsmatrix entfernt, sobald diese nicht mehr unterstützt werden.

- Die neueste Version von Configuration Manager (Current Branch) empfängt sowohl Sicherheits- als auch wichtige Updates, die Korrekturen für Probleme mit Windows 10-Versionen enthalten können. Wenn Microsoft eine neue Version von Configuration Manager (Current Branch) veröffentlicht, erhalten frühere Versionen nur Sicherheitsupdates. Weitere Informationen finden Sie unter [Support für die Versionen des aktuellen Branches von System Center Configuration Manager](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > Die beste Möglichkeit, um Windows 10 immer auf dem neuesten Stand zu halten, besteht darin Configuration Manager immer auf den neuesten Stand zu bringen. Weitere Informationen finden Sie unter [Configuration Manager und Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md).  

- Diese Informationen ergänzen die [unterstützten Betriebssysteme für Clients und Geräte](supported-operating-systems-for-clients-and-devices.md).  

- Wenn Sie Long-Term Servicing Branch von Configuration Manager verwenden, finden Sie weitere Informationen unter [Unterstützte Konfigurationen für Long-Term Servicing Branch](../../understand/supported-configurations-for-ltsb.md).  

In der folgenden Tabelle werden die Versionen von Windows 10 aufgelistet, die Sie als Client mit verschiedenen Versionen von Configuration Manager verwenden können:

| Windows 10-Version | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Nicht unterstützt](media/Red_X.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Weitere Informationen zum Windows-Lebenszyklus finden Sie unter [Informationsblatt zum Lebenszyklus von Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

| Key |
|--|
| ![Unterstützt](media/green_check.png) = **Unterstützt**  |
| ![Nicht unterstützt](media/Red_X.png) = **Not supported** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Hinweise zur Windows 10-Clientunterstützung

- Für Windows 10-Versionen, die über den halbjährlichen Kanal bezogen werden, werden die folgenden Editionen unterstützt: Enterprise, Pro, Education und Pro Education.  

- Ab Version 1906 unterstützt Configuration Manager Windows 10 Pro for Workstation.

- Für Windows 10, Version 1909 zeigen die Medien für die Bereitstellung des Betriebssystems die Version 10.0.18362.418 an.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> Windows 10 auf ARM64

Configuration Manager unterstützt den Client auf ARM64-Geräten mit Windows 10. Die Bereitstellung des Betriebssystems wird nicht unterstützt.<!-- 1353704 -->

Ab Version 2002 gilt Folgendes:<!--5954175--> Die Plattformversion **Alle Windows 10 (ARM64)** ist in der Liste unterstützter Betriebssystemversionen für Objekte mit Anforderungsregeln oder Anwendbarkeitslisten verfügbar.

> [!NOTE]
> Bisher wurde diese Aktion bei Auswahl der obersten **Windows 10**-Plattformebene automatisch sowohl für **Alle Windows 10 (64-Bit)** als auch für **Alle Windows 10 (32-Bit)** ausgewählt. Diese neue Plattform wird nicht automatisch ausgewählt. Wenn Sie **Alle Windows 10 (ARM64)** hinzufügen möchten, wählen Sie die Plattform manuell in der Liste aus.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> Unterstützung für Windows Insider

Ab Configuration Manager, Version 1906, können Sie Builds für das [Windows-Insider-Programm](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) aktualisieren und verwalten. Wir bieten unseren Kunden diese Funktion als zusätzliche Leistung an. Der Support funktioniert allerdings nach dem Best-Effort-Prinzip. Configuration Manager gibt möglicherweise keinen Hotfix für diese Funktion aus, wenn die Funktionalität nicht mehr gegeben ist.  

Feedback zu Windows-Insider können Sie gerne über den [Feedback-Hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback) übermitteln.

## <a name="windows-10-adk"></a>Windows 10 ADK

Beim Bereitstellen von Betriebssystemen mit Configuration Manager ist das Windows ADK eine erforderliche externe Abhängigkeit. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Windows ADK für Windows 10 herunterladen](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Ab Version 1809 von Windows 10 ist der Installer für Windows PE separat. Es wurden keine anderweitigen Änderungen an der Funktionsweise vorgenommen.
    >
    > Stellen Sie sicher, dass Sie sowohl das **Windows ADK für Windows 10** als auch das **Windows PE-Add-On für das ADK** herunterladen.

Die folgende Tabelle listet die Versionen des Windows 10 ADK auf, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können.

| Windows 10 ADK-Version  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Nicht unterstützt](media/Red_X.png)   | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Abwärtskompatibel](media/blue_compat.png) | ![Abwärtskompatibel](media/blue_compat.png) | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Abwärtskompatibel](media/blue_compat.png) | ![Abwärtskompatibel](media/blue_compat.png) | ![Nicht unterstützt](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Nicht unterstützt](media/Red_X.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |

|Key|
|--|
| ![Unterstützt](media/green_check.png) = **Unterstützt** <br/> In dieser Tabelle wird nur dargestellt, welche Versionen von Configuration Manager welche Versionen des Windows ADK unterstützen. Microsoft empfiehlt die Verwendung des Windows ADK, das der Windows-Version entspricht, die Sie bereitstellen. Verwenden Sie die neueste Windows ADK-Version, wenn Sie die neueste Version von Windows 10 bereitstellen. Die neueste Windows ADK-Version unterstützt möglicherweise die Bereitstellung von älteren Betriebssystemversionen, z. B. Windows 8.1.<!-- SCCMDocs issue 1229 --> Weitere Informationen zur Unterstützung für die Windows ADK-Komponente finden Sie unter [Unterstützte DISM-Plattformen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) und [USMT-Anforderungen](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Abwärtskompatibel](media/blue_compat.png)  = **Backward compatible** <br/> Diese Kombination wurde nicht getestet, sollte jedoch funktionieren. Alle bekannten Probleme und Einschränkungen werden dokumentiert. |
| ![Nicht unterstützt](media/Red_X.png) = **Not supported** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Hinweise zur Unterstützung von Windows 10 ADK

- Configuration Manager unterstützt nur x86- und AMD64-Komponenten des Windows 10 ADK. ARM- oder ARM64-Komponenten werden derzeit nicht unterstützt.

- Für Windows Server-Builds gilt die gleiche Windows ADK-Anforderung wie für die zugehörige Windows 10-Version. Windows Server 2016 weist beispielsweise die gleiche Buildversion wie Windows 10 LTSB 2016 auf.
