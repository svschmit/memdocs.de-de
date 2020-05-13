---
title: Verwaltungstasks für Anwendungen
titleSuffix: Configuration Manager
description: Verwalten von Anwendungen und Bereitstellungstypen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3352f8aa719e93210124d164d89791214eb20bf5
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905861"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Verwaltungstasks für Configuration Manager-Anwendungen

*Gilt für: Configuration Manager (Current Branch)*

Die Informationen in diesem Artikel unterstützen Sie bei der Verwaltung von Anwendungen und Bereitstellungstypen in Configuration Manager.  

Hilfe zum Erstellen von Anwendungen und Bereitstellungstypen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Je nach Anwendungs- oder Bereitstellungstyp sind einige Verwaltungsoptionen möglicherweise nicht verfügbar.  

##  <a name="manage-applications"></a>Verwalten von Anwendungen  
 Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Knoten **Anwendungsverwaltung** >  **Anwendungen**, und wählen Sie die zu verwaltende Anwendung und dann einen Verwaltungstask aus.  

|Aufgabe|Details|  
|----------|-------------|  
|**Zugriffskonten verwalten**|Öffnet das Dialogfeld **Zugriffskonten verwalten** , in dem Sie die zulässige Zugriffsebene für die Inhalte angeben können, die der ausgewählten Anwendung zugeordnet sind.|  
|**Datei für vorab bereitgestellten Inhalt erstellen**|Öffnet den **Assistenten zum Erstellen von vorab bereitgestellten Inhaltsdateien**, mit dessen Hilfe Sie die Verteilung von Inhalten an Remoteverteilungspunkte verwalten können. Wenn die Planung und Einschränkung als Lösung für den Remoteverteilungspunkt nicht infrage kommen, können Sie die Inhalte vorab auf dem Verteilungspunkt bereitstellen.<br /><br /> Siehe [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Revisionsverlauf**|Öffnet das Dialogfeld **Anwendungsrevisionsverlauf**, in dem Sie die Eigenschaften von Revisionen dieser Anwendung anzeigen, alte Revision löschen, und alte Versionen dieser Anwendung wiederherstellen können.<br /><br /> Siehe [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Bereitstellungstyp erstellen**|Öffnet den **Assistenten zum Erstellen neuer Bereitstellungstypen**, mit dessen Hilfe Sie der ausgewählten Anwendung einen neuen Bereitstellungstyp hinzufügen können.<br /><br /> Siehe [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).|  
|**Statistik aktualisieren**|Aktualisiert die Informationen zu Bereitstellungen dieser Anwendung, die im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** angezeigt werden.<br /><br /> Siehe [Überwachen von Anwendungen aus der Configuration Manager-Konsole](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Reaktivieren**|Reaktiviert eine Anwendung, die mithilfe des Verwaltungstasks **Außerkraftsetzen** außer Kraft gesetzt wurde.|  
|**Außerkraftsetzen**|Außer Kraft gesetzte Anwendungen können nicht mehr bereitgestellt werden, jedoch werden weder die Anwendung noch Bereitstellungen der Anwendung gelöscht. Bereits auf Clientcomputern installierte Exemplare dieser Anwendung werden nicht entfernt. Alle Anwendungsrevisionen werden von Configuration Manager nach 60 Tagen gelöscht. Installierte Kopien der Anwendung werden jedoch nicht entfernt.<br /><br /> Zum Löschen einer Anwendung müssen Sie diese zunächst außer Kraft setzen, sämtliche Bereitstellungen löschen, Verweise anderer Bereitstellungen auf diese Anwendung entfernen, und dann sämtliche Revisionen der Anwendung löschen.<br /><br /> Siehe [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exportierenieren**|Öffnet den **Assistenten zum Exportieren von Anwendungen**, mit dessen Hilfe Sie die ausgewählten Anwendungen in eine ZIP-Datei exportieren können. Diese Datei können Sie dann archivieren oder an einem anderen Standort installieren. Wenn Sie den Inhalt der Anwendung exportieren, wird ein Ordner erstellt, in dem sich der Inhalt befindet.<br /><br /> Sie können darüber hinaus Anwendungsabhängigkeiten, Ablösungsbeziehungen und -bedingungen und Inhalt für die Anwendung und ihre Abhängigkeiten exportieren.<br /><br /> Das Windows PowerShell-Cmdlet **Export-CMApplication** hat die gleiche Funktion. Weitere Informationen finden Sie unter [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication?view=sccm-ps).|  
|**Löschen**|Löscht die derzeit ausgewählte Anwendung.<br /><br /> Eine Anwendung kann nicht gelöscht werden, wenn andere Anwendungen von ihr abhängig sind oder sie über eine aktive Bereitstellung oder abhängige Tasksequenzen verfügt.|  
|**Bereitstellung simulieren**|Öffnet den **Assistenten zum Simulieren der Anwendungsbereitstellung**, mit dessen Hilfe Sie die Ergebnisse einer Anwendungsbereitstellung auf Computern ohne Installieren oder Deinstallieren der Anwendung überprüfen können.<br /><br /> Siehe [Simulieren von Anwendungsbereitstellungen](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Bereitstellen**|Öffnet den **Assistenten zum Bereitstellen von Software**, mit dessen Hilfe Sie die ausgewählte Anwendung auf Sammlungen oder Computern in Ihrer Hierarchie bereitstellen können.<br /><br /> Siehe [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).|  
|**Inhalt verteilen**|Öffnet den **Assistenten für die Verteilung von Inhalt**, mit dessen Hilfe Sie den Inhalt für die ausgewählte Anwendung auf Verteilungspunkte in Ihrer Hierarchie kopieren können.<br /><br /> Siehe [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Beziehungen anzeigen**|Zeigt eine grafische Darstellung der Beziehungen der ausgewählten Anwendungen zu anderen Anwendungen an. Wählen Sie eine der folgenden Optionen:<br><br><ul><li>**Abhängigkeit**: Zeigt die Anwendungen an, die von der ausgewählten Anwendung abhängig sind, und Anwendungen, von denen die ausgewählte Anwendung abhängig ist.</li><li>**Ablösung**: Zeigt Anwendungen, die die ausgewählte Anwendung ablösen, und Anwendungen, die von der ausgewählten Anwendung abgelöst werden.</li><li>**Globale Bedingungen**: Zeigt die globalen Bedingungen an, auf die von dieser Anwendung verwiesen werden.</li></ol><br /> Informationen hierzu finden Sie unter [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md) und [Erstellen von globalen Bedingungen](../../apps/deploy-use/create-global-conditions.md).|  
|**Anwendungen kopieren:**|Kopiert oder dupliziert Configuration Manager-Anwendungen, um eine neue zu erstellen. Diese Aktion ist nützlich, wenn Sie etwas testen möchten oder eine ähnliche Anwendung erstellen müssen. Der Standort erstellt eine neue Anwendung mit **-copy** an den Namen angehängt. Der Standort kopiert die meisten Metadaten zwar in die neue Anwendung, kopiert aber keine Bereitstellungen.|

##  <a name="manage-deployment-types"></a>Verwalten von Bereitstellungstypen  
 Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Anwendungsverwaltung**, und wählen Sie **Anwendungen** und dann die gewünschte Anwendung aus, die den Bereitstellungstyp enthält, den Sie verwalten möchten. Wählen Sie im Detailbereich die Registerkarte **Bereitstellungstypen** aus. Wählen Sie den Bereitstellungstyp, den Sie verwalten möchten, und anschließend einen Verwaltungstask aus.  

|Aufgabe|Details|  
|----------|-------------|  
|**Priorität erhöhen**|Erhöht die Priorität des ausgewählten Bereitstellungstyps. Bereitstellungstypen werden der Reihe nach ausgewertet. Wenn ein Bereitstellungstyp den angegebenen Anforderungen entspricht, wird er ausgeführt, und weitere Bereitstellungstypen in der Prioritätenliste werden nicht ausgewertet.|  
|**Priorität verringern**|Verringert die Priorität des ausgewählten Bereitstellungstyps.|  
|**Löschen**|Löscht den ausgewählten Bereitstellungstyp.<br><br>Ein Bereitstellungstyp kann nicht gelöscht werden, wenn er von einem Bereitstellungstyp in einer anderen Anwendung referenziert wird.<br>Zum Löschen eines Bereitstellungstyps müssen Sie für den Bereitstellungstyp alle Abhängigkeiten entfernen, die in anderen Bereitstellungstypen enthalten sind.<br>Darüber hinaus müssen Sie alle früheren Anwendungsrevisionen mit Bereitstellungstypen entfernen, von denen auf den zu löschenden Bereitstellungstyp verwiesen wird.|  
|**Inhalt aktualisieren**|Aktualisiert den Inhalt für den ausgewählten Bereitstellungstyp.<br /><br /> Wenn Sie diesen Assistenten für einen Bereitstellungstyp starten, der eine virtuelle Anwendung enthält, wird der **Assistent für das Update von Inhalten** gestartet. Mithilfe dieses Assistenten können Sie Veröffentlichungsoptionen und Anforderungsregeln für die ausgewählte virtuelle Anwendung ändern. Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).<br /><br /> Wenn Sie den Inhalt eines Bereitstellungstyps aktualisieren, wird eine neue Revision der Anwendung erstellt. Dies kann dazu führen, dass Clientgeräte mit der neuen Anwendung aktualisiert werden.|  
