---
title: Upgrade auf Windows 10
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Verwenden von Configuration Manager, um ein Upgrade von Windows 7 oder höher auf Windows 10 durchzuführen.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eb7e2e5c564263c7172d70ec33bb33c0dd73409c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697822"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Aktualisieren von Windows auf die neueste Version unter Verwendung von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erhalten Sie Informationen zu den Schritten, die Sie in Configuration Manager durchführen müssen, um das Betriebssystems Ihres Computers zu upgraden. Sie können aus unterschiedlichen Bereitstellungsmethoden auswählen, z. B. eigenständige Medien oder Softwarecenter. Durch das direkte Upgrade wird Folgendes durchgeführt:  

- Führt ein Upgrade des Betriebssystems auf Windows 10 oder Windows Server 2016 und höher durch

- Behält die Anwendungen, Einstellungen und Benutzerdaten auf dem Computer bei

- Weist keine externen Abhängigkeiten wie das Windows ADK auf

- Ist schneller und stabiler als herkömmliche Betriebssystembereitstellungen

> [!Note]  
> Die Tasksequenz für ein direktes Windows 10-Upgrade unterstützt jetzt die Bereitstellung auf internetbasierten Clients, die über [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) verwaltet werden. Mit dieser Funktion können Remotebenutzer einfacher ein Upgrade auf Windows 10 durchführen, ohne eine Verbindung mit dem Intranet herstellen zu müssen. Weitere Informationen finden Sie unter [Bereitstellen eines direkten Upgrades für Windows 10 über das CMG](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Unterstützte Versionen

### <a name="upgrade-version"></a>Upgradeversion

Erstellen Sie nur Betriebssystemupgradepakete, um die folgenden Betriebssystemversionen zu aktualisieren:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Ursprüngliche Version

Auf den Geräten muss eine der folgenden Betriebssystemversionen ausgeführt werden, um eine Tasksequenz für Betriebssystemupgrades zu erreichen:

#### <a name="windows-client"></a>Windows-Client

- Windows 7
- Windows 8.1
- Eine frühere Version von Windows 10 Beispielsweise können Sie Windows 10, Version 1809 auf Windows 10, Version 1903 aktualisieren.  

Weitere Informationen finden Sie unter [Windows 10-Upgradepfade](/windows/deployment/upgrade/windows-10-upgrade-paths).

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- Eine frühere Version von Windows Server 2016
- Eine frühere Version von Windows Server 2019

Weitere Informationen zu den von Windows [Server unterstützten Upgradepfaden finden Sie unter Unterstützte Upgradepfade](/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) für [WindowsServer 2016 und](https://aka.ms/upgradecenter) Windows Server Upgrade Center.


## <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

### <a name="task-sequence-requirements-and-limitations"></a>Anforderungen und Einschränkungen der Tasksequenz

Überprüfen Sie die folgenden, für die Tasksequenz zum Durchführen eines Betriebssystemupgrades geltenden Anforderungen und Einschränkungen, und stellen Sie sicher, dass die Tasksequenz Ihren Anforderungen entspricht:  

- Führen Sie nur zusätzliche Tasksequenzschritte aus, wenn diese für das Upgrade des Betriebssystems relevant sind. Zu derartigen Schritten gehört u.a. das Installieren von Paketen, Anwendung und Updates. Führen Sie außerdem Schritte durch, in denen die Befehlszeilen oder PowerShell ausgeführt oder dynamische Variablen festgelegt werden.  

- Überprüfen Sie die auf den Computern installierten Treiber und Anwendungen. Stellen Sie vor dem Bereitstellen der Upgradetasksequenz sicher, dass die Treiber mit Windows 10 kompatibel sind.  

Die folgenden Tasks sind mit einem direkten Upgrade nicht möglich. Dafür müssen Sie herkömmliche Betriebssystembereitstellungen verwenden:  

- Ändern der Domänenmitgliedschaft des Computers oder Aktualisieren der lokalen Administratorengruppe.  

- Implementieren einer grundlegenden Änderung auf Ihrem Computer. Das kann z.B. Folgendes sein:

  - Ändern der Datenträgerpartitionen
  - Ändern der Systemarchitektur von x86 in x64
  - Implementieren von UEFI. (Weitere Informationen zu einer anderen Möglichkeit finden Sie unter [Convert from BIOS to UEFI during an in-place upgrade (Wechsel von BIOS zu UEFI während eines direkten Upgrades)](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).)
  - Anpassen der Standardbetriebssystemsprache  

- Es gibt benutzerdefinierte Anforderungen, z.B. die Verwendung eines benutzerdefinierten Basisimages mit Festplattenverschlüsselung eines Drittanbieters oder das Durchführen von WinPE-Offlinevorgängen.  

### <a name="infrastructure-requirements"></a>Anforderungen an die Infrastruktur  

Die einzige Voraussetzung für ein Upgrade ist die Verfügbarkeit eines Verteilungspunkts. Verteilen Sie das Betriebssystemupgradepaket und alle anderen Pakete, die in der Tasksequenz beinhaltet sind. Weitere Informationen finden Sie unter [Installieren oder Modifizieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a> Konfigurieren  

### <a name="prepare-the-os-upgrade-package"></a>Vorbereiten des Betriebssystemupgradepakets  

Das Windows 10-Upgradepaket enthält die erforderlichen Quelldateien zum Aktualisieren des Betriebssystems auf dem Zielcomputer. Das Upgradepaket muss die gleiche Edition, Architektur und Sprache wie die Clients aufweisen, die aktualisiert werden sollen. Weitere Informationen finden Sie unter [Verwalten von Betriebssystem-Upgradepaketen](../get-started/manage-operating-system-upgrade-packages.md).  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades  

Führen Sie die im Artikel [Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades](create-a-task-sequence-to-upgrade-an-operating-system.md) beschriebenen Schritte aus, um das Upgrade des Betriebssystems zu automatisieren.  

> [!NOTE]  
> Wenn Sie eine Tasksequenz erstellen möchten, um ein Betriebssystem auf Windows 10 zu aktualisieren, sollten Sie die im Artikel [Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades](create-a-task-sequence-to-upgrade-an-operating-system.md) beschriebenen Schritte ausführen. Die Tasksequenz umfasst den Schritt **Betriebssystemupgrade durchführen** sowie weitere empfohlene Schritte und Gruppen für den End-to-End-Upgradeprozess.
>
> Sie können eine benutzerdefinierte Tasksequenz erstellen und den Schritt [Upgraden des Betriebssystems](../understand/task-sequence-steps.md#BKMK_UpgradeOS) hinzufügen. Dieser Schritt ist der einzige erforderliche Schritt für das Betriebssystemupgrade auf Windows 10. Wenn Sie sich für diese Methode entscheiden, sollten Sie nach dem Schritt **Betriebssystemupgrade durchführen** außerdem den Schritt [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer) ausführen, um das Upgrade abzuschließen. Stellen Sie sicher, dass die Einstellung **Aktuell installiertes Standardbetriebssystem** aktiviert ist, um den Computer mit dem installierten Betriebssystem und nicht mit Windows PE neu zu starten.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a> Bereitstellen  

Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

- [Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk](use-software-center-to-deploy-windows-over-the-network.md)  

- [Use stand-alone media to deploy Windows without using the network (Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks)](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > Wenn Sie eigenständige Medien verwenden, müssen Sie ein Startimage in die Tasksequenz einschließen. Mit dieser Konfiguration wird die Tasksequenz im Tasksequenzmedien-Assistenten zur Verfügung gestellt.


## <a name="monitor"></a>Überwachen  

Weitere Informationen zum Überwachen der Tasksequenzbereitstellung, um ein Betriebssystemupgrade durchzuführen, finden Sie unter [Überwachen von Betriebssystembereitstellungen](monitor-operating-system-deployments.md).