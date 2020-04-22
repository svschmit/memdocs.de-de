---
title: Hardwareinventur für Linux und UNIX
titleSuffix: Configuration Manager
description: Informieren Sie sich, wie die Hardwareinventur für Linux und UNIX in Configuration Manager verwendet wird.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1bdfb8c6d528c12581f05f86111a1a76d2259faa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695428"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Hardwareinventur für Linux- und UNIX in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr. 
> 
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Der Configuration Manager-Client für Linux und UNIX unterstützt die Hardwareinventur. Nach dem Erfassen der Hardwareinventur können Sie den Bestand im Ressourcen-Explorer oder in Configuration Manager-Berichten anzeigen und diese Informationen dazu verwenden, um Abfragen und Sammlungen zu erstellen, die die folgenden Vorgänge ermöglichen:  

- Softwarebereitstellung  

- Erzwingen von Wartungsfenstern  

- Bereitstellen benutzerdefinierter Clienteinstellungen  

Bei der Hardwareinventur für Linux- und UNIX-Server wird ein standardbasierter CIM-Server (Common Information Model) verwendet. Der CIM-Server wird als Softwaredienst (oder Daemon) ausgeführt und stellt eine Verwaltungsinfrastruktur bereit, die auf DMTF-Standards (Distributed Management Task Force) basiert. Der CIM-Server bietet ähnliche Funktionen wie die CIM-Funktionen der Windows-Verwaltungsinfrastruktur (Windows Management Infrastructure, WMI), die auf Windows-basierten Computern verfügbar sind.  

Ab dem kumulativen Update 1 verwendet der Client für Linux und UNIX die Open Source-Version von **omiserver**, Version 1.0.6, der **Open Group**. (Vor dem kumulativen Update 1 hat der Client **nanowbem** als CIM-Server verwendet).  

