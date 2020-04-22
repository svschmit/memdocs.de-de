---
title: Installieren über die Befehlszeile
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie das Configuration Manager-Setup über eine Eingabeaufforderung für eine Vielzahl von Standortinstallationen ausführen.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700398"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Verwenden einer Befehlszeile zum Installieren von Configuration Manager-Standorten

*Gilt für: Configuration Manager (Current Branch)*

 Sie können das Configuration Manager-Setup über eine Eingabeaufforderung für die Installation einer Vielzahl von Standorttypen ausführen.

## <a name="supported-tasks-for-command-line-installations"></a>Unterstützte Tasks für Befehlszeileninstallationen
 Diese Methode zum Ausführen des Setups unterstützt die folgenden Standortinstallations- und Standortwartungstasks:

- **Installieren Sie einen Standort der zentralen Verwaltung oder einen primären Standort über eine Eingabeaufforderung**  
  Anzeigen von [Befehlszeilenoptionen für Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Ändern Sie die an einem Standort der zentralen Verwaltung oder einem primären Standort verwendeten Sprachen**  
   Um die an einem Standort installierten Sprachen über die Eingabeaufforderung zu ändern (einschließlich Sprachen für Mobilgeräte), verfahren Sie wie folgt:  

  - Führen Sie das Setup im Ordner **&lt;ConfigMgrInstallationPath\>\Bin\X64** auf dem Standortserver aus,
  - Verwenden Sie die Befehlszeilenoption **/MANAGELANGS**,
  - Geben Sie eine Sprachskriptdatei an, die die Sprachen bestimmt, die Sie hinzufügen oder entfernen möchten,  

    Verwenden Sie z.B. die folgende Befehlssyntax: **setupwpf.exe /MANAGELANGS &lt;Sprachskriptdatei\>**  

    Um die Sprachskriptdatei zu erstellen, verwenden Sie die Informationen unter [Befehlszeilenoptionen zum Verwalten von Sprachen](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang).  

- **Verwenden Sie eine Skriptdatei für die unbeaufsichtigte Installation oder Wiederherstellung von Standorten**  
   Sie können Setup über eine Eingabeaufforderung ausführen, indem Sie ein Installationsskript verwenden, und Sie können eine unbeaufsichtigte Standortinstallation ausführen. Sie können diese Option auch zur Wiederherstellung eines Standorts verwenden.    

   So verwenden Sie ein Skript mit Setup:  

  - Führen Sie Setup mit der Befehlszeilenoption **/SCRIPT** aus, und geben Sie eine Skriptdatei an.  

  - Die Skriptdatei muss mit den erforderlichen Schlüsseln und Werten konfiguriert werden.  

    Für eine unbeaufsichtigte Installation eines Standorts der zentralen Verwaltung oder eines primären Standorts muss die Skriptdatei die folgenden Abschnitte aufweisen:  

  - Identification    
  - Optionen    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    Zum Wiederherstellen eines Standorts müssen Sie auch die folgenden Abschnitte der Skriptdatei einbeziehen:  

  - Identification  
  - Wiederherstellung

Weitere Informationen finden Sie unter [Unbeaufsichtigte Standortwiederherstellung für Configuration Manager](../../manage/unattended-recovery.md).  

Eine Liste mit Schlüsseln und Werten, die in einer unbeaufsichtigten Installationsskriptdatei verwendet werden sollen, finden Sie unter [Skriptdateischlüssel für unbeaufsichtigtes Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Informationen zur Befehlszeilen-Skriptdatei  
 Für unbeaufsichtigte Installationen von Configuration Manager können Sie Setup mit der Befehlszeilenoption **/SCRIPT** ausführen und eine Skriptdatei angeben, die Installationsoptionen enthält. Die folgenden Aufgaben werden von dieser Methode unterstützt:  

-   Installieren eines Standorts der zentralen Verwaltung  
-   Installieren eines primären Standorts  
-   Installieren einer Configuration Manager-Konsole  
-   Wiederherstellen eines Standorts  

> [!NOTE]  
>  Sie können die Skriptdatei für die unbeaufsichtigte Installation nicht verwenden, um ein Upgrade einer Evaluierungsversion auf eine lizenzierte Version von Configuration Manager auszuführen.  

### <a name="the-cdlatest-key-name"></a>Der Schlüsselname „CDLatest“
Wenn Sie Medien aus dem Ordner „CD.Latest“ verwenden, um eine Skriptinstallation der folgenden vier Installationsoptionen auszuführen, muss Ihr Skript den Schlüssel **CDLatest** mit einem Wert von **1** enthalten:
- Installieren eines neuen Standorts der zentralen Verwaltung
- Installieren eines neuen primären Standorts
- Wiederherstellen eines Standorts der zentralen Verwaltung
- Wiederherstellen eines primäre Standorts

Dieser Wert wird nicht für das Verwenden mit Installationsmedien unterstützt, die Sie von der Microsoft Volume License-Website erhalten.
Weitere Informationen zum Verwenden dieses Schlüsselnamens in der Skriptdatei finden Sie unter [Befehlszeilenoptionen](command-line-options-for-setup.md).



### <a name="create-the-script"></a>Erstellen des Skripts
Das Installationsskript wird automatisch erstellt, wenn Sie das [Setup ausführen, um einen Standort über die Benutzeroberfläche](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) zu installieren.  Wenn Sie die Einstellungen auf der Seite **Zusammenfassung** des Assistenten bestätigen, geschieht Folgendes:  

-   Setup erstellt das Skript **%TEMP%\ConfigMgrAutoSave.ini**.  Sie können diese Datei vor dem Verwenden umbenennen, müssen aber die Dateierweiterung „.ini“ beibehalten.  
-   Das Skript für die unbeaufsichtigte Installation enthält die Einstellungen, die Sie im Assistenten ausgewählt haben.  
-   Nach der Erstellung des Skripts können Sie es ändern, um andere Standorte in Ihrer Hierarchie zu installieren.  
-   Anschließend können Sie das Skript verwenden, um eine unbeaufsichtigte Installation von Configuration Manager durchzuführen.  

Mit der Skriptdatei werden die gleichen Informationen bereitgestellt, die vom Setup-Assistenten angefordert werden. Das Skript enthält jedoch keine Standardeinstellungen.   
Alle Werte müssen für die Setup-Schlüssel angegeben werden, die für den jeweils verwendeten Installationstyp gelten.   

Bei der Erstellung des Skripts für die unbeaufsichtigte Installation durch Setup wird dort der Wert für den Product Key eingetragen, den Sie während des Setups eingegeben haben. Dies kann ein gültiger Product Key oder **EVAL** sein, wenn Sie eine Evaluierungsversion von Configuration Manager installieren. Der Product Key-Wert im Skript wird eingetragen, damit die Voraussetzungsprüfung abgeschlossen werden kann.   

Wenn von Setup die Installation des tatsächlichen Standorts gestartet wird, wird erneut in das automatisch erstellte Skript geschrieben, um den Product Key-Wert im erstellten Skript zu löschen. Bevor Sie das Skript für die unbeaufsichtigte Installation eines neuen Standorts verwenden, können Sie es bearbeiten und einen gültigen Product Key eingeben oder eine Evaluierungsinstallation von Configuration Manager angeben.  

### <a name="section-names-key-names-and-values"></a>Abschnittsnamen, Schlüsselnamen und Werte
Das Skript enthält Abschnittsnamen, Schlüsselnamen und Werte. Beachten Sie die folgenden Informationen:
-   Welche Abschnitts- und Schlüsselnamen erforderlich sind, hängt von der Installationsart ab, für die Sie das Skript erstellen.
-   Die Reihenfolge der Schlüssel in den Abschnitten und die Reihenfolge der Abschnitte in der Datei spielen keine Rolle.     
-   Bei Schlüsseln wird die Groß-/Kleinschreibung nicht beachtet.  
-   Wenn Sie Werte für Schlüssel angeben, müssen dem Namen des Schlüssels ein Gleichheitszeichen (=) und der Wert für den Schlüssel folgen.    

> [!TIP]  
>  Eine vollständige Übersicht über die Optionen finden Sie unter [Befehlszeilenoptionen für Setup und Skripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>So verwenden Sie die Setup-Befehlszeilenoption /SCRIPT

-   Sie müssen eine Setupskriptdatei verwenden und den Namen der Datei nach der Setup-Befehlszeilenoption **/SCRIPT** angeben. Beachten Sie die folgenden Informationen:   
    -   Der Name der Datei muss die Dateinamenerweiterung **.ini** aufweisen.  
    -   Wenn Sie an der Eingabeaufforderung auf die Setupskriptdatei verweisen, muss der vollständige Dateipfad angegeben werden. Wenn die Setup-Initialisierungsdatei beispielsweise „Setup.ini“ heißt und sich im Ordner „C:\Setup“ befindet, geben Sie an der Eingabeaufforderung Folgendes ein:  **setup /script c:\setup\setup.ini**.  

-   Das Konto für die Ausführung von Setup benötigt **Administrator**rechte auf dem Computer. Wenn Sie Setup mit dem Skript für die unbeaufsichtigte Installation ausführen, öffnen Sie das Eingabeaufforderungsfenster mit der Option **Als Administrator ausführen**.   
