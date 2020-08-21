---
title: Verwenden des Tasksequenz-Editors
titleSuffix: Configuration Manager
description: Grundlegendes zur Verwendung des Tasksequenz-Editors in der Configuration Manager-Konsole
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a4aaaab8eb9195f4f5dce4deb890540b0837852
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697451"
---
# <a name="use-the-task-sequence-editor"></a>Verwenden des Tasksequenz-Editors

*Gilt für: Configuration Manager (Current Branch)*

Bearbeiten Sie Tasksequenzen in der Configuration Manager-Konsole mithilfe des **Tasksequenz-Editors**. Verwenden Sie den Editor für Folgendes:  

- Öffnen einer schreibgeschützten Ansicht der Tasksequenz

- Hinzufügen von Schritten zur Tasksequenz bzw. Entfernen von Schritten aus dieser  

- Ändern der Reihenfolge der Tasksequenzschritte  

- Hinzufügen oder Entfernen von Gruppen von Schritten  

- Kopieren und Einfügen von Schritten zwischen Tasksequenzen

- Festlegen von Schrittoptionen, z. B. ob die Tasksequenz beim Auftreten eines Fehlers fortgesetzt wird  

- Hinzufügen von Bedingungen zu den Schritten und Gruppen einer Tasksequenz  

- Kopieren und Einfügen von Bedingungen zwischen Schritten in einer Tasksequenz

- Suchen der Tasksequenz, um Schritte schnell zu finden

