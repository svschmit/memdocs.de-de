---
title: 'Erstellen von Konfigurationselementen für von Clients verwaltete Mac-Geräte '
titleSuffix: Configuration Manager
description: Verwenden Sie das Configuration Manager-Konfigurationselement für Max OS X, um Einstellungen für Mac OS X-Geräte zu verwalten.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 9323fc3c1203d20c77af1f2fd27cee0a377e8d68
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240081"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Erstellen von Konfigurationselementen für Mac OS X-Geräte
Verwenden Sie das Configuration Manager-Konfigurationselement **Mac OS X (benutzerdefiniert)** , um Einstellungen für Mac OS X-Geräte zu bearbeiten, die mit dem Configuration Manager-Client verwaltet werden.  
  
Anwendungseinstellungen werden im Mac OS X-Betriebssystem in Eigenschaftenlistendateien (PLIST-Dateien) gespeichert. Verwenden Sie Kompatibilitätseinstellungen zum Auswerten und Wiederherstellen von Einstellungen in einer Eigenschaftenlistendatei. Sie können Mac OS X-Einstellungen auch mithilfe eines Shellskripts verwalten, das einen Wert zurückgibt, den Sie zum Auswerten und Wiederherstellen der Konformität verwenden können.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Erstellen eines benutzerdefinierten Konfigurationselements für Mac OS X  
  
1. Wählen Sie in der Configuration Manager-Konsole die Option **Assets und Konformität** aus.  
  
2. Erweitern Sie im Arbeitsbereich **Assets und Konformität** die **Konformitätseinstellungen**, und wählen Sie dann **Konfigurationselemente** aus.  
  
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  
  
4. Geben Sie auf der Seite **Allgemein** des Assistenten zum **Erstellen von Konfigurationselementen** einen Namen und optional eine Beschreibung für das Konfigurationselement an.  
  
5. Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Mac OS X (benutzerdefiniert)** aus.  
  
6. Wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern, wählen Sie **Kategorien** aus.  
  
7. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweiligen Mac OS X-Versionen zur Auswertung des Konfigurationselements aus.  
  
8. Fügen Sie auf der Seite **Einstellungen** des Assistenten neue Einstellungen hinzu, die hinsichtlich ihrer Konformität auf Mac-Computern ausgewertet werden. Klicken Sie auf **Neu**, um das Dialogfeld **Einstellung erstellen** zu öffnen.  
  
9. Geben Sie im Dialogfeld **Einstellung erstellen** einen eindeutigen Namen und eine Beschreibung für die Einstellung ein.  
  
