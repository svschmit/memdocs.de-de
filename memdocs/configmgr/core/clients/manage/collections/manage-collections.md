---
title: Verwalten von Sammlungen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie allgemeine Verwaltungsaufgaben für Sammlungen in Configuration Manager ausführen.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fc8347ae766cbd16075ef4170efa2f8042371f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695308"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Verwalten von Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe der Übersichtsinformationen in diesem Artikel können Sie Verwaltungsaufgaben für Sammlungen in Configuration Manager ausführen.  

> [!NOTE]  
>  Weitere Informationen zum Erstellen von Configuration Manager-Sammlungen finden Sie unter [Erstellen von Sammlungen](create-collections.md).



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a>Verwalten von Gerätesammlungen  

Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Gerätesammlungen**und dann die zu verwaltende Sammlung aus. Wählen Sie anschließend einen Verwaltungstask aus.  


#### <a name="show-members"></a>Mitglieder anzeigen
Zeigt alle Ressourcen an, die Mitglieder der ausgewählten Sammlung in einem temporären Knoten unter dem Knoten **Geräte** sind.


#### <a name="add-selected-items"></a>Ausgewählte Elemente hinzufügen
Bietet folgende Optionen: 

- **Ausgewählte Elemente der vorhandenen Gerätesammlung hinzufügen:** Öffnet das Dialogfeld **Sammlung auswählen** . Wählen Sie die Sammlung aus, der Sie die Mitglieder der ausgewählten Sammlung hinzufügen möchten. Die ausgewählte Sammlung wird durch die Mitgliedschaftsregel **Sammlungen einschließen** in diese Sammlung eingeschlossen.  

- **Ausgewählte Elemente der neuen Gerätesammlung hinzufügen:** öffnet den **Assistenten zum Erstellen von Gerätesammlungen**, mit dem Sie eine neue Sammlung erstellen können. Die ausgewählte Sammlung wird durch die Mitgliedschaftsregel **Sammlungen einschließen** in diese Sammlung eingeschlossen.  


Weitere Informationen finden Sie unter [Erstellen von Sammlungen](create-collections.md).


#### <a name="install-client"></a>Client installieren
Öffnet den **Assistenten zur Clientinstallation**. Dieser Assistent installiert mithilfe einer Clientpushinstallation einen Configuration Manager-Client auf allen Computern in der ausgewählten Sammlung. Weitere Informationen finden Sie unter [Clientpushinstallation](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


#### <a name="run-script"></a>Skript ausführen
Öffnet den **Assistenten zur Skriptausführung**, um ein PowerShell-Skript auf allen Clients in der Sammlung auszuführen. Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Affinitätsanforderungen verwalten
Öffnet das Dialogfeld **Affinitätsanforderungen zwischen Benutzer und Gerät verwalten**. Sie können ausstehende Anforderungen genehmigen oder ablehnen, um Affinitäten zwischen Benutzern und Geräten für Geräte in der ausgewählten Sammlung festzulegen. Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).


#### <a name="clear-required-pxe-deployments"></a>Erforderliche PXE-Bereitstellungen löschen
Löscht alle erforderlichen PXE-Startbereitstellungen von allen Mitgliedern der ausgewählten Sammlung. Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).


#### <a name="update-membership"></a>Mitgliedschaft aktualisieren
Wertet die Mitgliedschaft für die ausgewählte Sammlung aus. Bei Sammlungen mit vielen Mitgliedern kann dieser Vorgang einige Zeit in Anspruch nehmen. Mit der Aktion **Aktualisieren** können Sie die Anzeige mit den neuen Sammlungsmitgliedern nach Abschluss des Vorgangs aktualisieren.


#### <a name="add-resources"></a>Ressourcen hinzufügen
Öffnet das Dialogfeld **Ressourcen zur Sammlung hinzufügen**. Suchen Sie nach neuen Ressourcen, die Sie der ausgewählten Sammlung hinzufügen möchten. Während des Vorgangs wird für die ausgewählte Sammlung ein Sanduhrsymbol angezeigt.


#### <a name="client-notification"></a>Clientbenachrichtigung
Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](../client-notification.md).


#### <a name="endpoint-protection"></a>Endpoint Protection
Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](../client-notification.md).