Bevor Sie eine Tasksequenz bearbeiten können, müssen Sie diese erstellen. Weitere Informationen finden Sie unter [Verwalten von Tasksequenzen zum Automatisieren von Tasks](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>Informationen zum Tasksequenz-Editor

Der Tasksequenz-Editor umfasst die folgenden Komponenten:

![Screenshot: Fenster des Tasksequenz-Editors einer Beispieltasksequenz mit Anmerkungen](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Der Name der Tasksequenz
2. Suchen. Weitere Informationen finden Sie unter [Suchen](#bkmk_search).
3. **Eigenschaften** der ausgewählten Gruppe oder des ausgewählten Schritts in der Sequenz

    Weitere Informationen zu den Eigenschaften und Optionen eines bestimmten Schritts finden Sie in den [Informationen zu Tasksequenzschritten](task-sequence-steps.md).

4. **Optionen** für die ausgewählte Gruppe oder den ausgewählten Schritt in der Sequenz

    Weitere Informationen zu den allgemeinen Optionen für alle Schritte oder den Optionen eines bestimmten Schritts finden Sie in den [Informationen zu Tasksequenzschritten](task-sequence-steps.md).

    Weitere Informationen zum Konfigurieren von Bedingungen finden Sie unter [Bedingungen](#bkmk_conditions).

5. **Hinzufügen** einer Gruppe oder von Schritten
6. **Entfernen** einer Gruppe oder von Schritten
7. Zuklappen oder Aufklappen aller Gruppen
8. Verschieben der Position einer Gruppe oder eines Schritts in der Sequenz (nach oben oder nach unten)
9. Die Tasksequenz:
    - Zeigen Sie die Reihenfolge von Schritten und Gruppen an.
    - Klappen Sie eine Gruppe auf oder zu.
    - Wenn Sie einen Schritt oder eine Gruppe unter den **Optionen** deaktivieren, wird dieser oder diese in der Sequenz ausgegraut.
    - Das Symbol eines Schritts ändert sich in ein rotes Fehlersymbol, wenn ein Problem mit dem Schritt besteht. Ein erforderlicher Wert fehlt z. b.
10. **OK**: Speichern und schließen
11. **Abbrechen:** Schließen ohne Speichern der Änderungen
12. **Übernehmen**: Speichern der Änderungen und Offenhalten des Fensters

Sie können die Größe des Tasksequenz-Editors mithilfe der Windows-Standardsteuerelemente anpassen. Wenn Sie die Breiten der beiden Hauptbereiche anpassen möchten, klicken Sie mit der Maus auf die Leiste zwischen der Tasksequenz und den Schritteigenschaften, und ziehen Sie diese dann nach links oder rechts.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a> Anzeigen einer Tasksequenz

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie anzeigen möchten.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Tasksequenz** die Option **Anzeigen** aus.

    > [!TIP]
    > Dies ist die Standardaktion. Wenn Sie auf eine Tasksequenz doppelklicken, wird die Tasksequenz **angezeigt**.

Durch diese Aktion wird der Tasksequenz-Editor im schreibgeschützten Modus geöffnet. In diesem Modus können Sie die folgenden Aktionen ausführen:

- Anzeigen aller Gruppen, Schritte, Eigenschaften und Optionen
- Erweitern und Reduzieren der Gruppen
- Suchen der Tasksequenz
- Anpassen der Größe des Editor-Fensters

In diesem schreibgeschützten Modus können Sie keine Änderungen vornehmen. Dazu zählt auch das Kopieren eines Schritts oder einer Bedingung. Bei dieser Aktion wird die Tasksequenz zudem nicht für die Bearbeitung gesperrt. Weitere Informationen zu diesen Sperren finden Sie unter [Entfernen der Sperre beim Bearbeiten](#bkmk_sedo).

Wenn Sie Änderungen an einer Tasksequenz vornehmen möchten, schließen Sie das Fenster des Tasksequenz-Editors, das im schreibgeschützten Modus geöffnet ist. [Bearbeiten](#bkmk_edit) Sie anschließend die Tasksequenz.

> [!NOTE]  
> Wenn Sie eine Tasksequenz anzeigen oder bearbeiten, die mithilfe des Tasksequenzerstellungs-Assistenten erstellt wurde, kann die Aktion oder der Typ des Schritts als Schrittname verwendet werden. Ein Schritt kann z.B. den Namen „Festplatte 0 partitionieren“ haben. Dies ist die Aktion für einen Schritt vom Typ [Datenträger formatieren und partitionieren](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Alle Tasksequenzschritte werden nach Ihrem *Typ* dokumentiert, also nicht unbedingt nach dem vom Editor angezeigten Namen des Schritts.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Bearbeiten einer Tasksequenz

Gehen Sie wie folgt vor, um eine vorhandene Tasksequenz zu ändern:  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie bearbeiten möchten.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Tasksequenz** die Option **Bearbeiten** aus. Führen Sie dann eine der folgenden Aktionen aus:  

    - **Hinzufügen eines Schritts:** Klicken Sie auf **Hinzufügen**, wählen Sie eine Kategorie und dann den Schritt aus, den Sie hinzufügen möchten. Wenn Sie z. B. den Schritt [Befehlszeile ausführen](task-sequence-steps.md#BKMK_RunCommandLine) hinzufügen möchten, wählen Sie **Hinzufügen** und die Kategorie **Allgemein** aus. Klicken Sie dann auf **Befehlszeile ausführen**. Bei dieser Aktion wird der Schritt nach dem derzeit ausgewählten Schritt hinzugefügt.

    - **Hinzufügen einer Gruppe:** Klicken Sie auf **Hinzufügen** und dann auf **Neue Gruppe**. Nachdem Sie eine Gruppe hinzugefügt haben, können Sie dieser Schritte hinzufügen.  

    - **Ändern der Reihenfolge:** Wählen Sie den Schritt oder die Gruppe aus, dessen bzw. deren Reihenfolge Sie ändern möchten. Verwenden Sie dann die Symbole **Nach oben verschieben** und **Nach unten verschieben**. Sie können nicht mehrere Schritte oder Gruppen gleichzeitig verschieben. Diese Aktionen sind auch verfügbar, wenn Sie mit der rechten Maustaste auf eine Gruppe oder einen Schritt klicken.

        Sie können eine Gruppe oder einen Schritt ausschneiden, kopieren und einfügen. Klicken Sie mit der rechten Maustaste auf das Element, und wählen Sie die Aktion aus. Sie können auch Standardtastenkombinationen für jede Aktion verwenden:

        - Ausschneiden: **STRG** + **X**
        - Kopieren: **STRG** + **C**
        - Einfügen: **STRG** + **V**

    - **Einen Schritt oder eine Gruppe entfernen**: Wählen Sie den Schritt oder die Gruppe aus, und klicken Sie auf **Entfernen**.  

4. Klicken Sie auf **OK**, um die Änderungen zu speichern und das Fenster zu schließen. Klicken Sie auf **Abbrechen**, um die Änderungen zu verwerfen und das Fenster zu schließen. Wählen Sie **Anwenden** aus, um die Änderungen zu speichern und den Tasksequenz-Editor geöffnet zu lassen.  

Eine Liste verfügbarer Tasksequenzschritte finden Sie unter [Tasksequenzschritte](task-sequence-steps.md).  

> [!IMPORTANT]  
> Wenn die Tasksequenz nicht zugeordnete Verweise auf ein Objekt aufgrund der Bearbeitung aufweist, werden Sie vom Editor aufgefordert, den Verweis zu beheben, bevor er geschlossen werden kann. Es können folgende Aktionen durchgeführt werden:  
>
> - Korrigieren des Verweises
> - Löschen des Objekts ohne Verweis aus der Tasksequenz  
> - Vorübergehendes Deaktivieren des fehlerhaften Tasksequenzschritts, bis der fehlerhafte Verweis korrigiert oder entfernt wurde  

Sie können mehrere Instanzen des Tasksequenz-Editors gleichzeitig öffnen. Mit diesem Verhalten können Sie mehrere Tasksequenzen vergleichen oder Schritte zwischen diesen kopieren und einfügen. Sie können eine Tasksequenz **bearbeiten** und eine andere **anzeigen**, jedoch können Sie nicht beide Aktionen auf dieselbe Tasksequenz anwenden.

## <a name="conditions"></a><a name="bkmk_conditions"></a> Bedingungen

Verwenden Sie Bedingungen, um das Verhalten der Tasksequenz zu steuern. Fügen Sie Bedingungen zu einem einzelnen Schritt oder einer Gruppe von Schritten hinzu. Die Tasksequenz wertet die Bedingungen aus, bevor sie den Schritt auf dem Gerät durchführt. Sie führt den Schritt nur durch, wenn die Bedingungen erfüllt sind. Wenn eine Bedingung nicht erfüllt ist, überspringt die Tasksequenz die Gruppe oder den Schritt.

Verwenden Sie die Registerkarte **Optionen**, um Bedingungen zu verwalten:

![Verwalten von Bedingungen auf der Registerkarte „Optionen“ des Tasksequenz-Editors](media/4621098-copy-paste-ts-condition.png)

Die folgenden Bedingungstypen sind verfügbar:

- **if-Anweisung:** Verwenden Sie eine *if*-Anweisung zum Gruppieren von Bedingungen. Sie können **alle Bedingungen**, **eine beliebige Bedingung** oder **keine** auswerten.

- **Tasksequenzvariable.** Werten Sie den aktuellen Wert einer beliebigen integrierten, benutzerdefinierten oder schreibgeschützten [Tasksequenzvariablen](task-sequence-variables.md) oder einer Tasksequenzvariablen für eine Aktion in der Tasksequenzumgebung aus. Weitere Informationen finden Sie unter [Bedingung für einen Schritt](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > Sie können in dieser Bedingung eine Arrayvariable verwenden, müssen jedoch den bestimmten Arraymember angeben. Beispielsweise gibt `OSDAdapter0EnableDHCP` an, ob der *erste* Netzwerkadapter das DHCP aktiviert. Weitere Informationen finden Sie unter [Array-Variablen](using-task-sequence-variables.md#bkmk_array).

- **Betriebssystemversion**: Werten Sie die Betriebssystemversion des Geräts aus, auf dem die Tasksequenz ausgeführt wird. In dieser Liste finden Sie die allgemeinen Betriebssystemversionen, die in Configuration Manager verwendet werden. Verwenden Sie die Bedingung **WMI abfragen**, um eine detailliertere Betriebssystemversion wie z. B. eine bestimmte Windows 10-Version auszuwerten.

- **Betriebssystemsprache:** Werten Sie die Betriebssystemsprache des Geräts aus, auf dem die Tasksequenz ausgeführt wird. In dieser Liste finden Sie die 257 Sprachen, die von Windows unterstützt werden.

- **Dateieigenschaften:** Werten Sie die Version oder den Zeitstempel einer beliebigen Datei auf dem Gerät aus, auf dem die Tasksequenz ausgeführt wird.

- **Ordnereigenschaften:** Werten Sie den Zeitstempel eines beliebigen Ordners auf dem Gerät aus, auf dem die Tasksequenz ausgeführt wird.

- **Registrierungseinstellung:** Werten Sie einen beliebigen Registrierungsschlüssel des Geräts aus, auf dem die Tasksequenz ausgeführt wird.

- **WMI abfragen:** Geben Sie den Namespace und die Abfrage an, die auf dem Gerät ausgewertet werden sollen, auf dem die Tasksequenz ausgeführt wird.

- **Installierte Software:** Geben Sie eine Windows Installer-Datei zum Laden von Produktinformationen zum Abgleich auf dem Gerät an, auf dem die Tasksequenz ausgeführt wird. Sie können einen Abgleich mit einem bestimmten Produkt oder einer beliebigen Version des Produkts vornehmen.

### <a name="cmdlets-for-conditions"></a>Cmdlets für Bedingungen

Verwalten Sie Bedingungen mithilfe der folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Kopieren und Einfügen von Bedingungen

<!-- 4621098 -->

Ab Version 1910 können Sie Bedingungen nun im Tasksequenz-Editor kopieren und einfügen, um Bedingungen aus einem Schritt in einem anderen wiederzuverwenden. Wählen Sie eine Bedingung aus, um sie auszuschneiden oder zu kopieren. Wenn eine Bedingung über untergeordnete Elemente verfügt, wird der gesamte Block kopiert. Wenn sich eine Bedingung in der Zwischenablage befindet, können Sie sie über die folgenden Optionen einfügen:

- Davor einfügen
- Dahinter einfügen
- Darunter einfügen (gilt nur für geschachtelte Bedingungen)

Verwenden Sie die Standardtastaturkombinationen zum Kopieren (**STRG** + **C**) und Ausschneiden (**STRG** + **X**). Mit der Standardtastaturkombination **STRG** + **V** können Sie die Aktion **Dahinter einfügen** ausführen.

Es stehen außerdem neue Optionen zur Verfügung, um Bedingungen in der Liste nach oben oder nach unten zu verschieben.

> [!Note]  
> Sie können Bedingungen zwischen Schritten in einer Tasksequenz kopieren und einfügen. Diese Aktion wird nicht zwischen unterschiedlichen Tasksequenzen unterstützt.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> Entfernen der Sperre beim Bearbeiten

<!--3699337-->
Wenn die Configuration Manager-Konsole nicht mehr reagiert, können Sie möglicherweise 30 Minuten lang (bis die Sperre aufgehoben wird) keine weiteren Änderungen vornehmen. Diese Sperre ist Teil des SEDO-Systems (Serialized Editing of Distributed Objects) für Configuration Manager. Weitere Informationen finden Sie unter [Configuration Manager SEDO (SEDO für Configuration Manager)](../../develop/core/understand/sedo.md).

Ab Version 1906 können Sie die Sperre für eine Tasksequenz löschen. Diese Aktion gilt nur für Benutzerkonten mit Sperren. Es muss dabei das Gerät verwendet werden, über das der Standort die Sperre erstellt hat. Wenn Sie versuchen, auf eine gesperrte Tasksequenz zuzugreifen, können Sie jetzt die Option **Änderungen verwerfen** auswählen und das Objekt weiter bearbeiten. Diese Änderungen würden sowieso gelöscht werden, sobald die Sperre aufgehoben wird.

> [!TIP]
> Ab Version 1910 können Sie die Sperre für ein beliebiges Objekt in der Configuration Manager-Konsole löschen. Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> Suchen

<!-- 4621085 -->

Wenn Sie über eine große Tasksequenz mit vielen Gruppen und Schritte verfügen, kann es schwierig sein, bestimmte Schritte zu finden. Ab Version 1910 können Sie jetzt im Tasksequenz-Editor suchen. Dadurch können Sie Schritte in der Tasksequenz schneller finden.

![Suchen im Tasksequenz-Editor](media/4621085-task-sequence-search.png)

Geben Sie zum Start der Suche einen Suchbegriff ein. Sie können Ihre Suche mit den folgenden Typen eingrenzen:

- Schrittname
- Schrittbeschreibung
- Schritttyp
- Gruppenname
- Gruppenbeschreibung
- Variablenname
- Bedingungen
- Andere Inhalte, z.B. Zeichenfolgen wie Variablenwerte oder Befehlszeilen

Alle Bereiche sind standardmäßig aktiviert.

Sie können auch mit den folgenden Attributen nach allen Schritten filtern:

- Bei Fehler fortsetzen
- Hat Bedingungen

Keiner der Filter ist standardmäßig aktiviert.

Bei der Suche werden im Editor-Fenster die Schritte, die Ihren Suchkriterien entsprechen, gelb hervorgehoben.

Mit den folgenden Tastenkombinationen können Sie schnell auf diese Suchfelder zugreifen und durch die Suchergebnisse navigieren:

- **STRG** + **F**: Eine Suchzeichenfolge eingeben.
- **STRG** + **O**: Die Suchoptionen zum Begrenzen der Ergebnisse auswählen.
- **F3** oder **EINGABETASTE**: Die Ergebnisse vorwärts durchlaufen.
- **UMSCHALT** + **F3**: Die Ergebnisse rückwärts durchlaufen.

## <a name="see-also"></a>Weitere Informationen:

- [Verwalten und Erstellen von Tasksequenzen](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Informationen zu Tasksequenzschritten](task-sequence-steps.md)

- [Verwenden von Tasksequenzvariablen](using-task-sequence-variables.md)

- [Verwenden der Configuration Manager-Konsole](../../core/servers/manage/admin-console.md)