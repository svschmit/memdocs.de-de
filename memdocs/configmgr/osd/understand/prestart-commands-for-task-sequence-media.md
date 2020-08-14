---
title: Prestart-Befehle für Tasksequenzmedien
titleSuffix: Configuration Manager
description: Erstellen Sie ein Skript zur Verwendung für den Prestart-Befehl, verteilen Sie die zugeordneten Inhalte mit dem Prestart-Befehl, und konfigurieren Sie den Prestart-Befehl in den Medien.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 06c96d668d3c37b107ae8e290ebcd124e8a2b773
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124379"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Prestart-Befehle für Tasksequenzmedien in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können in Configuration Manager einen Prestart-Befehl zur Verwendung mit Startmedien, eigenständigen Medien und vorab bereitgestellten Medien erstellen. Der Prestart-Befehl ist ein Skript oder eine ausführbare Datei, das bzw. die ausgeführt wird, bevor die Tasksequenz ausgewählt wird, und mit dem Benutzer unter Windows PE interagieren kann. Über den Prestart-Befehl können Benutzer zur Eingabe von Informationen aufgefordert werden, die dann in der Tasksequenzumgebung gespeichert werden, oder es können Informationen von einer Tasksequenzvariablen abgefragt werden. Beim Starten des Zielcomputers wird der Befehl in der Befehlszeile ausgeführt, bevor die Richtlinie vom Verwaltungspunkt heruntergeladen wird. Verwenden Sie die folgenden Verfahren, um ein Skript für den Prestart-Befehl zu erstellen, die zugeordneten Inhalte mit dem Prestart-Befehl zu verteilen und den Prestart-Befehl in den Medien zu konfigurieren.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Erstellen einer Skriptdatei für den Prestart-Befehl  
 Tasksequenzvariablen können während der Ausführung der Tasksequenz mithilfe des COM-Objekts "Microsoft.SMS.TSEnvironment" gelesen und geschrieben werden. Im folgenden Beispiel sehen Sie eine Visual Basic-Skriptdatei, mit der die Tasksequenzvariable _SMSTSLogPath nach dem aktuellen Protokollpfad abgefragt wird. Das Skript legt außerdem eine benutzerdefinierte Variable fest.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Erstellen eines Pakets für die Skriptdatei und Verteilen des Inhalts  
 Nach dem Erstellen des Skripts oder der ausführbaren Datei für den Prestart-Befehl müssen Sie eine Paketquelle zum Hosten der Dateien für das Skript oder die ausführbare Datei erstellen, ein Paket für die Dateien erstellen (kein Programm erforderlich) und den Inhalt dann an einen Verteilungspunkt verteilen.  

 Weitere Informationen zum Erstellen eines Pakets finden Sie unter [Pakete und Programme](../../apps/deploy-use/packages-and-programs.md).  

 Weitere Informationen zum Verteilen von Inhalten finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Konfigurieren des Prestart-Befehls in Medien  
 Sie können im Assistenten zum Erstellen von Tasksequenzmedien einen Prestart-Befehl für eigenständige Medien, startbare Medien oder vorab bereitgestellte Medien konfigurieren. Weitere Informationen zu den Medientypen finden Sie unter [Create task sequence media (Erstellen von Tasksequenzmedien)](../deploy-use/create-task-sequence-media.md). Verwenden Sie das folgende Verfahren, um in Medien einen Prestart-Befehl zu erstellen.  

#### <a name="to-create-a-prestart-command-in-media"></a>So erstellen Sie einen Prestart-Befehl in Medien  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenzmedien erstellen** , um den Assistenten zum Erstellen von Tasksequenzmedien zu starten.  

4.  Wählen Sie auf der Seite **Medientyp wählen** die Option **Eigenständige Medien**, **Startbare Medien**oder **Vorab bereitgestellte Medien**aus, und klicken Sie auf **Weiter**.  

5.  Navigieren Sie zur Seite **Anpassung** des Assistenten. Weitere Informationen zum Konfigurieren der anderen Seiten im Assistenten finden Sie unter [Create task sequence media (Erstellen von Tasksequenzmedien)](../deploy-use/create-task-sequence-media.md).  

6.  Geben Sie auf der Seite **Anpassung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Wählen Sie **Prestart-Befehl aktivieren**.  

    -   Geben Sie im Textfeld **Befehlszeile** das Skript oder die ausführbare Datei ein, das bzw. die Sie für den Prestart-Befehl erstellt haben.  

        > [!IMPORTANT]  
        >  Verwenden Sie **cmd /C <Prestart-Befehl\>** , um den Prestart-Befehl anzugeben. Wenn Sie z. B. "TSScript.vbs" als Namen für das Skript des Prestart-Befehls verwendet haben, geben Sie **cmd /C TSScript.vbs** in die Befehlszeile ein. Mit **cmd /C** wird ein neues Fenster für den Windows-Befehlsinterpreter geöffnet und mithilfe der Path-Umgebungsvariablen nach dem Skript oder der ausführbaren Datei des Prestart-Befehls gesucht. Sie können auch den vollständigen Pfad zum Prestart-Befehl angeben. Achten Sie dabei darauf, dass der Laufwerkbuchstabe auf Computern mit abweichender Laufwerkkonfiguration anders lauten kann.  

    -   Wählen Sie **Dateien für den Prestart-Befehl einbeziehen**.  

    -   Klicken Sie auf **Festlegen** , um das Paket auszuwählen, das den Prestart-Befehlsdateien zugeordnet ist.  

    -   Klicken Sie auf **Durchsuchen** , um den Verteilungspunkt auszuwählen, der den Inhalt für den Prestart-Befehl hostet.  

7.  Schließen Sie den Assistenten ab.  