10. Wählen Sie den gewünschten **Einstellungstyp** aus, und geben Sie die erforderlichen Informationen ein:  
  
    -   **Einstellungen für Mac OS X**  
  
        -   **Anwendungs-ID**: Geben Sie die Anwendungs-ID der Eigenschaftenlistendatei an, aus der die Konformität eines Schlüssels ausgewertet werden soll.  
  
             Beispielsweise, wenn Sie Einstellungen für den Safari-Webbrowser bearbeiten möchten, können **com.apple.Safari.plist**.  
  
        -   **Schlüssel:** Geben Sie den Namen des Schlüssels an, dessen Konformität auf Mac-Computern ausgewertet werden soll. Verwenden Sie die folgende Syntax: */<Wörterbuch\>/<Schlüsselname\>* .  
  
            > [!IMPORTANT]  
            >  Für den Schlüsselnamen muss die Groß-/Kleinschreibung beachtet werden, und er wird nicht ausgewertet, wenn er sich vom Schlüsselnamen auf dem Mac-Computer unterscheidet. Außerdem können Sie den Namen des Schlüssels nicht mehr bearbeiten, nachdem Sie ihn angegeben haben. Wenn Sie den Schlüsselnamen bearbeiten müssen, löschen Sie die Einstellung, und erstellen Sie sie dann erneut.  
  
    -   **Skript**  
  
        -   **Ermittlungsskript**: Wählen Sie **Skript hinzufügen** aus, und geben Sie dann ein Shellskript an, um die Konformität von Einstellungen auf dem Mac-Computer zu bewerten. Verwenden Sie den Befehl **echo** im Shellskript, um Werte zur Kompatibilität an Configuration Manager zurückzugeben. Configuration Manager verwendet die in **STDOUT** zurückgegebenen Ergebnisse, um die Kompatibilität auszuwerten.  
  
            > [!IMPORTANT]  
            >  Schließen Sie den Befehl **Neu starten** nicht in das Ermittlungsskript ein. Da das Ermittlungsskript bei jedem Neustart des Clients ausgeführt wird, würde dies dazu führen, dass der Mac-Computer immer wieder neu gestartet wird.  
  
        -   **Bereinigungsskript (optional)** : Optional können Sie **Skript hinzufügen** auswählen und ein Shellskript eingeben, das zum Wiederherstellen aller auf Mac-Clientcomputern ermittelten nicht konformen Einstellungen verwendet wird.  
  
            > [!IMPORTANT]  
            >  Um sicherzustellen, dass Sie keine Formatierungszeichen einfügen, die der Macintosh-Computer nicht interpretieren kann, verwenden Sie kein Kopieren und Einfügen. Geben Sie stattdessen das Skript ein.  
  
11. Wählen Sie den **Datentyp** aus, also das Format, in dem die Bedingung die Daten zurückgibt, bevor sie zum Auswerten der Einstellung verwendet werden.  
  
    > [!NOTE]  
    >  Vom Datentyp **Gleitkomma** werden nur 3 Ziffern nach dem Dezimalkomma unterstützt.  
    >   
    >  Configuration Manager unterstützt für die Skripteinstellungen von Mac-Konfigurationselementen nicht den Datentyp **boolesch**. Legen Sie den Datentyp stattdessen auf **Integer** fest, und stellen Sie sicher, dass das Skript einen ganzzahligen Wert zurückgibt.  
  
12. Wählen Sie **OK** aus, um die Einstellung zu speichern, und schließen Sie das Dialogfeld **Einstellung erstellen**. Fügen Sie weitere benötige Einstellungen hinzu.  
  
13. Geben Sie auf der Seite **Konformitätsregeln** des Assistenten die Bedingungen an, mit denen die Konformität eines Konfigurationselements definiert wird. Damit eine Einstellung auf Kompatibilität ausgewertet werden kann, muss sie über mindestens eine Kompatibilitätsregel verfügen. Klicken Sie auf **Neu**, um eine neue Regel hinzuzufügen.  
  
