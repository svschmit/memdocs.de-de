---
title: Verwenden von Tasksequenzvariablen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Variablen in einer Configuration Manager-Tasksequenz verwenden.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1cf428b479e9311c92f6d14d9c376817ee5e3ab5
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022261"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Verwenden von Tasksequenzvariablen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

 Die Tasksequenz-Engine in der Betriebssystembereitstellung von Configuration Manager verwendet viele Variable, um das Verhalten zu steuern. Diese Variablen bieten die folgenden Möglichkeiten:

- Festlegen von Bedingungen für Schritte  
- Ändern des Verhaltens für bestimmte Schritte  
- Verwenden in Skripts für komplexere Aktionen  

Eine Referenz für alle verfügbaren Tasksequenzvariablen finden Sie unter [Tasksequenzvariablen](task-sequence-variables.md).

## <a name="types-of-variables"></a><a name="bkmk_types"></a> Variablentypen

Es gibt unterschiedliche Typen von Variablen:  

- [Integriert](#bkmk_built-in)  
- [Aktion](#bkmk_action)  
- [Benutzerdefiniert](#bkmk_custom)  
- [Schreibgeschützt](#bkmk_read-only)  
- [Array](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> Integrierte Variablen

Integrierte Variable liefern Informationen zu der Umgebung, in der die Tasksequenz ausgeführt wird. Ihre Werte sind in der gesamten Tasksequenz verfügbar. In der Regel initialisiert die Tasksequenz-Engine integrierte Variable, bevor Schritte ausgeführt wird.

Beispiel: `_SMSTSLogPath` ist eine Umgebungsvariable, die den Pfad angibt, in den Configuration Manager-Komponenten Protokolldateien schreiben. Auf diese Umgebungsvariable kann von jedem Tasksequenzschritt aus zugegriffen werden.

Die Tasksequenz wertet vor jedem Schritt einige Variablen aus. `_SMSTSCurrentActionName` listet beispielsweise den Namen des aktuellen Schritts auf.

### <a name="action-variables"></a><a name="bkmk_action"></a> Aktionsvariablen

Tasksequenz-Aktionsvariablen geben Konfigurationseinstellungen an, die ein einzelner Tasksequenzschritt verwendet. Standardmäßig initialisiert der Schritt die Einstellungen vor der Ausführung. Dabei sind diese Einstellungen nur verfügbar, solange der zugehörige Tasksequenzschritt ausgeführt wird. Die Tasksequenz fügt den Aktionsvariablenwert der Umgebung hinzu, bevor der Schritt ausgeführt wird. Nachdem der Schritt ausgeführt wurde, wird der Wert aus der Umgebung entfernt.

Beispiel: Sie fügen den Schritt **Befehlszeile ausführen** einer Tasksequenz hinzu. Dieser Schritt enthält eine **Starten In**-Eigenschaft. Die Tasksequenz speichert einen Standardwert für diese Eigenschaft als `WorkingDirectory`-Variable. Die Tasksequenz initialisiert diesen Wert, bevor der Schritt **Befehlszeile ausführen** ausgeführt wird. Greifen Sie während der Schrittausführung auf den **Starten In**-Eigenschaftswert über den `WorkingDirectory`-Wert zu. Nach dem Schritt wird der Wert der Variablen `WorkingDirectory` aus der Umgebung entfernt. Wenn die Tasksequenz einen weiteren Schritt **Befehlszeile ausführen** enthält, wird eine neue `WorkingDirectory`-Variable initialisiert. Zu diesem Zeitpunkt legt die Tasksequenz die Variable auf den Startwert des aktuellen Schritts fest. Weitere Informationen finden Sie unter [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

Der *Standardwert* für eine Aktionsvariable ist vorhanden, wenn der Schritt ausgeführt wird. Wenn Sie einen *neuen Wert* festlegen, ist dieser für mehrere Tasksequenzschritte verfügbar. Wenn Sie einen Standardwert überschreiben, bleibt der neue Wert in der Umgebung. Dieser neue Wert überschreibt den Standardwert für andere Tasksequenzschritte. Beispiel: Sie fügen den Schritt **Tasksequenzvariable festlegen** als ersten Schritt der Tasksequenz hinzu. Dieser Schritt legt die `WorkingDirectory`-Variable auf `C:\` fest. Alle Schritte **Befehlszeile ausführen** in der Tasksequenz verwenden den neuen Startverzeichniswert.  

Einige Tasksequenzschritte kennzeichnen bestimmte Aktionsvariablen als *Ausgabe*. Nachfolgende Schritte in der Tasksequenz lesen diese Ausgabevariablen.

> [!Note]  
> Nicht alle Tasksequenzschritte verfügen über Aktionsvariablen. Beispielsweise gibt es zwar Variablen, die der Aktion **BitLocker aktivieren** zugeordnet sind, jedoch keine Variablen, die der Aktion **BitLocker deaktivieren** zugeordnet sind.  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> Benutzerdefinierte Variablen

Hierzu zählen alle Variablen, die nicht von Configuration Manager erstellt wurden. Initialisieren Sie Ihre eigenen Variablen, um sie als Bedingungen, in Befehlszeilen oder in Skripts zu verwenden.

Wenn Sie einen Namen für eine neue Tasksequenzvariable angeben, beachten Sie Folgendes:  

- Buchstaben, Ziffern, Unterstriche (`_`) und Bindestriche (`-`) sind zulässig.  

- Die Namenslänge darf 1 bis 256 Zeichen umfassen.  

- Benutzerdefinierte Variable müssen mit einem Buchstaben (`A-Z` oder `a-z`) beginnen.  

- Benutzerdefinierte Variablennamen dürfen nicht mit einem Unterstrich beginnen. Nur schreibgeschützte Tasksequenzvariablen beginnen mit dem Unterstrich.  

- Die Groß-/Kleinschreibung wird nicht berücksichtigt. Beispiel: `OSDVAR` und `osdvar` entsprechen derselben Tasksequenzvariablen.  

- Namen dürfen nicht mit einem Leerzeichen beginnen oder enden. Sie dürfen generell kein Leerzeichen enthalten. Die Tasksequenz ignoriert Leerzeichen am Anfang oder Ende des Namens.  

Sie können beliebig viele Tasksequenzvariable erstellen. Die Anzahl der Variablen wird jedoch durch die Größe der Tasksequenzumgebung beschränkt. Die Beschränkung der Gesamtgröße für die Tasksequenzumgebung beträgt 32 MB.  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> Schreibgeschützte Variablen

Sie können den Wert einiger Variablen, die schreibgeschützt sind, nicht ändern. In der Regel beginnt der Name mit einem Unterstrich (`_`). Die Tasksequenz verwendet sie für ihre Vorgänge. Schreibgeschützte Variable sind in der Tasksequenzumgebung sichtbar.

Diese Variablen sind nützlich in Skripts und Befehlszeilen. Beispiel: Sie möchten eine Befehlszeile ausführen und die Ausgabe an eine Protokolldatei in `_SMSTSLogPath` mit anderen Protokolldateien weiterreichen.

> [!NOTE]  
> Schreibgeschützte Tasksequenzvariable können von Tasksequenzschritten gelesen, jedoch nicht festgelegt werden. Verwenden Sie schreibgeschützte Variable beispielsweise als Teil der Befehlszeile für den Schritt **Befehlszeile ausführen**. Sie können schreibgeschützte Variable nicht mit dem Schritt **Tasksequenzvariable festlegen** bestimmen.  

### <a name="array-variables"></a><a name="bkmk_array"></a> Arrayvariablen

Die Tasksequenz speichert einige Variablen als Array. Jedes Element im Array stellt die Einstellungen für ein einzelnes Objekt dar. Verwenden Sie diese Variablen, wenn für ein Gerät mehr als ein Objekt konfiguriert werden soll. Die folgenden Tasksequenzschritte verwenden Arrayvariablen:

- [Netzwerkeinstellungen anwenden](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> Festlegen von Variablen

Für benutzerdefinierte nicht schreibgeschützte Variable gibt es mehrere Methoden, um den Variablenwert zu initialisieren und festzulegen:  

- Schritt [Tasksequenzvariable festlegen](#bkmk_set-ts-step)
- Schritt [Dynamische Variablen festlegen](#bkmk_set-dyn-step)
- Schritt [PowerShell-Skript ausführen](#bkmk_run-ps)
- [Sammlungs- und Gerätevariablen](#bkmk_set-coll-var)  
- [TSEnvironment-COM-Objekt](#bkmk_set-com)  
- [Prestart-Befehl](#bkmk_set-prestart)  
- [Tasksequenz-Assistent](#bkmk_set-tswiz)
- [Tasksequenzmedien-Assistent](#bkmk_set-media)  

Löschen Sie eine Variable aus der Umgebung, indem Sie die gleichen Methoden wie beim Erstellen von Variablen verwenden. Um eine Variable zu löschen, legen Sie den Variablenwert auf eine leere Zeichenfolge fest.  

Sie können Methoden kombinieren, um eine Tasksequenzvariable auf verschiedene Werte für die gleiche Sequenz festzulegen. Legen Sie beispielsweise die Standardwerte mit dem Tasksequenz-Editor fest, und bestimmen Sie dann benutzerdefinierte Werte mit einem Skript.

Wenn Sie die gleiche Variable mit verschiedenen Methoden festlegen, folgt die Tasksequenz-Engine der folgenden Reihenfolge:  

1. Zuerst werden Sammlungsvariablen ausgewertet.  

2. Gerätespezifische Variable überschreiben dieselbe Variable, die von einer Sammlung festgelegt wurde.  

3. Variablen, die von einer beliebigen Methode während der Tasksequenz festgelegt wurden, haben Vorrang vor Sammlungs- bzw. Gerätevariablen.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Allgemeine Einschränkungen für Variablenwerte von Tasksequenzen

- Die Werte dürfen 4.000 Zeichen nicht überschreiten.  

- Eine schreibgeschützte Tasksequenzvariable kann nicht geändert werden. Die Namen von schreibgeschützten Variablen beginnen mit einem Unterstrich (`_`).  

- Je nach Einsatz des Werts muss die Groß-/Kleinschreibung berücksichtigt werden. In der Regel ist die Groß-/Kleinschreibung nicht relevant. Bei einer Variablen, die ein Kennwort enthält, muss jedoch zwischen Groß-/Kleinschreibung unterschieden werden.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a> Tasksequenzvariable festlegen

Verwenden Sie diesen Schritt in der Tasksequenz, um eine einzelne Variable auf einen einzelnen Wert festzulegen.

Weitere Informationen finden Sie unter [Tasksequenzvariable festlegen](task-sequence-steps.md#BKMK_SetTaskSequenceVariable).

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a> Dynamische Variablen festlegen

Verwenden Sie diesen Schritt in der Tasksequenz, um mindestens eine Tasksequenzvariable festzulegen. In diesem Schritt definieren Sie Regeln, mit denen Sie festlegen, welche Variablen und Werte verwendet werden.

Weitere Informationen finden Sie unter [Dynamische Variablen festlegen](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a> PowerShell-Skript ausführen

<!-- 6315548 -->

Verwenden Sie diesen Schritt in der Tasksequenz, um mithilfe eines PowerShell-Skripts eine Tasksequenzvariable festzulegen.

Sie können in diesem Schritt einen Skriptnamen aus einem Paket angeben oder direkt ein PowerShell-Skript eingeben. Verwenden Sie dann die Schritteigenschaft für die **Ausgabe an Tasksequenzvariable**, um die Skriptausgabe in einer benutzerdefinierten Tasksequenzvariablen zu speichern.

Weitere Informationen zu diesem Schritt finden Sie unter [PowerShell-Skript ausführen](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> Sie können auch ein PowerShell-Skript verwenden, um eine oder mehrere Variablen mit dem **TSEnvironment**-Objekt festzulegen. Weitere Informationen finden Sie im Configuration Manager SDK unter [Verwenden von Variablen in einer ausgeführten Tasksequenz](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).

#### <a name="example-scenario-with-run-powershell-script-step"></a>Beispielszenario mit dem Schritt „PowerShell-Skript ausführen“

Ihre Umgebung enthält Benutzer in mehreren Ländern oder Regionen, daher sollten Sie die Betriebssystemsprache abfragen, um diese als Bedingung für mehrere sprachspezifische **Betriebssystem anwenden**-Schritte festzulegen.

1. Fügen Sie der Tasksequenz vor den **Betriebssystem anwenden**-Schritten eine Instanz des Schritts **PowerShell-Skript ausführen** hinzu.

1. Verwenden Sie die Option **PowerShell-Skript angeben**, um den folgenden Befehl festzulegen:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Weitere Informationen zum Cmdlet finden Sie unter [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture). Weitere Informationen zu den zweibuchstabigen ISO-Sprachnamen finden Sie in der [Liste der ISO-639-1-Codes](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. Für die Option **Ausgabe an Tasksequenzvariable** legen Sie `CurrentOSLanguage` fest.

    ![Screenshot des Beispielschritts „PowerShell-Skript ausführen“](media/run-powershell-script-example-language.png)

1. Erstellen Sie im Schritt **Betriebssystem anwenden** für das Image in englischer Sprache die folgende Bedingung: `Task Sequence Variable CurrentOSLanguage equals "en"`.

    ![Screenshot der Beispielbedingung im Schritt „Betriebssystem anwenden“](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Weitere Informationen zum Erstellen einer Bedingung in einem Schritt finden Sie unter [Zugreifen auf Variablen – Bedingung für einen Schritt](#bkmk_access-condition).

1. Speichern Sie die Tasksequenz, und stellen Sie sie bereit.

Wenn der Schritt **PowerShell-Skript ausführen** auf einem Gerät mit der englischen Sprachversion von Windows ausgeführt wird, gibt der Befehl den Wert `en` zurück. Dann wird dieser Wert in der benutzerdefinierten Variable gespeichert. Wenn der Schritt **Betriebssystem anwenden** für das englischsprachige Image auf demselben Gerät ausgeführt wird, wird die Bedingung als TRUE ausgewertet. Wenn Sie mehrere Instanzen des Schritts **Betriebssystem anwenden** für verschiedene Sprachen erstellt haben, führt die Tasksequenz dynamisch den Schritt aus, der mit der Betriebssystemsprache übereinstimmt.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> Sammlungs- und Gerätevariablen

Sie können benutzerdefinierte Tasksequenzvariablen für Geräte und Sammlungen definieren. Für ein Gerät definierte Variablen werden als gerätespezifische Tasksequenzvariablen bezeichnet. Für eine Sammlung definierte Variablen werden als sammlungsspezifische Tasksequenzvariablen bezeichnet. Bei einem Konflikt haben gerätespezifische Variablen Vorrang vor sammlungsspezifischen Variablen. Dieses Verhalten ist darauf zurückzuführen, dass einem bestimmten Gerät zugewiesene Tasksequenzvariablen automatisch eine höhere Priorität als Variablen haben, die der Sammlung mit dem Gerät zugewiesen wurden.  

Beispiel: Das Gerät „XYZ“ ist ein Mitglied der Sammlung „ABC“. Sie weisen MyVariable der Sammlung „ABC“ mit dem Wert „1“ zu. Darüber hinaus weisen Sie MyVariable dem Gerät „XYZ“ mit dem Wert „2“ zu. Die Variable, die „XYZ“ zugewiesen ist, hat eine höhere Priorität als die Variable, die der Sammlung „ABC“ zugewiesen ist. Wenn eine Tasksequenz mit dieser Variable auf „XYZ“ ausgeführt wird, weist MyVariable den Wert „2“ auf.

Sie können gerätespezifische und sammlungsspezifische Variablen ausblenden, damit sie in der Configuration Manager-Konsole nicht sichtbar sind. Bei Verwendung der Option **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen** wird der Wert der Variable in der Konsole nicht angezeigt. Die Variable kann allerdings weiterhin von der Tasksequenz während der Ausführung verwendet werden. Wenn diese Variablen nicht mehr ausgeblendet sein sollen, löschen Sie diese zuerst. Definieren Sie dann erneut die Variablen, und lassen Sie die Option zum Ausblenden dieser Variablen dieses Mal deaktiviert.  

> [!WARNING]  
> Die Einstellung **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen** ist nur für die Configuration Manager-Konsole gültig. Die Werte für die Variablen werden weiterhin in der Tasksequenz-Protokolldatei (**smsts.log**) angezeigt.

Sie können gerätespezifische Variablen an einem primären Standort oder an einem Standort der zentralen Verwaltung verwalten. Configuration Manager unterstützt je Gerät maximal 1.000 zugewiesene Variablen.  

> [!IMPORTANT]  
> Bei der Verwendung sammlungsspezifischer Variablen für Tasksequenzen sind folgende Verhalten zu beachten:  
>
> - Änderungen an Sammlungen werden immer in der gesamten Hierarchie repliziert. Änderungen, die Sie an Sammlungsvariablen vornehmen, gelten nicht nur für die Mitglieder des aktuellen Standorts, sondern für alle Mitglieder der Sammlung in der gesamten Hierarchie.  
>  
> - Wenn Sie eine Sammlung löschen, werden auch die Tasksequenzvariablen gelöscht, die für die Sammlung konfiguriert sind.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Erstellen von Tasksequenzvariablen für ein *Gerät*

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Geräte** aus.  

2. Wählen Sie das Zielgerät und dann **Eigenschaften** aus.  

3. Wechseln Sie im Dialogfeld **Eigenschaften** zur Registerkarte **Variablen**.  

4. Wählen Sie für jede Variable, die erstellt werden soll, das Symbol **Neu** aus. Geben Sie den **Namen** und den **Wert** der Tasksequenzvariable an. Wenn Sie die Variable ausblenden möchten, damit sie in der Configuration Manager-Konsole nicht sichtbar ist, heben Sie die Auswahl für die Option **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen** auf.  

5. Wählen Sie **OK** aus, nachdem Sie den Geräteeigenschaften alle Variablen hinzugefügt haben.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Erstellen von Tasksequenzvariablen für eine *Sammlung*

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus. Wählen Sie die Zielsammlung und dann **Eigenschaften** aus.  

2. Wechseln Sie im Dialogfeld **Eigenschaften** zur Registerkarte **Sammlungsvariablen**.  

3. Wählen Sie für jede Variable, die erstellt werden soll, das Symbol **Neu** aus. Geben Sie den **Namen** und den **Wert** der Tasksequenzvariable an. Wenn Sie die Variable ausblenden möchten, damit sie in der Configuration Manager-Konsole nicht sichtbar ist, heben Sie die Auswahl für die Option **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen** auf.  

4. Geben Sie optional die Priorität an, die bei der Auswertung der Tasksequenzvariablen durch Configuration Manager gelten soll.  

5. Wählen Sie **OK** aus, nachdem Sie den Sammlungseigenschaften alle Variablen hinzugefügt haben.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> TSEnvironment-COM-Objekt

Verwenden Sie das **TSEnvironment**-Objekt, um mit Variablen aus einem Skript zu arbeiten.

Weitere Informationen finden Sie im Configuration Manager SDK unter [Verwenden von Variablen in einer ausgeführten Tasksequenz](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> Prestart-Befehl

Der Prestart-Befehl ist ein Skript oder eine ausführbare Datei, die in Windows PE ausgeführt wird, bevor der Benutzer die Tasksequenz auswählt. Der Prestart-Befehl kann eine Variable abfragen oder den Benutzer zur Eingabe von Informationen auffordern, die dann in der Umgebung gespeichert werden. Verwenden Sie das [TSEnvironment](#bkmk_set-com)-COM-Objekt, um Lese- und Schreibvorgänge für eine Variable aus dem Prestart-Befehl auszuführen.

Weitere Informationen finden Sie unter [Prestart-Befehle für Tasksequenzmedien](prestart-commands-for-task-sequence-media.md).

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> Tasksequenz-Assistent

Ab Version 1906: Nachdem Sie eine Tasksequenz im Tasksequenzerstellungs-Assistenten-Fenster ausgewählt haben, enthält die Seite zum Bearbeiten von Tasksequenzvariablen die Schaltfläche **Bearbeiten**. Sie können Tastenkombinationen zum Bearbeiten der Variablen verwenden. Diese Änderung ist hilfreich in Fällen, in denen die Maus nicht verfügbar ist.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> Tasksequenzmedien-Assistent

Geben Sie Variablen für Tasksequenzen an, die von Medien ausgeführt werden. Wenn Sie das Betriebssystem mit Medien bereitstellen, fügen Sie die Tasksequenzvariablen hinzu, und geben Sie ihre Werte an, wenn Sie die Medien erstellen. Die Variablen und ihre Werte werden auf den Medien gespeichert.  

> [!NOTE]  
> Tasksequenzen werden auf eigenständigen Medien gespeichert. Allerdings wird die Tasksequenz von allen anderen Medientypen, wie beispielsweise vorab bereitgestellten Medien, von einem Verwaltungspunkt abgerufen.  

Wenn Sie eine Tasksequenz über Medien ausführen, können Sie eine Variable auf der Seite **Anpassung** des Assistenten hinzufügen.

Verwenden Sie die Medienvariablen anstelle der sammlungs- bzw. computerspezifischen Variablen. Computer- und sammlungsspezifische Variablen treffen nicht zu und werden nicht verwendet, wenn die Tasksequenz über Medien ausgeführt wird.  

> [!TIP]  
> Die Tasksequenz schreibt die Paket-ID und die Prestart-Befehlszeile in die Datei **CreateTSMedia.log** auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird. Diese Protokolldatei enthält den Wert für alle Tasksequenzvariablen. Anhand dieser Protokolldatei können Sie den Wert für die Tasksequenzvariablen überprüfen.  

Weitere Informationen finden Sie unter [Erstellen von Tasksequenzmedien](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> Zugreifen auf Variablen

Sie können die Variable in Tasksequenzen verwenden, nachdem Sie sie und ihren Wert mithilfe einer der Methoden aus dem vorherigen Abschnitt angegeben haben. Sie können beispielsweise auf Standardwerte für integrierte Tasksequenzvariable zugreifen oder einen Schritt von einem Variablenwert abhängig machen.  

Verwenden Sie die folgenden Methoden, um in der Tasksequenzumgebung auf Variablenwerte zuzugreifen:

- [Verwenden in einem Schritt](#bkmk_access-step)  
- [Bedingung für einen Schritt](#bkmk_access-condition)  
- [Benutzerdefiniertes Skript](#bkmk_access-script)  
- [Windows-Setupantwortdatei](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> Verwenden in einem Schritt

Geben Sie einen Variablenwert für eine Einstellung in einem Tasksequenzschritt an. Bearbeiten Sie den Schritt im Tasksequenz-Editor, und geben Sie den Variablennamen als Feldwert an. Schließen Sie den Variablennamen in Prozentzeichen (`%`) ein.

Verwenden Sie beispielsweise den Variablennamen als Teil des Felds **Befehlszeile** in Schritt **Befehlszeile ausführen**. Die folgende Befehlszeile schreibt den Computernamen in eine Textdatei.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> Bedingung für einen Schritt

Verwenden Sie integrierte oder benutzerdefinierte Tasksequenzvariable als Teil einer Bedingung für einen Schritt oder eine Gruppe. Die Tasksequenz wertet den Variablenwert aus, bevor der Schritt bzw. die Gruppe ausgeführt wird.

Gehen Sie wie folgt vor, um eine Bedingung hinzuzufügen, die einen Variablenwert auswertet:  

1. Wählen Sie im Tasksequenz-Editor den Schritt bzw. die Gruppe aus, der Sie die Bedingung hinzufügen möchten.  

2. Wechseln Sie zur Registerkarte **Optionen** für den Schritt oder die Gruppe. Klicken Sie auf **Bedingung hinzufügen**, und wählen Sie **Tasksequenzvariable** aus.  

3. Legen Sie im Dialogfeld **Tasksequenzvariable** die folgenden Einstellungen fest:  

    - **Variable:** der Name der Variablen. Beispiel: `_SMSTSInWinPE`.  

    - **Bedingung:** die Bedingung zum Auswerten des Variablenwerts. Beispiel: **gleich**.  

    - **Wert:** der Wert der zu überprüfenden Variablen. Beispiel: `false`.  

Die drei oben genannten Beispiele bilden eine allgemeine Bedingung, um zu testen, ob die Tasksequenz von einem Startimage in Windows PE aus ausgeführt wird:

> **Tasksequenzvariable** `_SMSTSInWinPE equals "false"`

Sie finden diese Bedingung in der Gruppe **Dateien und Einstellungen erfassen** der Tasksequenz-Standardvorlage, um ein vorhandenes Betriebssystemimage zu installieren.

Weitere Informationen zu Bedingungen finden Sie unter [Tasksequenz-Editor – Bedingungen](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a> Benutzerdefiniertes Skript

Variablen können beim Ausführen der Tasksequenz mithilfe des COM-Objekts **Microsoft.SMS.TSEnvironment** gelesen und geschrieben werden.

Das folgende Windows PowerShell-Beispiel fragt die Variable **_SMSTSLogPath** ab, um den aktuellen Protokollspeicherort abzurufen. Das Skript legt außerdem eine benutzerdefinierte Variable fest.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> Windows Setup-Antwortdatei

Die von Ihnen bereitgestellte Windows-Setupantwortdatei kann eingebettete Tasksequenzvariablen enthalten. Verwenden Sie das Format `%varname%`, wobei *varname* dem Namen der Variablen entspricht. Der Schritt **Windows und ConfigMgr einrichten** ersetzt die Zeichenfolge des Variablennamens durch den tatsächlichen Variablenwert. Diese eingebetteten Tasksequenzvariablen können nicht in rein numerischen Feldern in einer „unattend.xml“-Antwortdatei verwendet werden.

Weitere Informationen finden Sie unter [Windows und ConfigMgr einrichten](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Weitere Informationen:

- [Tasksequenzschritte](task-sequence-steps.md)

- [Tasksequenzvariablen](task-sequence-variables.md)

- [Planungsüberlegungen für das Automatisieren von Tasks](../plan-design/planning-considerations-for-automating-tasks.md)

- [Tasksequenz-Editor](task-sequence-editor.md)
