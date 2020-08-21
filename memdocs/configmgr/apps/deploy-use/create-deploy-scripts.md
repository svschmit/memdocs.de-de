---
title: Erstellen und Ausführen von Skripts
titleSuffix: Configuration Manager
description: Erfahren Sie, wie PowerShell-Skripts erstellt und auf Clientgeräten ausgeführt werden.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db3a673d99efc40bd6fa0da7930c66c648136e03
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695357"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole

*Gilt für: Configuration Manager (Current Branch)*

<!--1236459-->
Configuration Manager verfügt über eine integrierte Funktion zum Ausführen von PowerShell-Skripts. PowerShell bietet den Vorteil der Erstellung ausgeklügelter, automatisierter Skripts, die von einer größeren Community verstanden und geteilt werden. Die Skripts vereinfachen die Erstellung benutzerdefinierter Tools zur Verwaltung von Software und ermöglichen Ihnen, alltägliche Aufgaben schnell zu erledigen, sodass Sie große Aufträge einfacher und konsistenter bewältigen können.  

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Durch diese Integration in Configuration Manager können Sie die Funktion *Skripts ausführen* für Folgendes verwenden:

- Erstellen und Bearbeiten von Skripts für die Verwendung mit Configuration Manager
- Verwalten der Skriptnutzung mithilfe von Rollen und Sicherheitsbereichen 
- Anwenden von Skripts auf Sammlungen einzelner lokal verwalteter Windows-PCs
- Abrufen schnell aggregierter Skriptergebnisse von Clientgeräten
- Überwachen der Skriptausführung und Anzeigen von Berichtsergebnissen in der Skriptausgabe

> [!WARNING]
> - Angesichts der Leistungsfähigkeit von Skripts möchten wir Sie daran erinnern, diese bewusst und sorgfältig einzusetzen. Wir haben zusätzliche Sicherheitsvorkehrungen eingebaut, um Sie zu unterstützen: getrennte Rollen und Bereiche. Stellen Sie die Fehlerfreiheit von Skripts sicher, bevor Sie sie ausführen. Bestätigen Sie außerdem, dass sie aus einer vertrauenswürdigen Quelle stammen, um eine unbeabsichtigte Ausführung von Skripts zu verhindern. Achten Sie auf Sonderzeichen oder sonstige Obfuskation, und informieren Sie sich über die Absicherung von Skripts. Unter [Learn more about PowerShell script security (Weitere Informationen zur sicheren Verwendung von PowerShell-Skripts)](learn-script-security.md) finden Sie weiterführende Hinweise.
> - Bestimmte Antischadsoftware kann unbeabsichtigt Ereignisse auslösen, die gegen die Configuration Manager-Features „Skripts ausführen“ und „CMPivot“ gerichtet sind. Es empfiehlt sich, „%windir%\CCM\ScriptStore“ auszuschließen, damit die Antischadsoftware die störungsfreie Ausführung dieser Features zulässt.

## <a name="prerequisites"></a>Voraussetzungen

- Um PowerShell-Skripts ausführen zu können, muss auf dem Client PowerShell 3.0 installiert sein. Wenn ein Skript jedoch Funktionen aus einer neueren PowerShell-Version enthält, muss diese auch auf dem Client installiert sein, der diese Version von PowerShell ausführt.
- Das Ausführen von Skripts ist nur auf Clients mit Configuration Manager 1706 oder neuer möglich.
- Um Skripts zu verwenden, müssen Sie Mitglied der entsprechenden Configuration Manager-Sicherheitsrolle sein.
- Importieren und Erstellen von Skripts: Ihr Konto benötigt die Berechtigung **Erstellen** für **SMS-Skripts**.
- Genehmigen und Ablehnen von Skripts: Ihr Konto benötigt die Berechtigung **Genehmigen** für **SMS-Skripts**.
- Ausführen von Skripts: Ihr Konto benötigt die Berechtigung **Skript ausführen** für **Sammlungen**.

