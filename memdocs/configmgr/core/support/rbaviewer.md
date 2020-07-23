---
title: Tool für die rollenbasierte Verwaltung
titleSuffix: Configuration Manager
description: Verwenden Sie das Tool für die rollenbasierte Verwaltung und Überwachung, um Sicherheitsrollen und -bereiche in Configuration Manager zu erstellen und zu überwachen.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4cf9d4d3f9d1b2f439d2e87d41cc280e7af0805a
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239707"
---
# <a name="role-based-administration-and-auditing-tool"></a>Tool für die rollenbasierte Verwaltung und Überwachung

*Gilt für: Configuration Manager (Current Branch)*

Das Tool für die rollenbasierte Verwaltung und Überwachung ist eines der [Configuration Manager-Tools](tools.md). Sie können dieses Tool für folgende Tasks verwenden:

- Modellsicherheitsrollen mit bestimmten Berechtigungen  

- Überwachen der Sicherheitsbereiche und Sicherheitsrollen anderer Benutzer



## <a name="requirements"></a>Anforderungen

- Das Tool muss auf demselben Computer wie der Configuration Manager-Standortserver ausgeführt werden. 

- Sie verfügen über die Rolle **Hauptadministrator**, **Analyst mit Leseberechtigung** oder **Sicherheitsadministrator**.  

- Ihrem Konto müssen der Sicherheitsbereich **Alle** und sämtliche Sammlungen zugewiesen werden.  

- (*Optional*) Sie benötigen SQL-Zugriff, um die Sicherheit des Berichtsordners analysieren zu können.  

- (*Optional*) Zum Analysieren des Drillthroughs eines Berichts müssen Sie dieses Tool auf dem Standortsystemserver mit der Rolle für den Berichterstattungspunkt ausführen.



## <a name="procedures"></a>Vorgehensweisen


### <a name="model-permissions-for-a-new-role"></a>Modellberechtigungen für eine neue Rolle

Verwenden Sie die folgende Prozedur für Modellberechtigungen für eine neu zu erstellende Rolle: 

1. Führen Sie **RBAViewer.exe** aus.  

2. Wählen Sie die Sicherheitsrollen aus, die als Grundlage dienen sollen, oder beginnen Sie mit einem leeren Berechtigungssatz. Wählen Sie die erforderlichen Berechtigungen aus.  

3. Klicken Sie auf **Analysieren**, um die Benutzeroberfläche anzuzeigen, die dieser benutzerdefinierten Rolle angezeigt wird.  

    > [!Note]  
    > Wechseln Sie zur Registerkarte **Ähnlichkeit**, um zu überprüfen, ob eine Sicherheitsrolle vorhanden ist, die Ihre Anforderungen erfüllt.  

4. Klicken Sie auf **Exportieren**, um die Rolle als XML-Datei zu speichern. Sie können die Rolle anschließend über die Configuration Manager-Konsole importieren. Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Sicherheitsrollen](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Überwachen vorhandener Sicherheitsbereiche

Gehen Sie wie folgt vor, um sämtliche vorhandenen Administratoren, Sammlungen und Sicherheitsbereiche in Configuration Manager zu überwachen:

1. Führen Sie **RBAViewer.exe** aus.  

2. Klicken Sie auf der Symbolleiste auf die Schaltfläche **Audit RBA** (RBA überwachen).  

    1. Wechseln Sie zur Registerkarte **Collection Summary** (Sammlungszusammenfassung), um die auf eine Sammlung begrenzten Beziehungen in einer Strukturansicht anzuzeigen.  

    2. Wechseln Sie zur Registerkarte **Bereichszusammenfassung**, um die Objekte anzuzeigen, die einer Sicherheitsrolle zugewiesen sind.  


### <a name="audit-a-specific-user"></a>Überwachen eines bestimmten Benutzers

Gehen Sie wie folgt vor, um die Konfiguration für die rollenbasierte Verwaltung für einen bestimmten Benutzer zu überwachen:

1. Führen Sie **RBAViewer.exe** aus.  

2. Klicken Sie auf der Symbolleiste auf die Schaltfläche **Ausführen als**.  

3. Geben Sie den Namen des bestimmten Benutzers ein, um die Berechtigungen für dieses Konto zu überprüfen.  

4. Das Tool zeigt die Sicherheitsrollen an, die dem Benutzer zugewiesen sind, oder die Sicherheitsgruppe, zu der der Benutzer gehört. Zudem zeigt es die Objekte an, die dem Benutzer angezeigt werden, und die Maßnahmen, die dieser in der Konsole ergreifen kann.  



## <a name="see-also"></a>Weitere Informationen:

- [Grundlagen der rollenbasierten Verwaltung](../understand/fundamentals-of-role-based-administration.md)
- [Configure role-based administration (Konfigurieren der rollenbasierten Verwaltung)](../servers/deploy/configure/configure-role-based-administration.md)
