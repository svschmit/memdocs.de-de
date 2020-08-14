---
title: Vorabbereitstellung von BitLocker in Windows PE
titleSuffix: Configuration Manager
description: Der Task „BitLocker vorab bereitstellen“ in Configuration Manager aktiviert BitLocker aus Windows Preinstallation Environment vor der Bereitstellung des Betriebssystems.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124942"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Vorabbereitstellung von BitLocker in Windows PE mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe des Tasksequenzschritts **BitLocker vorab bereitstellen** in Configuration Manager können Sie vor Bereitstellung des Betriebssystems BitLocker aus Windows PE (Windows Preinstallation Environment) aktivieren. Es wird nur der auf dem Laufwerk verwendete Speicherplatz verschlüsselt, sodass die Verschlüsselungszeit erheblich verkürzt wird. Hierzu wird eine zufällig erzeugte unverschlüsselte Schutzkomponente auf das formatierte Volume angewendet und dieses vor der Ausführung des Windows-Setupvorgangs verschlüsselt. Die Möglichkeit der Vorabbereitstellung von BitLocker wurde mit Windows 8 und Windows Server 2012 eingeführt. Sie können BitLocker allerdings auf einer Festplatte vorab bereitstellen und Windows 7 nachfolgend installieren, solange Sie die folgenden besonderen Schritte beachten. Nach dem Abschluss des Windows 7-Setups müssen Sie eine BitLocker-Schlüsselschutzkomponente festlegen, da BitLocker mit unverschlüsselter Schutzkomponente von der Windows 7-BitLocker-Systemsteuerung nicht unterstützt wird. Sie müssen mithilfe des Schritts **BitLocker aktivieren** oder des Befehlszeilenprogramms „manage-bde.exe“ eine Schlüsselschutzkomponente hinzufügen.  

 Allgemein beschrieben müssen Sie folgende Schritte ausführen, um BitLocker auf einem Computer, auf dem Windows 7 installiert werden soll, erfolgreich vorab bereitzustellen:  

