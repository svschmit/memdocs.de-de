---
title: Erstellen eines Labs in Azure
titleSuffix: Configuration Manager
description: Automatisieren der Erstellung eines Labs für die Technical Preview von Configuration Manager oder eines Current Branch-Evaluierungs-Labs mithilfe von Azure-Vorlagen
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 23cc7d0c642637a310f53280bafed6a2a28d2834
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406689"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Erstellen eines Configuration Manager-Labs in Azure

*Gilt für: Configuration Manager (Current Branch, Technical Preview-Branch)*

<!--3556017-->

In diesem Handbuch wird beschrieben, wie in Microsoft Azure eine Configuration Manager-Laborumgebung erstellt wird. Dabei werden Azure-Vorlagen verwendet, um die Erstellung eines Labs mithilfe von Azure-Ressourcen zu vereinfachen und zu automatisieren. Es stehen zwei Azure-Vorlagen zur Verfügung: 

- Mit der Azure-Vorlage für die Technical Preview von Configuration Manager wird die aktuelle Version des Technical Preview-Branchs von Configuration Manager installiert.
- Mit der Current Branch-Vorlage für Configuration Manager in Azure wird die Auswertung der aktuellen Current Branch-Version von Configuration Manager installiert. 

Weitere Informationen finden Sie unter [Configuration Manager in Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Voraussetzungen

Für diesen Vorgang benötigen Sie ein Azure-Abonnement, mit dem Sie folgende Objekte erstellen können: 
- Zwei virtuelle Computer vom Typ „Standard_B2s“ für Domänencontroller, Verwaltungspunkt und Verteilungspunkt.
- Einen virtuellen Computer vom Typ „Standard_B2ms“ für den primären Standortserver und den SQL-Datenbank-Server.
- Standard_LRS-Speicherkonto

> [!Tip]  
> Der [Azure-Preisrechner](https://azure.microsoft.com/pricing/calculator/) hilft Ihnen, die potenziellen Kosten zu ermitteln.  



## <a name="process"></a>Prozess

1. Wechseln Sie zur [Technical Preview-Vorlage für Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) oder zur [Current Branch-Vorlage für Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Wählen Sie **Bereitstellung in Azure** aus, um das Azure-Portal zu öffnen.  

3. Geben Sie in der Azure-Schnellstartvorlage die folgenden Informationen ein:

    - Grundlagen  

        - **Abonnement**: Der Name des Abonnements, unter dem die VMs erstellt werden sollen  

        - **Ressourcengruppe**: Eine Gruppe von Ressourcen zur Verwendung für diese VMs  

        - **Speicherort:** Ein Azure-Rechenzentrum zum Hosten dieser Laborumgebung  

    - Einstellung  

        - **Präfix**: Der Präfixname der Computer. Weitere Informationen finden Sie unter [Infos zu Azure-VMs](#azure-vm-info).  

        - **Administratorbenutzername**: Der Name eines Benutzers mit Administratorrechten auf den VMs. Verwenden Sie diesen Benutzernamen für die Anmeldung bei den VMs.  

        - **Administratorkennwort**: Das Kennwort muss den Komplexitätsanforderungen von Azure entsprechen. Weitere Informationen finden Sie unter [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Die folgenden Einstellungen müssen für Azure festgelegt werden. Verwenden Sie die Standardwerte. Ändern Sie diese Werte nicht.  
    > 
    > - **\_Artefaktspeicherort**: Der Speicherort für die Skripts dieser Vorlage <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_SAS-Token für den Artefaktspeicherort**: Das für den Zugriff auf den Artefaktspeicherort erforderliche SAS-Token  
    > 
    > - **Speicherort:** Der Speicherort für alle Ressourcen

4. Lesen Sie die Geschäftsbedingungen durch. Wenn Sie einverstanden sind, wählen Sie **Ich stimme den oben genannten Geschäftsbedingungen zu** aus. Wählen Sie anschließend **Purchase** (Kaufen) aus, um den Vorgang fortzusetzen. 

Azure überprüft die Einstellungen und beginnt dann mit der Bereitstellung. Überprüfen Sie im Azure-Portal den Status der Bereitstellung. 

> [!NOTE]
> Der Vorgang kann 2 bis 4 Stunden dauern. Auch wenn im Azure-Portal bereits eine erfolgreiche Bereitstellung angezeigt wird, kann es sein, dass noch Konfigurationsskripts ausgeführt werden. Starten Sie die VMs während dieses Vorgangs nicht.

Stellen Sie eine Verbindung mit dem `<prefix>PS1`-Server her, und rufen Sie die Datei `%windir%\TEMP\ProvisionScript\PS1.json` auf, um den Status der Konfigurationsskripts anzuzeigen. Der Vorgang ist abgeschlossen, wenn alle Schritte als abgeschlossen angezeigt werden.

Zum Herstellen einer Verbindung mit den VMs müssen Sie zunächst im Azure-Portal die öffentlichen IP-Adressen für die einzelnen VMs abrufen. Beim Herstellen einer Verbindung mit der VM lautet der Domänenname `contoso.com`. Verwenden Sie die Anmeldeinformationen, die Sie in der Bereitstellungsvorlage angegeben haben. Weitere Informationen finden Sie unter [Gewusst wie: Herstellen einer Verbindung mit einem virtuellen Azure-Computer unter Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Infos zu Azure-VMs

Für alle drei VMs gelten die folgenden Spezifikationen:
- 150 GB Speicherplatz
- Sowohl eine öffentliche als auch eine private IP-Adresse. Die öffentlichen IP-Adressen befinden sich in einer Netzwerksicherheitsgruppe, in der nur Remotedesktopverbindungen an TCP-Port 3389 zulässig sind. 

Bei dem Präfix, das Sie in der Bereitstellungsvorlage angegeben haben, handelt es sich um das VM-Namenspräfix. Wenn Sie beispielsweise „contoso“ als Präfix festlegen, lautet der Name des Domänencontrollercomputers `contosoDC`.


### `<prefix>DC01`

- Active Directory-Domänencontroller
- Standard_B2s mit zwei Prozessoren und 4 GB Arbeitsspeicher
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Windows-Features und -Rollen
- Active Directory Domain Services (ADDS)
- .NET
- Remotedifferenzialkomprimierung (RDC)


### `<prefix>PS01`

- Standard_B2ms mit zwei Prozessoren und 8 GB Arbeitsspeicher
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows 10 ADK mit Windows PE 
- Primärer Configuration Manager-Standort

#### <a name="windows-features-and-roles"></a>Windows-Features und -Rollen
- .NET
- Remotedifferenzialkomprimierung (RDC) 
- Internetinformationsdienste (IIS)


### `<prefix>DPMP01`

- Standard_B2s mit zwei Prozessoren und 4 GB Arbeitsspeicher
- Windows Server 2019 Datacenter Edition
- Verteilungspunkt
- Verwaltungspunkt

#### <a name="windows-features-and-roles"></a>Windows-Features und -Rollen
- .NET
- Remotedifferenzialkomprimierung (RDC) 
- Internetinformationsdienste (IIS)
- Background Intelligent Transfer Service (BITS)

### `<prefix>CL01`

- Nur für die Evaluierungsvorlage der Current Branch-Version von Configuration Manager
- Windows 10
- Configuration Manager-Client