#### <a name="export"></a>Exportieren
Öffnet den **Assistenten zum Exportieren von Sammlungen**, mit dem Sie diese Sammlung in eine MOF-Datei (Managed Object Format) exportieren können. Diese Datei kann dann an einem anderen Configuration Manager-Standort archiviert oder importiert werden. Wenn Sie eine Sammlung exportieren, werden referenzierte Sammlungen nicht exportiert. Auf eine referenzierte Sammlung wird von der ausgewählten Sammlung durch eine **Einbeziehungsregel** oder eine **Ausschlussregel** verwiesen.


#### <a name="copy"></a>Kopieren
Erstellt eine Kopie der ausgewählten Sammlung. Von der neuen Sammlung wird die ausgewählte Sammlung als begrenzende Sammlung verwendet.


#### <a name="refresh"></a>Aktualisieren
Aktualisiert die Ansicht.


#### <a name="delete"></a>Löschen
Löscht die ausgewählte Sammlung. Sie können auch alle Ressourcen in der Sammlung aus der Standortdatenbank löschen. 

In Configuration Manager integrierte Sammlungen können nicht gelöscht werden. Eine Liste der integrierten Sammlungen finden Sie unter [Einführung in Sammlungen](introduction-to-collections.md#built-in-collections).


#### <a name="simulate-deployment"></a>Bereitstellung simulieren
Öffnet den **Assistenten zum Simulieren der Anwendungsbereitstellung**. Mit diesem Assistenten können Sie die Ergebnisse einer Anwendungsbereitstellung ohne Installieren oder Deinstallieren der Anwendung testen. Weitere Informationen finden Sie unter [Simulieren von Anwendungsbereitstellungen](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Bereitstellen
Zeigt folgende Optionen an:  

- **Anwendung:** öffnet den **Assistenten zum Bereitstellen von Software**. Wählen Sie eine Anwendungsbereitstellung aus, und konfigurieren Sie sie für die ausgewählte Sammlung. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../../../apps/deploy-use/deploy-applications.md).  

- **Programm**: öffnet den **Assistenten zum Bereitstellen von Software**. Wählen Sie eine Programmbereitstellung aus, und konfigurieren Sie sie für die ausgewählte Sammlung. Weitere Informationen finden Sie unter [Pakete und Programme](../../../../apps/deploy-use/packages-and-programs.md).  

- **Konfigurationsbaseline:** öffnet das Dialogfeld **Konfigurationsbaselines bereitstellen**. Konfigurieren Sie die Bereitstellung von mindestens einer Konfigurationsbaseline für die ausgewählte Sammlung. Weitere Informationen finden Sie unter [Bereitstellen von Konfigurationsbaselines](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Tasksequenz:** öffnet den **Assistenten zum Bereitstellen von Software**. Wählen Sie eine Tasksequenz aus, und konfigurieren Sie sie für die ausgewählte Sammlung. Weitere Informationen finden Sie unter [Verwalten von Tasksequenzen zum Automatisieren von Aufgaben](../../../../osd/deploy-use/deploy-a-task-sequence.md).  

- **Softwareupdates:** öffnet den **Assistenten zum Bereitstellen von Softwareupdates**. Konfigurieren Sie die Bereitstellung von Softwareupdates für Ressourcen in der ausgewählten Sammlung. Weitere Informationen finden Sie unter [Verwalten von Softwareupdates](../../../../sum/understand/software-updates-introduction.md).  


#### <a name="clear-server-group-deployment-locks"></a>Bereitstellungssperren für Servergruppe löschen
Geben Sie manuell alle Servergruppen-Bereitstellungssperren für die Sammlung frei. Weitere Informationen finden Sie unter [Bereitstellen einer Servergruppe](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Verschieben
Verschieben Sie die ausgewählte Sammlung in einen anderen Ordner auf dem Knoten **Gerätesammlungen**. 


#### <a name="properties"></a>Eigenschaften
Weitere Informationen finden Sie unter [Sammlungseigenschaften](#BKMK_CollProp).  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a>Verwalten von Benutzersammlungen  

Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Benutzersammlungen**und dann die zu verwaltende Sammlung aus. Wählen Sie anschließend einen Verwaltungstask aus.  

> [!Note]  
> Die folgenden Aktionen sind für Benutzersammlungen verfügbar – doch das Verhalten ist das gleiche wie bei Gerätesammlungen. Abgesehen davon gelten sie für Benutzersammlungen und die darin enthaltenen Benutzer. Weitere Informationen zu den einzelnen Aktionen finden Sie unter [Verwalten von Gerätesammlungen](#bkmk_device).  

- **Mitglieder anzeigen**  
- **Ausgewählte Elemente hinzufügen**  
    - **Ausgewählte Elemente der vorhandenen Benutzersammlung hinzufügen**  
    - **Ausgewählte Elemente der neuen Benutzersammlung hinzufügen**  
- **Affinitätsanforderungen verwalten**  
- **Mitgliedschaft aktualisieren**  
- **Ressourcen hinzufügen**  
- **Exportierenieren**  
- **Kopieren**  
- **Aktualisieren**  
- **Löschen**  
- **Bereitstellung simulieren**  
- **Bereitstellen**  
    - **Anwendung**  
    - **Programm**  
    - **Konfigurationsbaseline**
- **Verschieben**  
- **Eigenschaften**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Sammlungseigenschaften  

Wenn Sie das Dialogfeld **Eigenschaften** für eine Sammlung öffnen, können Sie die folgenden Optionen ansehen und konfigurieren:  

#### <a name="general"></a>Allgemein
Hier können Sie allgemeine Informationen zur ausgewählten Sammlung ansehen und konfigurieren, einschließlich des Sammlungsnamens und der begrenzenden Sammlung.

#### <a name="membership-rules"></a>Mitgliedschaftsregeln
Hier können Sie die Mitgliedschaftsregeln konfigurieren, die die Mitgliedschaft dieser Sammlung definieren. Weitere Informationen finden Sie unter [Erstellen von Sammlungen](create-collections.md).  

#### <a name="power-management"></a>Energieverwaltung
Hier können Sie Energieverwaltungspläne konfigurieren, die Sie Computern in der ausgewählten Sammlung zugewiesen haben. Weitere Informationen finden Sie unter [Einführung in die Energieverwaltung](../power/introduction-to-power-management.md).  

#### <a name="deployments"></a>Bereitstellungen
Hier wird jede Software angezeigt, die Sie für Mitglieder der ausgewählten Sammlung bereitgestellt haben.  

#### <a name="maintenance-windows"></a>Wartungsfenster
Hier können Sie Wartungsfenster anzeigen und konfigurieren, die auf Mitglieder der ausgewählten Sammlung angewendet werden. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](use-maintenance-windows.md).

#### <a name="collection-variables"></a>Sammlungsvariablen
Hier können Sie Variablen konfigurieren, die für diese Sammlung gelten und von Tasksequenzen verwendet werden können. Weitere Informationen finden Sie unter [Festlegen von Tasksequenzvariablen](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set).  

#### <a name="distribution-point-groups"></a>Verteilungspunktgruppen
Hier können Sie mindestens eine Verteilungspunktgruppe Mitgliedern der ausgewählten Sammlung zuordnen. Weitere Informationen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

#### <a name="aad-group-sync"></a>Synchronisieren von AAD-Gruppen
Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen. Diese Synchronisierung ist eine [Featurevorabversion](../../../servers/manage/pre-release-features.md), die ab Version 1906 verfügbar ist. Weitere Informationen finden Sie unter [Erstellen von Sammlungen](create-collections.md#bkmk_aadcollsync).

#### <a name="security"></a>Sicherheit
Auf dieser Registerkarte können Sie die Administratoren anzeigen, die dank zugeordneter Rollen und Sicherheitsbereiche über Berechtigungen für die ausgewählte Sammlung verfügen Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../../understand/fundamentals-of-role-based-administration.md).  

#### <a name="alerts"></a>Warnungen 
Hier können Sie konfigurieren, wann Warnungen zu Clientstatus und Endpoint Protection generiert werden. Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus](../../deploy/configure-client-status.md) und [Überwachen von Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Verwenden von PowerShell

PowerShell kann zum Verwalten von Sammlungen verwendet werden.  Weitere Informationen finden Sie in folgenden Quellen:

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)
