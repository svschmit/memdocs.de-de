---
title: Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Verwendung des Migrationstools zur programmgesteuerten Erstellung von Azure-VMs für Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707938"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure

*Gilt für: Configuration Manager (Current Branch)*


Dieses in Version 1910 eingeführte Tool unterstützt Sie dabei, Azure-VMs für Configuration Manager programmgesteuert zu erstellen. <!--3556022--> Es lässt sich mit Standortrollen mit Standardeinstellungen für passive Standortserver, Verwaltungspunkte und Verteilungspunkte installieren. Sobald Sie die neuen Rollen überprüft haben, können Sie sie als zusätzliche Standortsysteme für Hochverfügbarkeit verwenden. Sie können auch die lokale Standortsystemrolle entfernen und nur die Azure-VM-Rolle beibehalten.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Azure-Abonnement

- Ein virtuelles Azure-Netzwerk mit ExpressRoute-Gateway

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Ihr Benutzerkonto muss **Hauptadministrator** in Configuration Manager sein und über Administratorrechte auf dem primärer Standortserver verfügen.

- Damit ein passiver Server hinzugefügt werden kann, muss der primäre Standort die [Hochverfügbarkeitsanforderungen der Standortserver](../servers/deploy/configure/site-server-high-availability.md#prerequisites) erfüllen. Beispielsweise ist eine [Remoteinhaltsbibliothek](../plan-design/hierarchy/the-content-library.md#bkmk_remote) erforderlich.

### <a name="required-azure-permissions"></a>Erforderliche Azure-Berechtigungen

Sie benötigen die folgenden Berechtigungen in Azure, wenn Sie das Tool ausführen:
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


Weitere Informationen zu den Berechtigungen und Rollenzuweisungen finden Sie unter [Hinzufügen oder Entfernen von Rollenzuweisungen mithilfe von Azure RBAC und dem Azure-Portal](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Ausführen des Tools

1. Melden Sie sich beim primären Standortserver an, und führen Sie das folgende Tool im Configuration Manager-Installationsverzeichnis aus: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Lesen Sie die Informationen auf der Registerkarte **Allgemein**, und wechseln Sie dann zur Registerkarte **Azure-Informationen**.

1. Wählen Sie auf der Registerkarte **Azure-Informationen** Ihre **Azure-Umgebung** aus, und klicken Sie auf **Anmelden**.

    > [!TIP]
    > Möglicherweise müssen Sie `https://*.microsoft.com` zu Ihrer Liste der vertrauenswürdigen Websites hinzufügen, um sich ordnungsgemäß anzumelden.

    [![Registerkarte „Azure-Informationen“ im Tool zum Erweitern und Migrieren](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Wählen Sie nach der Anmeldung Ihre **Abonnement-ID** und Ihr **Virtuelles Netzwerk** aus. Das Tool listet nur Netzwerke mit ExpressRoute-Gateway auf.

## <a name="site-server-high-availability"></a>Standortserver-Hochverfügbarkeit

1. Wählen Sie auf der Registerkarte **Standortserver-Hochverfügbarkeit** die Option **Überprüfen** aus, um die Bereitschaft Ihres Standorts zu bewerten.

    Wenn eine der Überprüfungen nicht erfolgreich verläuft, klicken Sie auf **Weitere Details**, um zu ermitteln, wie sich das Problem beheben lässt. Weitere Informationen zu diesen Voraussetzungen finden Sie unter [Hochverfügbarkeit der Standortserver](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Wenn Sie Ihren Standortserver auf Azure erweitern oder zu Azure migrieren möchten, klicken Sie auf **Standortserver in Azure erstellen**. Füllen Sie dann folgende Felder aus:

    |Name|Beschreibung|
    |---|---|
    |**Abonnement**|Schreibgeschützt. Zeigt Namen und ID des Abonnements an.|
    |**Ressourcengruppe**| Listet verfügbare Ressourcengruppen auf. Wenn Sie eine neue Ressourcengruppe erstellen müssen, wechseln Sie zum [Azure-Portal](https://portal.azure.com), und führen Sie dieses Tool dann erneut aus.|
    |**Speicherort**| Schreibgeschützt. Wird durch den Standort Ihres virtuellen Netzwerks bestimmt.|
    |**VM-Größe**|Wählen Sie eine für Ihre Workload passende Größe aus. Microsoft empfiehlt **Standard_DS3_v2**.|
    |**Betriebssystem**|Schreibgeschützt. Das Tool verwendet Windows Server 2019.|
    |**Datenträgertyp**|Schreibgeschützt. Das Tool verwendet SSD Premium-Datenträger, um eine optimale Leistung zu erzielen.|
    |**Virtuelles Netzwerk**|Schreibgeschützt.|
    |**Subnetz**|Wählen Sie das zu verwendende Subnetz aus. Wenn Sie ein neues Subnetz erstellen müssen, verwenden Sie dafür das [Azure-Portal](https://portal.azure.com).|
    |**Computername**|Geben Sie den Namen der VM des passiven Standortservers in Azure ein. Es handelt sich um denselben Namen, der auch im [Azure-Portal](https://portal.azure.com) angezeigt wird.|
    |**Benutzername des lokalen Administrators**|Geben Sie den Namen des lokalen Administratorbenutzers ein, der die Azure-VM erstellt, bevor dieser der Domäne beitritt.|
    |**Kennwort des lokalen Administrators**|Das Kennwort des lokalen Administratorbenutzers. Um das Kennwort während der Azure-Bereitstellung zu schützen, speichern Sie es als Geheimnis in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Verwenden Sie dieses dann hier als Referenz. Erstellen Sie bei Bedarf im [Azure-Portal](https://portal.azure.com) ein neues Kennwort.|
    |**Vollqualifizierter Domänenname**|Der vollqualifizierte Domänenname (Fully Qualified Domain Name, FQDN) für die Active Directory-Domäne, der der Server beitreten soll. Standardmäßig ruft das Tool diesen Wert von Ihrem aktuellen Computer ab.|
    |**Domänenbenutzername**|Der Name des Domänenbenutzers, der der Domäne beitreten darf. Standardmäßig verwendet das Tool den Namen des aktuell angemeldeten Benutzers.|
    |**Domänenkennwort**|Das Kennwort des Domänenbenutzers, der der Domäne beitritt. Das Tool überprüft dies, nachdem Sie auf **Start** geklickt haben. Um das Kennwort während der Azure-Bereitstellung zu schützen, speichern Sie es als Geheimnis in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Verwenden Sie dieses dann hier als Referenz. Erstellen Sie bei Bedarf im [Azure-Portal](https://portal.azure.com) ein neues Kennwort.|
    |**DNS-IP der Domäne**|Wird zum Einbinden der Domäne verwendet. Standardmäßig verwendet das Tool den aktuellen DNS-Wert Ihres aktuellen Computers.|
    |**Typ**|Schreibgeschützt. Als Typ wird *Passiver Standortserver* angezeigt.|

    > [!IMPORTANT]
    > Standardmäßig ist die Option **Vorhandene Windows Server-Lizenz verwenden** für die virtuellen Computer auf **Nein** festgelegt. Wenn Sie Ihre lokalen Windows Server-Lizenzen mit Software Assurance nutzen möchten, konfigurieren Sie diese Einstellung im [Azure-Portal](https://portal.azure.com), nachdem die virtuellen Computer bereitgestellt wurden. Weitere Informationen finden Sie unter [Azure-Hybridvorteil für Windows Server](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit).

1. Um mit der Bereitstellung der Azure-VM zu beginnen, klicken Sie auf **Start**. Zum Überwachen des Bereitstellungsstatus wechseln Sie im Tool zur Registerkarte **Bereitstellungen in Azure**. Um den neuesten Status abzurufen, klicken Sie auf **Bereitstellungsstatus aktualisieren**.

    > [!TIP]
    > Sie können auch das [Azure-Portal](https://portal.azure.com) verwenden, um den Status zu überprüfen, Fehler zu finden und mögliche Problembehebungen zu ermitteln.

1. Wenn die Bereitstellung abgeschlossen ist, wechseln Sie zu Ihren SQL Server-Instanzen, und erteilen Sie Berechtigungen für die neue Azure-VM. Weitere Informationen finden Sie unter [Hochverfügbarkeit des Standortservers: Erforderliche Komponenten](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Um die Azure-VM als Standortserver im passiven Modus hinzuzufügen, klicken Sie auf **Standortserver im passiven Modus hinzufügen**.

1. Sobald der Standort den Standortserver im passiven Modus hinzugefügt hat, wird der Status auf der Registerkarte **Standortserver-Hochverfügbarkeit** angezeigt.

   [![Passiver Standortserver zur Registerkarte „Standortserver-Hochverfügbarkeit“ hinzugefügt](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Wechseln Sie jetzt zur Registerkarte [Bereitstellungen in Azure](#bkmk_deploy-azure), um die Bereitstellung abzuschließen.

## <a name="site-database"></a>Standortdatenbank

Das Tool verfügt derzeit über keine Aufgaben zum Migrieren der Datenbank aus dem lokalen Standort zu Azure. Sie können die Datenbank von einer lokalen SQL Server-Instanz auf eine Azure-SQL Server-VM verschieben. Das Tool listet auf der Registerkarte **Standortdatenbank** die folgenden Artikel auf, die Sie hierbei unterstützen:

- [Sichern und Wiederherstellen der Datenbank](../servers/manage/backup-and-recovery.md)
- [Konfigurieren von SQL Always On und Zulassen der Datenreplikation](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Migrieren einer SQL-Datenbank zu einer Azure-SQL Server-VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Standortsystemrollen

1. Wechseln Sie zur Registerkarte **Standortsystemrollen**. Um eine neue Standortsystemrolle mit Standardeinstellungen bereitzustellen, klicken Sie auf **Neu erstellen**. Sie können Rollen wie z. B. „Verwaltungspunkt“, „Verteilungspunkt“ und „Softwareupdatepunkt“ bereitstellen. Derzeit sind nicht alle Rollen im Tool verfügbar.

    [![Registerkarte „Standortsystemrollen“ im Tool zum Erweitern und Migrieren](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. Füllen Sie die Felder im Bereitstellungsfenster aus, um die VM der Standortrolle in Azure bereitzustellen. Diese Informationen sind die gleichen wie in der oben stehenden Liste für den Standortserver.

1. Um mit der Bereitstellung der Azure-VM zu beginnen, klicken Sie auf **Start**. Zum Überwachen des Bereitstellungsstatus wechseln Sie im Tool zur Registerkarte **Bereitstellungen in Azure**. Um den neuesten Status abzurufen, klicken Sie auf **Bereitstellungsstatus aktualisieren**.

    > [!TIP]
    > Sie können auch das [Azure-Portal](https://portal.azure.com) verwenden, um den Status zu überprüfen, Fehler zu finden und mögliche Problembehebungen zu ermitteln.

1. Wiederholen Sie diesen Vorgang, um weitere Standortsystemrollen hinzuzufügen.

1. Wechseln Sie jetzt zur Registerkarte [Bereitstellungen in Azure](#bkmk_deploy-azure), um die Bereitstellung abzuschließen.

1. Wenn die Bereitstellung abgeschlossen ist, wechseln Sie zur Configuration Manager-Konsole, um weitere Änderungen an der Standortrolle vorzunehmen.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Bereitstellungen in Azure

1. Nachdem Azure die VM erstellt hat, wechseln Sie im Tool zur Registerkarte **Bereitstellungen in Azure**. Klicken Sie auf **Bereitstellen**, um die Rolle mit den Standardeinstellungen zu konfigurieren.

1. Klicken Sie auf **Ausführen**, um das PowerShell-Skript zu starten.

    [![Bereitstellen von Standortrollen durch Ausführen des generierten PowerShell-Skripts](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Wiederholen Sie diesen Vorgang, um weitere Rollen zu konfigurieren.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> Hinzufügen von Standortrollen zu einer vorhandenen Bereitstellung virtueller Maschinen
<!--5665775, 6307931-->
Ab Version 2002 von Configuration Manager unterstützt das Tool „Extend and migrate on-premises site to Microsoft Azure“ (Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure) die Bereitstellung mehrerer Standortsystemrollen auf einer einzigen Azure-VM. Sie können Standortsystemrollen nach Abschluss der ersten Bereitstellung der Azure-VM hinzufügen. Gehen Sie wie folgt vor, um eine neue Rolle zu einer vorhandenen VM hinzuzufügen:
1. Klicken Sie in der Registerkarte **Deployments in Azure** (Bereitstellungen in Azure) auf eine Bereitstellung einer virtuellen Maschine mit dem Status **Abgeschlossen**.
1. Klicken Sie auf die Schaltfläche **Neu erstellen**, um der virtuellen Maschine eine zusätzliche Rolle hinzuzufügen.


## <a name="next-steps"></a>Nächste Schritte

Überprüfen Ihrer Änderungen im [Azure-Portal](https://portal.azure.com)