- Neustart des Computers in Windows PE ausführen  

  > [!IMPORTANT]  
  >  Sie müssen ein Startabbild mit Windows PE 4 oder höher zur Vorabbereitstellung von BitLocker verwenden. Weitere Informationen zu in Configuration Manager unterstützten Windows PE-Versionen finden Sie unter [Externe Abhängigkeiten von Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Festplatte partitionieren und formatieren  

- BitLocker vorab bereitstellen  

- Windows 7 mit den betreffenden Betriebssystem- und Netzwerkeinstellungen installieren  

- Schlüsselschutzkomponente zu BitLocker hinzufügen  

  In Configuration Manager besteht die empfohlene Vorgehensweise zur Vorabbereitstellung von BitLocker auf einer Festplatte und der nachfolgenden Installation von Windows 7 darin, eine neue Tasksequenz zu erstellen und **Bestehendes Imagepaket auf einer virtuellen Festplatte installieren** auf der Seite **Neue Tasksequenz erstellen** des **Assistenten zum Erstellen von Tasksequenzen** auszuwählen. Die in der folgenden Tabelle aufgeführten Tasksequenzschritte werden dann vom Assistenten erstellt.  

> [!NOTE]  
>  Abhängig von der Konfiguration der Einstellungen im Assistenten kann die Tasksequenz zusätzliche Schritte aufweisen. So kann beispielsweise der Schritt **Windows-Einstellungen erfassen** vorhanden sein, wenn Sie **Microsoft Windows-Einstellungen erfassen** auf der Seite **Zustandsmigration** des Assistenten ausgewählt haben.  

|Tasksequenzschritt|Details|  
|------------------------|-------------|  
|BitLocker deaktivieren|Mit diesem Schritt wird die BitLocker-Verschlüsselung erforderlichenfalls deaktiviert. Weitere Informationen finden Sie unter [BitLocker deaktivieren](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Neustart des Computers in Windows PE|Bei diesem Schritt wird der Computer in Windows PE neu gestartet, indem das der Tasksequenz zugewiesene Startabbild ausgeführt wird. Sie müssen ein Startabbild mit Windows PE 4 oder höher zur Vorabbereitstellung von BitLocker verwenden. Weitere Informationen finden Sie unter [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Festplatte 0 partitionieren – BIOS<br /><br /> Festplatte 0 partitionieren – UEFI|Mit diesen Schritten wird das angegebene Laufwerk auf dem Zielcomputer unter Verwendung von BIOS oder UEFI formatiert und partitioniert. UEFI wird von der Tasksequenz verwendet, wenn erkannt wird, dass sich der Zielcomputer im UEFI-Modus befindet. Weitere Informationen finden Sie unter [Datenträger formatieren und partitionieren](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|BitLocker vorab bereitstellen|Bei diesem Schritt wird BitLocker auf einem Laufwerk in Windows PE aktiviert. Es wird nur der auf dem Laufwerk verwendete Speicherplatz verschlüsselt. Da die Festplatte im vorherigen Schritt partitioniert und formatiert wurde, sind keine Daten vorhanden, und die Verschlüsselung wird sehr schnell abgeschlossen. Weitere Informationen finden Sie unter [BitLocker vorab bereitstellen](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Betriebssystem anwenden|In diesem Schritt wird die Antwortdatei vorbereitet, mit deren Hilfe das Betriebssystem auf dem Zielcomputer installiert wird. Außerdem wird die Tasksequenzvariable OSDTargetSystemDrive auf den Laufwerksbuchstaben der Partition festgelegt, auf der die Betriebssystemdateien enthalten sind. Antwortdatei und Variable werden im Schritt „Windows und ConfigMgr einrichten“ zur Installation des Betriebssystems verwendet. Weitere Informationen finden Sie unter [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Windows-Einstellungen anwenden|In diesem Schritt werden die Windows-Einstellungen der Antwortdatei hinzugefügt. Die Antwortdatei wird im Schritt „Windows und ConfigMgr einrichten“ zur Installation des Betriebssystems verwendet. Weitere Informationen finden Sie unter [Windows-Einstellungen anwenden](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Netzwerkeinstellungen anwenden|In diesem Schritt werden die Netzwerkeinstellungen der Antwortdatei hinzugefügt. Die Antwortdatei wird im Schritt „Windows und ConfigMgr einrichten“ zur Installation des Betriebssystems verwendet. Weitere Informationen finden Sie unter [Schritt „Netzwerkeinstellungen anwenden“](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Gerätetreiber anwenden|In diesem Schritt werden die geeigneten Treiber identifiziert und als Teil der Betriebssystembereitstellung installiert. Weitere Informationen finden Sie unter [Treiber automatisch anwenden](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Windows und ConfigMgr einrichten|In diesem Schritt wird der Übergang von Windows PE zum neuen Betriebssystem ausgeführt. Dieser Tasksequenzschritt muss bei jeder Betriebssystembereitstellung ausgeführt werden. Mit diesem Schritt wird der Configuration Manager-Client im neuen Betriebssystem installiert und die weitere Ausführung der Tasksequenz im neuen Betriebssystem ermöglicht. Weitere Informationen finden Sie unter [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Aktivieren von BitLocker|Bei diesem Schritt wird die BitLocker-Verschlüsselung auf der Festplatte aktiviert, und die Schlüsselschutzkomponenten werden festgelegt. Da die Festplatte zuvor mit BitLocker vorab bereitgestellt wurde, ist dieser Schritt sehr schnell abgeschlossen. Windows 7 erfordert das Hinzufügen einer Schlüsselschutzkomponente. Wenn Sie diesen Schritt nicht verwenden, können Sie das Befehlszeilenprogramm „manage-bde.exe“ ausführen, um eine Schlüsselschutzkomponente festzulegen. Weitere Informationen finden Sie unter [BitLocker aktivieren](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
