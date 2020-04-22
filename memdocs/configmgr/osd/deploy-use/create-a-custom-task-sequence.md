---
title: Erstellen einer benutzerdefinierten Tasksequenz
titleSuffix: Configuration Manager
description: Bearbeiten einer benutzerdefinierten Tasksequenz in Configuration Manager, um Schritte zur Tasksequenz hinzuzufügen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9107e9787cf7f12cab624101c37344ea20684112
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704198"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Erstellen einer benutzerdefinierten Tasksequenz mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie eine benutzerdefinierte Tasksequenz in Configuration Manager erstellen, enthält diese keine Tasksequenzschritte. Bearbeiten Sie die Tasksequenz nach der Erstellung, und fügen Sie die benötigten Tasksequenzschritte hinzu.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> Erstellen einer benutzerdefinierten Tasksequenz

Gehen Sie folgendermaßen vor, um eine benutzerdefinierte Tasksequenz zu erstellen:

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

1. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz erstellen** aus. Daraufhin wird der Tasksequenzerstellungs-Assistent gestartet.  

1. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Neue benutzerdefinierte Tasksequenz erstellen**aus.  

1. Geben Sie auf der Seite **Informationen zur Tasksequenz** Folgendes an:

    - Einen Namen für die Tasksequenz
    - Eine Beschreibung der Tasksequenz
    - Optional ein Startimage, das von der Tasksequenz verwendet werden soll

Nachdem Sie den Tasksequenzerstellungs-Assistenten abgeschlossen haben, fügt Configuration Manager dem Knoten **Tasksequenzen** eine benutzerdefinierte Tasksequenz hinzu. Sie können diese Tasksequenz dann bearbeiten, um ihr Schritte hinzuzufügen.  

## <a name="see-also"></a>Weitere Informationen:

Eine Liste verfügbarer Tasksequenzschritte finden Sie unter [Tasksequenzschritte](../understand/task-sequence-steps.md).  

Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md).  

Am häufigsten werden Sie Tasksequenzen zum Automatisieren von Betriebssystem-Bereitstellungstasks verwenden, Sie können jedoch auch eine benutzerdefinierte Tasksequenz erstellen, um andere Arten von Tasks zu automatisieren. Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen](create-a-task-sequence-for-non-operating-system-deployments.md).

Ab Version 2002 können Sie komplexe Anwendungen mithilfe von Tasksequenzen über das Anwendungsmodell installieren. Fügen Sie einer App einen Bereitstellungstyp hinzu, der eine Tasksequenz ist, um die App entweder zu installieren oder zu deinstallieren. Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Nächste Schritte

[Deploy the task sequence (Bereitstellen der Tasksequenz)](deploy-a-task-sequence.md)