Der CIM-Server wird im Rahmen des Clients für Linux und UNIX installiert. Der Client für Linux und UNIX kommuniziert direkt mit dem CIM-Server und verwendet nicht die WS-MAN-Schnittstelle des CIM-Servers. Der WS-MAN-Port auf dem CIM-Server ist deaktiviert, wenn der Client installiert wird. Microsoft hat den CIM-Server entwickelt, der jetzt über das OMI-Projekt (Open Management Infrastructure) als Open Source verfügbar ist. Weitere Informationen zum Open Management Infrastructure-Projekt finden Sie auf der [The Open Group](https://www.opengroup.org/) -Website.  

Die Hardwareinventur auf Linux- und UNIX-Servern erfolgt durch die Zuordnung von vorhandenen Win32-WMI-Klassen und -Eigenschaften zu entsprechenden Klassen und Eigenschaften für Linux- und UNIX-Server. Diese 1:1-Zuordnung von Klassen und Eigenschaften ermöglicht das Integrieren der Hardwareinventur für Linux und UNIX in Configuration Manager. Es werden Inventurdaten von Linux- und UNIX-Servern zusammen mit dem Bestand von Windows-basierten Computern in der Configuration Manager-Konsole und in Berichten angezeigt. Durch dieses Verhalten wird eine konsistente heterogene Verwaltung ermöglicht.  

> [!TIP]  
>  Mit dem **Beschriftung** -Wert für die **Betriebssystem** -Klasse können Sie verschiedene Linux- und UNIX-Betriebssysteme in Abfragen und Sammlungen identifizieren.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Konfigurieren der Hardwareinventur für Linux- und UNIX-Server  
 Sie können die standardmäßigen Clienteinstellungen verwenden oder benutzerdefinierte Clienteinstellungen erstellen, um die Hardwareinventur zu konfigurieren. Wenn Sie benutzerdefinierte Clientgeräteeinstellungen verwenden, können Sie die Klassen und Eigenschaften konfigurieren, die Sie nur von Ihren Linux- und UNIX-Servern erfassen möchten. Sie können auch benutzerdefinierte Zeitpläne für die Erfassung von vollständigen und Deltainventuren von Ihren Linux- und UNIX-Servern verwenden.  

 Der Client für Linux und UNIX unterstützt die folgenden Hardwareinventurklassen, die auf Linux- und UNIX-Servern verfügbar sind:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Nicht alle Eigenschaften für diese Inventurklassen sind für Linux- und UNIX-Computer in Configuration Manager aktiviert.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Vorgänge für die Hardwareinventur  
 Nachdem Sie die Hardwareinventur von den Linux- und UNIX-Servern erfasst haben, können Sie diese Informationen auf dieselbe Weise wie den Bestand anzeigen, den Sie von anderen Computern erfassen:  

- Verwenden des Ressourcen-Explorers zum Anzeigen von detaillierten Hardwareinventurinformationen von Linux- und UNIX-Servern  

- Erstellen von Abfragen auf Basis von bestimmten Hardwarekonfigurationen  

- Erstellen von abfragebasierten Sammlungen, die auf bestimmten Hardwarekonfigurationen basieren  

- Ausführen von Berichten, die bestimmte Details zu Hardwarekonfigurationen anzeigen  

Die Hardwareinventur auf einem Linux- oder UNIX-Server wird gemäß dem Zeitplan ausgeführt, den Sie in den Clienteinstellungen konfigurieren. Dieser Zeitplan umfasst standardmäßig jeweils sieben Tage. Der Client für Linux und UNIX unterstützt sowohl vollständige Inventurzyklen als auch Deltainventurzyklen.  

Sie können den Client auf einem Linux- oder UNIX-Server auch zwingen, die Hardwareinventur unmittelbar durchzuführen. Verwenden Sie zum Ausführen der Hardwareinventur auf einem Client die **Stamm**anmeldeinformationen, um den folgenden Befehl zum Starten eines Hardwareinventurzyklus auszuführen: `/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

Aktionen für die Hardwareinventur werden in die Clientprotokolldatei **scxcm.log**eingegebenen.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Gewusst wie: Verwenden der Open Management Infrastructure zum Erstellen einer benutzerdefinierten Hardwareinventur  
 Der Client für Linux und UNIX unterstützt die benutzerdefinierte Hardwareinventur, die Sie mithilfe der Open Management Infrastructure (OMI) erstellen können. Führen Sie dazu die folgenden Schritte aus:  

1.  Erstellen eines benutzerdefinierten Inventuranbieters mithilfe der OMI-Quelle  

2.  Konfigurieren von Computern für die Verwendung des neuen Anbieters zum Melden des Bestands  

3.  Aktivieren von Configuration Manager zur Unterstützung des neuen Anbieters  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Erstellen Sie einen benutzerdefinierten Hardwareinventuranbieter für Linux- und UNIX-Computer:  
 Verwenden Sie **OMI Source – v.1.0.6**, und befolgen Sie die Anweisungen im Handbuch für die ersten Schritte mit OMI, um einen benutzerdefinierten Hardwareinventuranbieter für den Configuration Manager-Client für Linux und UNIX zu erstellen. Dieser Prozess umfasst das Erstellen einer MOF-Datei (Managed Object Format), die das Schema für den neuen Anbieter definiert. Später importieren Sie die MOF-Datei in Configuration Manager, um die Unterstützung der neuen benutzerdefinierten Inventurklasse zu aktivieren.  

 Sowohl „OMI Source – v.1.0.6“ als auch das Handbuch für die ersten Schritte mit OMI können auf der [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) -Website heruntergeladen werden. Sie finden diese Downloads auf der Registerkarte für **Dokumente** der folgenden Webseite der Website „OpenGroup.org“: [Open Management Infrastructure (OMI)](https://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Konfigurieren Sie jeden Computer, der Linux oder UNIX ausführt, mit dem benutzerdefinierten Hardwareinventuranbieter:  
 Nachdem Sie einen benutzerdefinierten Inventuranbieter erstellt haben, müssen Sie die Anbieterbibliotheksdatei auf jeden Computer kopieren und dann registrieren, der über zu erfassendes Inventar verfügt.  

1.  Kopieren Sie die Anbieterbibliothek auf jeden Linux- und UNIX-Computer, von dem Sie Inventar erfassen möchten. Der Name der Anbieterbibliothek ähnelt dem folgenden Namen: **XYZ_MyProvider.so**  

2.  Dann wird auf jedem Linux- und UNIX-Computer die Anbieterbibliothek mit dem OMI-Server registriert. Der OMI-Server wird auf dem Computer installiert, wenn Sie den Configuration Manager-Client für Linux und UNIX installieren, aber Sie müssen benutzerdefinierte Anbieter manuell registrieren. Verwenden Sie die folgende Befehlszeile zum Registrieren des Anbieters: `/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`.  

3.  Nachdem Sie den neuen Anbieter registriert haben, testen Sie den Anbieter mithilfe des **omicli** -Tools. Das **omicli**-Tool wird auf jeden Linux- und UNIX-Computer installiert, wenn Sie den Configuration Manager-Client für Linux und UNIX installieren. Führen Sie z. B. den folgenden Befehl auf dem Computer aus, wobei **XYZ_MyProvider** den Namen des erstellten Anbieters angibt: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Informationen zu **omicli** und zum Testen von benutzerdefinierten Anbietern finden Sie im Handbuch zu den ersten Schritten mit OMI.  

> [!TIP]  
>  Verwenden Sie die Verteilung von Software zum Bereitstellen von benutzerdefinierter Providers und benutzerdefinierte Anbieter auf jedem Linux- und UNIX-Clientcomputer zu registrieren.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Aktivieren Sie die neue Inventurklasse in Configuration Manager:  
 Bevor Configuration Manager den Bestand melden kann, der vom neuen Anbieter auf Linux- und UNIX-Computern gemeldet wird, müssen Sie die MOF-Datei (Managed Object Format) importieren, die das Schema des benutzerdefinierten Anbieters definiert.  

 Informationen zum Import einer benutzerdefinierte MOF-Datei in Configuration Manager finden Sie unter [Konfigurieren der Hardwareinventur](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