14. Geben Sie im Dialogfeld **Regel erstellen** die folgenden Informationen an:  
  
    -   **Name:** Geben Sie einen Namen für die Kompatibilitätsregel ein.  
  
    -   **Beschreibung:** Geben Sie eine Beschreibung für die Kompatibilitätsregel ein.  
  
    -   **Ausgewählte Einstellung:** Wählen Sie zum Öffnen des Dialogfelds **Einstellung auswählen** die Option **Durchsuchen** aus. Wählen Sie die Einstellung aus, für die Sie eine Regel definieren möchten, oder wählen Sie **Neue Einstellung** aus. Klicken Sie danach auf **Weiter**.  
  
        > [!TIP]  
        >  Sie können zum Anzeigen von Informationen über die derzeit ausgewählte Einstellung auch auf **Eigenschaften** klicken.  
  
    -   **Regeltyp:** Wählen Sie den Typ der Konformitätsregel, die Sie verwenden möchten:  
  
        -   **Wert:** Erstellen Sie eine Regel, mit deren Hilfe der vom Konfigurationselement zurückgegebene Wert mit einem von Ihnen angegebenen Wert verglichen wird.  
  
        -   **Existenziell**: Erstellen Sie eine Regel, mit der die Einstellung abhängig davon ausgewertet wird, ob sie auf einem Gerät vorhanden ist.  
  
    -   Geben Sie für eine Regel des Typs **Wert**die folgenden Informationen an:  
  
        -   **Die Einstellung muss der folgenden Regel entsprechen**: Wählen Sie einen Operator und einen Wert aus, der mit der ausgewählten Einstellung auf Konformität ausgewertet wird. Folgende Operatoren können verwendet werden:  
  
            -   **Gleich**  
  
            -   **Ungleich**  
  
            -   **Größer als**  
  
            -   **Kleiner als**  
  
            -   **Zwischen**  
  
            -   **Größer oder gleich**  
  
            -   **Kleiner oder gleich**  
  
            -   **Eine von**: Geben Sie im Textfeld pro Zeile einen Eintrag an.  
  
            -   **Keine von**: Geben Sie im Textfeld pro Zeile einen Eintrag an.  
  
        -   **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird:** Wählen Sie diese Option aus, wenn nicht konforme Regeln von Configuration Manager automatisch wiederhergestellt werden sollen.  
  
            > [!IMPORTANT]  
            >  Sie können nicht kompatible Regeln nur wiederherstellen, wenn der Regeloperator auf **Ist gleich**festgelegt ist.  
  
        -   **Als nicht konform melden, wenn diese Einstellungsinstanz nicht gefunden wird**: Das Konfigurationselement meldet Nichtkonformität, wenn diese Einstellung auf dem Mac-Computer nicht gefunden wird.  
  
        -   **Schweregrad der Nichtkonformität für Berichte**: Geben Sie den gemeldeten Schweregrad an, wenn bei dieser Konformitätsregel ein Fehler auftritt. Die verfügbaren Schweregrade sind:  
  
            -   **Keine**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
            -   **Information**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
            -   **Warnung:** Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
            -   **Kritisch**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
            -   **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Auf dem Macintosh-Clientcomputer wird auch dieser Schweregrad protokolliert.  
  
    -   Geben Sie für eine Regel des Typs **Existenziell**die folgenden Informationen an:  
  
        -   Wählen Sie eine der folgenden Optionen aus:  
  
            -   **Diese Einstellung muss auf Clientgeräten vorhanden sein.**  
  
            -   **Diese Einstellung darf auf Clientgeräten nicht vorhanden sein.**  
  
        -   **Schweregrad der Nichtkonformität für Berichte**: Geben Sie den zu meldenden Schweregrad an, wenn bei dieser Konformitätsregel ein Fehler auftritt. Die verfügbaren Schweregrade sind:  
  
            -   **Keine**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
            -   **Information**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
            -   **Warnung:** Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
            -   **Kritisch**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
            -   **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Auf dem Macintosh-Clientcomputer wird auch dieser Schweregrad protokolliert.  
  
        > [!NOTE]  
        >  Die angezeigten Optionen sind möglicherweise unterschiedlich, je nach Einstellungstyp, für den Sie eine Regel konfigurieren.  
  
15. Wählen Sie **OK** aus, um das Dialogfeld **Regel erstellen** zu schließen.  
  
16. Bestätigen Sie auf der Seite **Zusammenfassung** die Einstellungen für das neue Konfigurationselement. Schließen Sie anschließend den Assistenten ab.  
  
Sie können das neue Konfigurationselement im Arbeitsbereich **Assets und Konformität** im Knoten **Konfigurationselemente** anzeigen.  
  
Wenn Sie dieses Konfigurationselement einer Konfigurationsbaseline hinzufügen möchten, ziehen Sie [Erstellen von Konfigurationsbaselines](../../compliance/deploy-use/create-configuration-baselines.md) zurate.  
  
## <a name="next-steps"></a>Nächste Schritte

 [Konfigurationselemente für Geräte, die mit dem Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/create-configuration-items.md)
