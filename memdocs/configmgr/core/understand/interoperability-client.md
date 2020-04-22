---
title: Client für erweiterte Interoperabilität
titleSuffix: Configuration Manager
description: Erfahren Sie alles über die Verwendung des Clients für erweiterte Interoperabilität für die langfristige Unterstützung eines statischen Configuration Manager-Clients mit einer Current Branch-Website.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706978"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Verwenden der Configuration Manager-Clientsoftware für erweiterte Interoperabilität mit den zukünftigen Versionen eines Current Branch-Standorts

*Gilt für: Configuration Manager (Current Branch)*  

Unternehmensrichtlinien erlauben Ihnen möglicherweise nicht, den Configuration Manager-Client auf einigen Geräten regelmäßig zu aktualisieren. So müssen Sie beispielsweise Change Management-Richtlinien einhalten, oder das Gerät ist unternehmenskritisch. Passen Sie diese Bedürfnisse an, indem Sie einen neuen Client für den langfristigen Gebrauch installieren, also den Client für erweiterte Interoperabilität (Extended Interoperability Client, EIC). Verwenden Sie den EIC ausschließlich für bestimmte Geräte, die nicht häufig aktualisiert werden können, wie Kiosk- oder POS-Geräte. Verwenden Sie dieses [automatische Clientupgrade](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) für die meisten Ihrer Clients.

## <a name="how-it-works"></a>Funktionsweise

Beim Installieren eines neuen [konsoleninternen Updates](../servers/manage/install-in-console-updates.md) für Configuration Manager aktualisieren die Clients ihre Clientsoftware typischerweise automatisch, um die neuen Funktionen verwenden zu können. In diesem Szenario aktualisieren Sie noch immer auf Current Branch und erhalten die neuen Features und Updates. Die meisten Geräte aktualisieren die Configuration Manager-Clientsoftware mit jedem Versionsupdate, das Sie installieren. Wenn Sie jedoch für bestimmte kritische Systeme keine Clientsoftwareupdates erhalten möchten, können Sie den erweiterten Interoperabilitätsclient installieren. Diese Clients werden erst dann neue Clientsoftware installieren, wenn Sie ihnen ausdrücklich eine neue Clientsoftwareversion bereitstellen.

## <a name="supported-versions"></a>Unterstützte Versionen

In der folgenden Tabelle sind die Versionen des Configuration Manager-Clients aufgeführt, die für dieses Szenario unterstützt werden:

| Version | Verfügbarkeitsdatum | Supportenddatum |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27. März 2019 | Nicht früher als 27. März 2021 |
| 1802<br/>5.00.8634 | 1\. May 2018 | Nicht früher als 1. Mai 2020 |
| 1606<br/>5.00.8412 | 18. November 2016 | 1\.Mai 2019 |

> [!TIP]  
> Der EIC wird für mindestens zwei Jahre ab dem Releasedatum unterstützt. Weitere Informationen zu Releasedaten finden Sie unter [Support for Configuration Manager current branch versions (Unterstützung für Versionen des aktuellen Branch von Configuration Manager)](../servers/manage/current-branch-versions-supported.md).  

Denken Sie daran, den erweiterten Interoperabilitätsclient auf den mit Current Branch verwalteten Geräten zu aktualisieren, bevor der Client nicht mehr unterstützt wird. Hierfür laden Sie eine neue Clientversion von Microsoft herunter und stellen die aktualisierte Clientsoftware auf Ihren Geräten bereit, die den aktuellen erweiterten Interoperabilitätsclient verwenden.

## <a name="how-to-use-the-eic"></a>Verwenden des EIC

1. Fügen Sie diese Geräte einer Sammlung hinzu, und schließen Sie diese Sammlung von automatischen Clientupgrades aus. Weitere Informationen finden Sie unter [Ausschließen von Clientupgrades für Windows-Computer in System Center Configuration Manager](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Fordern Sie eine unterstützte Version des EIC aus dem Ordner `\SMSSETUP\Client` des Updateinstallationsmediums von Configuration Manager an. Stellen Sie sicher, dass Sie den gesamten Inhalt des Ordners kopieren.  

    > [!TIP]  
    > Wenn Sie Configuration Manager-Medien im [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) suchen möchten, wechseln Sie zur Registerkarte **Downloads and Keys** (Downloads und Schlüssel), und suchen Sie nach `System Center Config`. Wählen Sie anschließend **System Center Config Mgr (Current Branch)** aus.

1. Installieren Sie den EIC manuell auf diesen Geräten. Weitere Informationen finden Sie unter [ Manuelles Installieren von Clients](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).  

    > [!Important]  
    > Wenn Sie ein Upgrade von Clients der Version 1606 auf Version 1802 durchführen, verwenden Sie die CCMSETUP-Option **/AlwaysExcludeUpgrade:True**. Andernfalls erhält der Client möglicherweise eine Richtlinie vom Verwaltungspunkt, um ein automatisches Upgrade vor der Ausschlussrichtlinie durchzuführen.  

## <a name="limitations"></a>Einschränkungen

- Updates für die Software des erweiterten Interoperabilitätsclients sind nicht per konsoleninternem Update verfügbar. Weitere Informationen zum Aktualisieren von EIC-Clients finden Sie unter [Aktualisieren eines ausgeschlossenen Clients](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- Der EIC unterstützt nur die folgenden Features:  

  - Softwareupdates  
  - Hardware- und Softwareinventur
  - Pakete und Programme

## <a name="next-steps"></a>Nächste Schritte

[Ausschließen von Clientupgrades für Windows-Computer in System Center Configuration Manager](../clients/manage/upgrade/exclude-clients-windows.md)

Verwenden Sie die Informationen in [How to monitor clients](../clients/manage/monitor-clients.md) (Überwachen von Clients), um sicherzustellen, dass die Clients auf den gewünschten Geräten ordnungsgemäß installiert werden.
