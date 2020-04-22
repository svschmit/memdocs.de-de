---
title: Upgraden von macOS-Clients
titleSuffix: Configuration Manager
description: Upgraden des Configuration Manager-Clients auf Mac-Computern
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696258"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Installieren von Clients auf Mac-Computern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Befolgen Sie die in diesem Artikel beschriebenen allgemeinen Schritte, um den Client für Mac-Computer mithilfe einer Configuration Manager-Anwendung zu aktualisieren. Alternativ können Sie auch die Clientinstallationsdatei für Mac herunterladen, in einen freigegebenen Netzwerkpfad oder einen lokalen Ordner auf dem Mac-Computer kopieren und dann die Benutzer auffordern, die Installation manuell auszuführen.  

> [!NOTE]  
> Stellen Sie vor der Ausführung dieser Schritte sicher, dass Ihr Mac-Computer alle Voraussetzungen erfüllt. Informationen hierzu finden Sie unter [Supported operating systems for clients and devices for System Center Configuration Manager (Unterstützte Betriebssysteme für Clients und Geräte für System Center Configuration Manager)](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Herunterladen der neusten Version des Mac-Clients

Der Mac-Client für Configuration Manager wird nicht auf dem Installationsmedium für Configuration Manager bereitgestellt. Laden Sie ihn aus dem Microsoft Download Center herunter, [Microsoft Endpoint Configuration Manager – macOS-Client (64-Bit)](https://www.microsoft.com/download/details.aspx?id=100850). Die Clientinstallationsdateien für Mac sind in einer Windows Installer-Datei mit dem Namen **ConfigmgrMacClient.msi** enthalten.  

## <a name="create-the-mac-client-installation-file"></a>Erstellen der Clientinstallationsdatei für Mac

Führen Sie die Datei **ConfigmgrMacClient.msi** auf einem Windows-Computer aus. Dieser Installer entpackt die Clientinstallationsdatei für Mac mit dem Namen **Macclient.dmg**. Standardmäßig ist diese Datei im folgenden Ordner enthalten: **C:\Programme\Microsoft\System Center Configuration Manager for Mac client**.  

## <a name="extract-the-client-installation-files"></a>Extrahieren der Clientinstallationsdateien

Kopieren Sie die Datei **Macclient.dmg** auf einen Mac-Computer. Integrieren Sie die Datei „MacClient.dmg“ in macOS, und kopieren Sie den Inhalt in einen Ordner auf dem Mac-Computer.  

## <a name="create-a-cmmac-file"></a>Erstellen einer CMMAC-Datei

1. Öffnen Sie den Ordner **Tools** der Clientinstallationsdateien für Mac. Erstellen Sie mithilfe des Tools **CMAppUtil** eine CMMAC-Datei aus dem Clientinstallationspaket. Mit dieser Datei können Sie die Configuration Manager-Anwendung erstellen.  

2. Kopieren Sie die neue Datei **CMClient.pkg.cmmac** an einen Netzwerkpfad, der für den Computer verfügbar ist, auf dem die Configuration Manager-Konsole ausgeführt wird.  

    Weitere Informationen finden Sie unter [Zusätzliche Verfahren zum Erstellen und Bereitstellen von Anwendungen für Macintosh-Computer](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Erstellen und Bereitstellen der App

1. Erstellen Sie in der Configuration Manager-Konsole eine [Anwendung](../../../../apps/get-started/creating-mac-computer-applications.md) aus der Datei **CMClient.pkg.cmmac**.  

2. [Stellen Sie diese Anwendung](../../../../apps/deploy-use/deploy-applications.md) für die Mac-Computer in Ihrer Hierarchie bereit.  

## <a name="install-the-updated-client"></a>Installieren des aktualisierten Clients

Der auf den Mac-Computern installierte Konfigurations-Manager-Client fordert den Benutzer zur Installation eines verfügbaren Updates auf. Nachdem die Benutzer den Client installiert haben, müssen sie ihren Macintosh-Computer neu starten.  

Nach dem Neustart des Computers wird automatisch der Assistent für die **Computeranmeldung** ausgeführt, um ein neues Benutzerzertifikat anzufordern.

Wenn Sie nicht die Configuration Manager-Registrierung verwenden, sondern das Clientzertifikat unabhängig von Configuration Manager installieren, finden Sie weitere Informationen unter [Konfigurieren des Clients für die Verwendung eines vorhandenen Zertifikats](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a> Konfigurieren von Clients für die Verwendung eines vorhandenen Zertifikats

Führen Sie das folgende Verfahren aus, um zu verhindern, dass der Assistent für die Computeranmeldung ausgeführt wird, und den aktualisierten Client für die Verwendung eines vorhandenen Clientzertifikats zu konfigurieren.  

1. Erstellen Sie in der Configuration Manager-Konsole ein [Konfigurationselement](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) vom Typ **Mac OS X**.  

1. Fügen Sie diesem Konfigurationselement eine Einstellung mit dem Einstellungstyp **Skript**hinzu.  

1. Fügen Sie der Einstellung das folgende Skript hinzu:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Fügen Sie das Konfigurationselement einer [Konfigurationsbaseline](../../../../compliance/deploy-use/create-configuration-baselines.md) hinzu. Stellen Sie anschließend die [Konfigurationsbaseline](../../../../compliance/deploy-use/deploy-configuration-baselines.md) auf allen Mac-Computern bereit, die unabhängig von Configuration Manager ein Zertifikat installieren.  