Weitere Informationen zu Configuration Manager-Sicherheitsrollen finden Sie unter:</br>
[Sicherheitsbereiche für das Ausführen von Skripts](#security-scopes)</br>
[Sicherheitsrollen für das Ausführen von Skripts](#bkmk_ScriptRoles)</br>
[Grundlagen der rollenbasierten Verwaltung](../../core/understand/fundamentals-of-role-based-administration.md)

## <a name="limitations"></a>Einschränkungen

Von der Funktion „Skripts ausführen“ wird derzeit Folgendes unterstützt:

- Skriptsprachen: PowerShell
- Parametertypen: „integer“, „string“ und „list“


>[!WARNING]
>Beachten Sie, dass die Verwendung von Parametern das Risiko für PowerShell Injection-Angriffe erhöht. Es gibt verschiedene Möglichkeiten, dieses Risiko zu verringern. Sie können beispielsweise reguläre Ausdrücken zum Überprüfen der Parametereingabe oder vordefinierte Parameter verwenden. Als allgemeine bewährte Methode wird empfohlen, keine Geheimnisse wie Kennwörter in PowerShell-Skripts zu hinterlegen. Unter [Learn more about PowerShell script security (Weitere Informationen zur sicheren Verwendung von PowerShell-Skripts)](learn-script-security.md) finden Sie weiterführende Hinweise. <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Skript ausführen: Ersteller und Genehmiger

Die Funktion „Skripts ausführen“ arbeitet für die Implementierung und Ausführung eines Skripts mit dem Konzept von *Skriptautoren* und *Skriptgenehmigern* als getrennte Rollen. Die Trennung von Autor- und Genehmigerrolle ermöglicht eine wichtige Prozessüberprüfung für das überaus leistungsstarke Tool „Skripts ausführen“. Mit der zusätzlichen Rolle *Skriptausführende* können Skripts ausgeführt aber nicht erstellt oder genehmigt werden. Weitere Informationen finden Sie unter [Erstellen von Sicherheitsrollen für Skripts](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Steuerung von Skriptrollen

Standardmäßig können Benutzer kein Skript genehmigen, das sie erstellt haben. Da Skripts leistungsstark und vielseitig sind und auf vielen Geräten bereitgestellt werden können, lassen sich für das Erstellen und Genehmigen von Skripts unterschiedliche Rollen definieren. Dies bietet Ihnen zusätzliche Sicherheit vor der unbeaufsichtigten Ausführung eines Skripts. Sie können die sekundäre Genehmigung deaktivieren, um das Testen zu vereinfachen.

### <a name="approve-or-deny-a-script"></a>Genehmigen oder Ablehnen eines Skripts

Skripts müssen von der Rolle *Skriptgenehmiger* genehmigt werden, bevor sie ausgeführt werden dürfen. So genehmigen Sie ein Skript

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Wählen Sie in der Liste **Skript** das Skript, das Sie genehmigen oder ablehnen möchten. Klicken Sie dann in der Gruppe **Skript** auf der Registerkarte **Start** auf **Genehmigen/Ablehnen**.
4. Aktivieren Sie im Dialogfeld **Skript genehmigen oder ablehnen** für das Skript entweder das Optionsfeld **Genehmigen** oder **Ablehnen**. Geben Sie optional einen Kommentar zu Ihrer Entscheidung ein.  Wenn Sie ein Skript ablehnen, kann es nicht auf Clientgeräten ausgeführt werden. <br>
![Skript: Genehmigung](./media/run-scripts/RS-approval.png)
1. Schließen Sie den Assistenten ab. In der Liste **Skript** ändert sich die Spalte **Genehmigungsstatus** abhängig von der Aktion, die Sie ausgeführt haben.

### <a name="allow-users-to-approve-their-own-scripts"></a>Benutzern erlauben, eigene Skripts zu genehmigen

Diese Genehmigung erfolgt in erster Linie in der Testphase der Skriptentwicklung.

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.
2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.
3. Wählen Sie in der Liste der Standorte Ihren Standort aus, und klicken Sie dann auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
4. Deaktivieren Sie im Dialogfeld **Eigenschaften von Hierarchieeinstellungen** auf der Registerkarte **Allgemein** das Kontrollkästchen **Script authors require additional script approver** (Skriptautoren benötigen einen zusätzlichen Skriptgenehmiger).

>[!IMPORTANT]
>Als bewährte Methode sollten Sie nicht zulassen, dass Skriptautoren ihre eigenen Skripts genehmigen können. Dies sollte nur in einer Testumgebung gestattet sein. Bedenken Sie die möglichen Auswirkungen, die eine Änderung dieser Einstellung in einer Produktionsumgebung mit sich bringt.

## <a name="security-scopes"></a>Sicherheitsbereichen
  
Die Funktion „Skripts ausführen“ arbeitet mit Sicherheitsbereichen, einer bereits vorhandenen Configuration Manager-Funktion, um die Erstellung und Ausführung von Skripts zu steuern, indem Kategorien zugewiesen werden, die Benutzergruppen darstellen. Weitere Informationen zum Verwenden von Sicherheitsbereichen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Erstellen von Sicherheitsrollen für Skripts
Die drei Sicherheitsrollen zum Ausführen von Skripts werden standardmäßig nicht in Configuration Manager erstellt. Führen Sie zum Erstellen der Rollen für die Skriptausführenden, -ersteller und -genehmiger die folgenden Schritte aus:

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** >**Sicherheit** >**Sicherheitsrollen**.
2. Klicken Sie mit der rechten Maustaste auf die Rolle und anschließend mit der linken auf **Kopieren**. Der zu kopierenden Rolle sind bereits Berechtigungen zugewiesen. Achten Sie darauf, nur die gewünschten Rollen zu nutzen. 
3. Legen Sie für die benutzerdefinierte Rolle **Name** und **Beschreibung** fest. 
4. Weisen Sie der Sicherheitsrolle die unten aufgeführten Berechtigungen zu.  

### <a name="security-role-permissions"></a>Berechtigungen für Sicherheitsrollen  

**Rollenname:** Skriptausführende  
- **Beschreibung:** Durch die folgenden Berechtigungen können mit dieser Rolle nur Skripts ausgeführt werden, die zuvor erstellt und von anderen Rollen genehmigt wurden.  
- **Berechtigungen:** Legen Sie für die folgenden Berechtigungen als Status **Ja** fest.  

|Kategorie|Berechtigung|Zustand|
|---|---|---|
|Sammlung|Skript ausführen|Ja|
|Standort|Überwachungsdaten|Ja|
|SMS-Skripts|Überwachungsdaten|Ja|


**Rollenname:** Skriptautoren  
- **Beschreibung:** Durch die folgenden Berechtigungen können mit dieser Rolle Skripts erstellt, aber nicht genehmigt oder ausgeführt werden.  
- **Berechtigungen**: Legen Sie für die folgenden Berechtigungen den in der Tabelle aufgeführten Status fest.
 
|Kategorie|Berechtigung|Zustand|
|---|---|---|
|Sammlung|Skript ausführen|Nein|
|Standort|Überwachungsdaten|Ja|
|SMS-Skripts|Erstellen|Ja|
|SMS-Skripts|Überwachungsdaten|Ja|
|SMS-Skripts|Löschen|Ja|
|SMS-Skripts|Ändern|Ja|


**Rollenname:** Genehmigende Personen für Skripts  
- **Beschreibung:** Durch die folgenden Berechtigungen können mit dieser Rolle Skripts genehmigt, aber nicht erstellt oder ausgeführt werden.  
- **Berechtigungen:** Legen Sie für die folgenden Berechtigungen den in der Tabelle aufgeführten Status fest.  

|Kategorie|Berechtigung|Zustand|
|---|---|---|
|Sammlung|Skript ausführen|Nein|
|Standort|Überwachungsdaten|Ja|
|SMS-Skripts|Überwachungsdaten|Ja|
|SMS-Skripts|Genehmigen|Ja|
|SMS-Skripts|Ändern|Ja|

     
**Beispiel für SMS-Skript-Berechtigungen für die Rolle Skriptersteller**  

 ![Beispiel für SMS-Skript-Berechtigungen für die Rolle Skriptersteller](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Erstellen eines Skripts

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Skript erstellen**.
4. Konfigurieren Sie im Assistenten **Skript erstellen** auf der Seite **Skript** die folgenden Einstellungen:
    - **Skriptname**: Geben Sie einen Namen für das Skript ein. Sie können zwar mehrere Skripts mit dem gleichen Namen erstellen, dies erschwert aber das Auffinden des benötigten Skripts in der Configuration Manager-Konsole.
    - **Skriptsprache**: Derzeit werden nur PowerShell-Skripts unterstützt.
    - **Importieren**: Importieren Sie ein PowerShell-Skript in die Konsole. Das Skript wird im Feld **Skript** angezeigt.
    - **Löschen**: Entfernt das aktuelle Skript aus dem Feld „Skript“
    - **Skript**: Zeigt das gerade importierte Skript. Sie können das Skript in diesem Feld nach Bedarf bearbeiten.
5. Schließen Sie den Assistenten ab. Das neue Skript wird in der Liste **Skript** mit dem Status **Warten auf Genehmigung** angezeigt. Bevor Sie dieses Skript auf Clientgeräten ausführen können, müssen Sie es genehmigen. 

> [!IMPORTANT]
> Vermeiden Sie im Skript einen Neustart des Geräts oder einen Neustart des Configuration Manager-Agents, wenn Sie das Feature „Skripts ausführen“ verwenden. Dies könnte zu einem kontinuierlichen Neustartzustand führen. Bei Bedarf stehen Erweiterungen für die Clientbenachrichtigungsfunktion zur Verfügung, die das Neustarten von Geräten ermöglichen. Anhand der Spalte [Neustart steht aus](../../core/clients/manage/manage-clients.md#restart-clients) können Sie Geräte identifizieren, für die ein Neustart erforderlich ist. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Skriptparameter

Durch Hinzufügen von Parametern zu einem Skript können Sie Ihre Arbeit flexibler gestalten. Sie können bis zu 10 Parameter einschließen. Im Folgenden wird die aktuelle Fähigkeit der Funktion „Skripts ausführen“ mit Skriptparametern für die Datentypen *String* und *Integer* dargelegt. Listen mit vordefinierten Werten sind ebenfalls verfügbar. Wenn das Skript nicht unterstützte Datentypen aufweist, erhalten Sie eine Warnung.

Klicken Sie im Dialogfeld **Skript erstellen** unter **Skript** auf **Skriptparameter**.

Jeder Parameter Ihres Skripts hat ein eigenes Dialogfeld, in dem Sie weitere Details und eine Validierung hinzufügen können. Wenn ein Standardparameter im Skript vorhanden ist, wird er in der Parameterbenutzeroberfläche aufgelistet, und Sie können ihn festlegen. Configuration Manager überschreibt den Standardwert nicht, da der Dienst nie direkt das Skript verändert. Stellen Sie sich dieses Prinzip als „vorab aufgefüllte, vorgeschlagene Werte“ vor, die auf der Benutzeroberfläche bereitgestellt werden. Der Zugriff auf die „Standardwerte“ wird zur Laufzeit jedoch von Configuration Manager nicht genehmigt. Sie können dieses Problem umgehen, indem Sie das Skript so bearbeiten, dass es die richtigen Standardwerte enthält. <!--17694323-->

>[!IMPORTANT]
> Parameterwerte dürfen kein einfaches Anführungszeichen enthalten. </br></br>
> Es ist ein bekanntes Problem, dass Parameterwerte, die einfache Anführungszeichen enthalten oder darin eingeschlossen sind, nicht ordnungsgemäß an das Skript übergeben werden. Wenn Sie Standardparameterwerte angeben, die ein Leerzeichen innerhalb eines Skripts enthalten, verwenden Sie stattdessen doppelte Anführungszeichen. Wenn beim Erstellen oder Ausführen eines **Skripts** Standardparameterwerte angegeben werden, muss der Standardwert unabhängig davon, ob er ein Leerzeichen enthält, nicht in doppelte oder einfache Anführungszeichen eingeschlossen werden.

### <a name="parameter-validation"></a>Validierung von Parametern

Für jeden Parameter in Ihrem Skript gibt es das Dialogfeld **Skriptparameter – Eigenschaften**, in dem Sie eine Validierung für den jeweiligen Parameter hinzufügen können. Nach dem Hinzufügen der Validierung sollten Sie Fehlermeldungen erhalten, wenn Sie einen Wert für einen Parameter eingeben, der nicht dessen Validierung entspricht.

#### <a name="example-firstname"></a>Beispiel: *FirstName*

In diesem Beispiel können Sie die Eigenschaften des Zeichenfolgenparameters *FirstName* festlegen.

![Skriptparameter: String](./media/run-scripts/RS-parameters-string.png)


Der Abschnitt „Überprüfung“ des Dialogfelds **Skriptparametereigenschaften** enthält die folgenden Felder, die Sie verwenden können:

- **Mindestlänge**: Minimale Anzahl von Zeichen im Feld *FirstName*.
- **Maximale Länge**: Maximale Anzahl von Zeichen im Feld *FirstName*.
- **RegEx**: Kofferwort für *Regular Expression*, d.h. regulärer Ausdruck. Weitere Informationen zur Verwendung von regulären Ausdrücken finden Sie im nächsten Abschnitt *Durchführen der Überprüfung von regulären Ausdrücken*.
- **Benutzerdef. Fehler**: Nützlich zum Hinzufügen einer eigenen benutzerdefinierten Fehlermeldung, die alle Fehlermeldungen im Rahmen der Systemüberprüfung ersetzt.

#### <a name="using-regular-expression-validation"></a>Durchführen der Überprüfung von regulären Ausdrücken

Ein regulärer Ausdruck stellt eine kompakte Programmiermethode dar, um eine Zeichenfolge anhand einer codierten Überprüfung zu überprüfen. Sie können z.B. im Feld *FirstName* nach einem fehlenden Großbuchstaben suchen, indem Sie `[^A-Z]` in das Feld *RegEx* eingeben.

Die Verarbeitung regulärer Ausdrücke für dieses Dialogfeld wird vom .NET Framework unterstützt. Hinweise zur Verwendung von regulären Ausdrücken finden Sie unter [Reguläre Ausdrücke von .NET](/dotnet/standard/base-types/regular-expressions) und [Sprachreferenz zu regulären Ausdrücken](/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Beispiele für Skripts

Hier finden Sie einige Beispiele, die Skripts veranschaulichen, die sich mit dieser Funktion verwenden lassen.

### <a name="create-a-new-folder-and-file"></a>Erstellen eines neuen Ordners und einer neuen Datei

Dieses Skript erstellt basierend auf der Namenseingabe einen neuen Ordner und eine Datei in diesem Ordner.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Abrufen der Betriebssystemversion

Dieses Skript verwendet WMI, um die Betriebssystemversion des Computers abzufragen.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> Bearbeiten oder Kopieren von PowerShell-Skripts
<!--3705507-->
*(Mit Version 1902 eingeführt)*  
Sie können ein vorhandenes PowerShell-Skript **bearbeiten** oder **kopieren**, das mit dem Feature **Skripts ausführen** verwendet wird. Sie können ein Skript, das Sie ändern müssen, nun direkt bearbeiten und müssen es nicht mehr neu erstellen. Für beide Aktionen wird der gleiche Assistent wie zum Erstellen eines neuen Skripts verwendet. Wenn Sie ein Skript bearbeiten oder kopieren, behält Configuration Manager den Genehmigungsstatus nicht bei.

> [!Tip]  
> Bearbeiten Sie kein Skript, das aktiv auf Clients ausgeführt wird. Auf diesen wird die Ausführung des ursprünglichen Skripts nicht abgeschlossen, und Sie erhalten möglicherweise nicht die gewünschten Ergebnisse von diesen Clients.  

### <a name="edit-a-script"></a>Bearbeiten eines Skripts

1. Wechseln Sie zum Knoten **Skripts** im Arbeitsbereich **Softwarebibliothek**.
1. Wählen Sie das zu bearbeitende Skript aus, und klicken Sie dann im Menüband auf **Bearbeiten**. 
1. Auf der Seite **Skriptdetails** können Sie das Skript ändern oder neu importieren.
1. Klicken Sie auf **Weiter**, um die **Zusammenfassung** anzuzeigen. Wenn Sie die Bearbeitung abgeschlossen haben, klicken Sie auf **Schließen**.

### <a name="copy-a-script"></a>Kopieren eines Skripts

1. Wechseln Sie zum Knoten **Skripts** im Arbeitsbereich **Softwarebibliothek**.
1. Wählen Sie das zu kopierende Skript aus, und klicken Sie im Menüband auf **Kopieren**.
1. Benennen Sie das Skript im Feld **Skriptname** um, und nehmen Sie ggf. weitere erforderliche Änderungen vor.
1. Klicken Sie auf **Weiter**, um die **Zusammenfassung** anzuzeigen. Wenn Sie die Bearbeitung abgeschlossen haben, klicken Sie auf **Schließen**.


## <a name="run-a-script"></a>Ausführen eines Skripts

Nachdem ein Skript genehmigt wurde, kann es für ein einzelnes Gerät oder eine Sammlung ausgeführt werden. Sobald die Ausführung Ihres Skripts beginnt, wird es schnell in einem System mit hoher Priorität gestartet, bei dem binnen einer Stunde ein Timeout auftritt. Die Ergebnisse des Skripts werden dann über ein Zustandsmeldungssystem zurückgegeben.

So wählen Sie eine Sammlung von Zielen für Ihr Skript aus

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Klicken Sie im Arbeitsbereich Bestand und Kompatibilität auf **Gerätesammlungen**.
3. Klicken Sie in der Liste **Gerätesammlungen** auf die Sammlung von Geräten, auf denen das Skript ausgeführt werden soll.
4. Wählen Sie eine Sammlung Ihrer Wahl aus, und klicken Sie auf **Skript ausführen**.
5. Wählen Sie im Assistenten **Skript ausführen** auf der Seite **Skript** ein Skript in der Liste aus. Es werden nur genehmigte Skripts angezeigt.
6. Klicken Sie auf **Weiter**, und schließen Sie den Assistenten ab.

> [!IMPORTANT]
> Wenn ein Skript nicht ausgeführt wird, weil ein Zielgerät beispielsweise während des einstündigen Zeitraums ausgeschaltet ist, müssen Sie es erneut ausführen.

### <a name="target-machine-execution"></a>Ausführung auf dem Zielcomputer

Das Skript wird mit dem Konto *System* oder *Computer* auf den entsprechenden Zielclients ausgeführt. Dieses Konto hat begrenzten Netzwerkzugriff. Jeder Zugriff auf Remotesysteme und -standorte durch das Skript muss entsprechend eingerichtet werden.

## <a name="script-monitoring"></a>Skriptüberwachung

Nachdem Sie mit der Anwendung eines Skripts auf eine Sammlung von Geräten begonnen haben, gehen Sie wie folgt vor, um den Vorgang zu überwachen. Sie können ein Skript in Echtzeit überwachen, während es ausgeführt wird, und später zum Zustand und den Ergebnissen einer bestimmten Ausführung von „Skript ausführen“ zurückkehren. Die Skriptstatusdaten werden als Teil des [Wartungstasks zum Löschen veralteter Clientvorgänge](../../core/servers/manage/reference-for-maintenance-tasks.md) oder durch Löschen des Skripts bereinigt.<br>

![Skriptüberwachung: Status der Skriptausführung](./media/run-scripts/RS-monitoring-three-bar.png)

1. Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.
2. Klicken Sie im Arbeitsbereich **Überwachung** auf **Skriptstatus**.
3. In der Liste **Skriptstatus** sehen Sie die Ergebnisse für jedes Skript, das Sie auf Clientgeräten ausgeführt haben. Der Exitcode **0** eines Skripts bedeutet im Allgemeinen, dass das Skript erfolgreich ausgeführt wurde.

 
   ![Skriptmonitor: gekürztes Skript](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>Skriptausgabe

Clients geben die Skriptausgabe mithilfe der JSON-Formatierung zurück, indem sie die Ergebnisse des Skripts über die Pipeline an das Cmdlet [ConvertTo-Json](/powershell/module/microsoft.powershell.utility/convertto-json) übergeben. Das JSON-Format gibt stets eine lesbare Skriptausgabe zurück. Bei Skripts, die keine Objekte als Ausgabe zurückgeben, konvertiert das Cmdlet „ConvertTo-Json“ die Ausgabe in eine einfache Zeichenfolge, die der Client statt JSON zurückgibt.  

- Skripts mit unbekanntem Ergebnis oder einem Client, der offline war, werden nicht in den Diagrammen oder Datasets angezeigt. <!--507179-->
- Vermeiden Sie die Rückgabe einer umfassenden Skriptausgabe, da diese auf 4 KB beschränkt wird. <!--508488-->
- Konvertieren Sie Enumerationsobjekte in Zeichenfolgenwerte, damit die JSON-Formatierung bei der Anzeige der Skripts korrekt verwendet wird. <!--508377-->

   ![Konvertieren eines Enumerationsobjekts in einen Zeichenfolgenwert](./media/run-scripts/enum-tostring-JSON.png)

Sie können die ausführliche Skriptausgabe im nicht formatierten Format oder im strukturierten JSON-Format anzeigen. Diese Formatierung vereinfacht das Lesen und Analysieren der Ausgabe. Wenn das Skript gültigen Text im JSON-Format zurückgibt oder die Ausgabe mithilfe des PowerShell-Cmdlets [ConvertTo-Json](/powershell/module/microsoft.powershell.utility/convertto-json) in JSON konvertiert werden kann, zeigen Sie die ausführliche Ausgabe entweder als **JSON-Ausgabe** oder als **unformatierte Ausgabe** an. Andernfalls ist die einzige Option **Skriptausgabe**.

### <a name="example-script-output-is-convertible-to-valid-json"></a>Beispiel: Die Skriptausgabe kann in ein gültiges JSON-Format konvertiert werden.

Befehl: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Beispiel: Die Skriptausgabe weist kein gültiges JSON-Format auf.

Befehl: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>Protokolldateien

- Für den Client standardmäßig unter C:\Windows\CCM\logs:  
  - **Scripts.log**  
  - **CcmMessaging.log**  

- Auf dem Verwaltungspunkt standardmäßig unter: C:\SMS_CCM\Logs:
  - **MP_RelayMsgMgr.log**  

- Auf dem Standortserver standardmäßig unter: C:\Programme\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Grundlagen der rollenbasierten Verwaltung](../../core/understand/fundamentals-of-role-based-administration.md)