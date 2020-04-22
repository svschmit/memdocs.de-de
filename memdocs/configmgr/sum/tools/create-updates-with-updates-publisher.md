---
title: Erstellen von Updates
titleSuffix: Configuration Manager
description: Erstellen und Bündeln von Softwareupdates mit System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708698"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Erstellen von Softwareupdates und Updatepaketen mit Updates Publisher

*Gilt für: System Center Updates Publisher*

Mit Updates Publisher können Sie den **Assistenten zum Erstellen von Updates** zum Erstellen eigener Updates und den **Assistenten zum Erstellen von Paketen** zum Erstellen von Updatepaketen verwenden.

Diese zwei Assistenten haben ähnliche Workflows, deshalb wird im Verfahren zum Erstellen eines Updatepakets auf das Verfahren zum Erstellen von Updates verwiesen, und es werden nur die relevanten Unterschiede erläutert.

## <a name="use-the-create-update-wizard"></a>Verwenden des Assistenten zum Erstellen von Updates
1. Wechseln Sie in der Konsole zum **Arbeitsbereich „Updates“** , und wählen Sie dann im Bereich **Erste Schritte** auf der Registerkarte **Start** des Menübands die Option **Update** aus. Daraufhin wird der Assistent **Update erstellen** geöffnet.

2. Verwenden Sie die folgenden Informationen auf der Seite **Paket**, um das Update zu konfigurieren:

   -   Wählen Sie **Durchsuchen** aus, um nach dem Softwareupdatepaket zu suchen, das Sie als Paketquelle verwenden. Gültige Quellen sind MSI-, MSP- oder EXE-Dateien. Updates Publisher erfordert Zugriff auf die Datei, um einen Dateihash zu erstellen. Der Hash und die Datei werden anschließend in den Updatemetadaten für das Update verwendet, das Sie erstellen.

   -   Geben Sie den Quellspeicherort des Inhalts für dieses Update an. Normalerweise ist dies der Speicherort, in den die Updatebinärdatei während der Veröffentlichung auf einem WSUS-Server heruntergeladen wird.  Wenn die Option **Lokale Quelle zum Veröffentlichen von Softwareupdateinhalt verwenden** ausgewählt ist, ist der Pfad nicht erforderlich.

       Später, wenn das Update auf einem WSUS-Server veröffentlicht wird, lädt Updates Publisher die Binärdateien für das Update vom angegebenen Quellspeicherort herunter.  Wenn kein Pfad angegeben ist, durchsucht Updates Publisher den [Veröffentlichungspfad für lokale Quellen](updates-publisher-options.md#advanced) nach der Updatebinärdatei.

   -   Geben Sie die **Binärsprache** des Softwareupdates an.

   -   Geben Sie **Rückgabecodes bei Erfolg** und **Rückgabecodes bei Erfolg mit ausstehendem Neustart** für das Update an. Trennen Sie mehrere Rückgabecodes durch ein Komma. Sie können mithilfe von Rückgabecodes ermitteln, ob eine Updateinstallation erfolgreich war und ob Neustarts erforderlich waren.

       -   Windows-Installerdateien und -Patches (MSI- und MSP-Dateien) legen diese Werte automatisch fest, und diese können nicht geändert werden.

       -   Für EXE-Updates werden die von der EXE-Datei definierten Standardcodes verwendet, wenn keine Rückgabecodes angegeben wurden.

   -   Geben Sie etwaige Befehlszeilenargumente an, die zum Installieren des Softwareupdates erforderlich sind.

       -   Windows-Installerdateien und -Patches (MSI- und MSP-Dateien) legen diese Werte automatisch fest. Für diese Dateitypen müssen die Argumente in der Form **\[Name\]=\[Wert\]** angegeben werden. Alle Optionen, die mit **/** (wie z.B. **/qn**) beginnen, werden für MSI- und MSP-Softwareupdates nicht unterstützt.

       -   Für EXE-Updates sind alle Argumente gültig.

3. Geben Sie auf der Seite **Informationen** Details zum Update an, die beim Veröffentlichen oder Exportieren des Updates eingeschlossen werden. Zu den Details gehören lokalisierte Eigenschaften wie beispielsweise der Updatename (Titel) und eine Beschreibung. Anschließend geben Sie allgemeinere Details an, z.B. Klassifizierung, Anbieter, Produkt und einen Hinweis darauf, wo weitere Informationen zum Update bereitgestellt werden.

    __Lokalisierte Eigenschaften:__

   - **Sprache**: Wählen Sie eine Sprache aus, und geben Sie dann einen Titel und eine Beschreibung an. Sie können anschließend (nacheinander) zusätzliche Sprachen auswählen, wobei für jede Sprache ein eigener Titel und eine eigene Beschreibung unterstützt wird.

   - **Titel**: Geben Sie den Namen des Updates ein. Dieser Name wird im Arbeitsbereich „Updates“ der Updates Publisher-Konsole angezeigt.

   - **Beschreibung**: Eine Beschreibung des Updates. Sie können beispielsweise angeben, welche Komponenten mit dem Update installiert werden, und warum oder wann das Update verwendet werden sollte.

   **Klassifizierung:** Nachfolgend finden Sie gängige Beschreibungen für die verschiedenen Klassifizierungen.

   - **Update**: Ein Update für eine aktuell installierte Anwendung oder Datei.

   - **Kritisch**: Ein in großem Umfang freigegebenes Update für ein bestimmtes Problem, mit dem ein kritischer, nicht sicherheitsrelevanter Fehler behoben wird.

   - **Feature Pack**: Neue Produktfunktionen, die außerhalb einer Produktversion verteilt werden und in der Regel in der nächsten vollständigen Produktversion enthalten sind.

   - **Sicherheit**: Ein in großem Umfang freigegebenes Update für ein produktspezifisches, sicherheitsrelevantes Problem.

   - **Updaterollup**: Ein kumulativer Satz an Hotfixes, die für eine einfachere Bereitstellung gebündelt sind. Diese Hotfixes können Sicherheitsupdates, wichtige Updates, Updates usw. umfassen. Ein Aktualisierungsrollup betrifft in der Regel einen bestimmten Bereich, z.B. die Sicherheit oder ein Produktfeature.

   - **Service Pack**: Ein kumulativer Satz an Hotfixes, die auf eine Anwendung angewendet werden. Diese Hotfixes können Sicherheitsupdates, wichtige Updates, Softwareupdates usw. umfassen.

   - **Tool**: Gibt ein Dienstprogramm oder Feature an, das bei der Durchführung einer oder mehrerer Aufgaben hilft.

   - **Treiber**: Ein Update für die Treibersoftware.

   **Anbieter**: Geben Sie einen Anbieter für das Update an. Sie können mithilfe der Dropdownliste Werte aus Updates verwenden, die sich im Repository befinden. Wenn Sie einen Anbieter angeben, erstellt der Assistent einen Ordner mit dem Anbieternamen unter **Alle Softwareupdates** im **Arbeitsbereich „Updates“** , sofern dieser Ordner noch nicht vorhanden ist. Die nachfolgenden Namen sind reservierte WSUS-Namen (Windows Server Updates Services), die nicht für von Ihnen erstellte Updates verwendet werden können:
   - Microsoft Corporation
   - Microsoft
   - Update
   - Softwareupdate
   - Extras
   - Tool
   - Kritisch
   - Wichtige Updates
   - Sicherheit
   - Sicherheitsupdates
   - Feature Pack
   - Updaterollup
   - Service Pack
   - Treiber
   - Treiberupdate
   - Paket
   - Paketupdate

   **Produkt**: Geben Sie die Art des Produkts an, für das das Update vorgesehen ist. Sie können mithilfe der Dropdownliste Werte aus Updates verwenden, die sich im Repository befinden. Die Liste der für WSUS reservierten Namen, die nicht für **Anbieter** verwendet werden können, gilt auch für **Produkt**.

   **URL mit weiteren Informationen**: Geben Sie die URL an, über die weitere Informationen zu diesem Update bereitgestellt werden. Sie müssen Kleinbuchstaben für **https** oder **http** verwenden, wenn Sie diese URL eingeben.

4. Auf der Seite **Optionale Informationen** können Sie Details mit zusätzlichen Informationen zum Update konfigurieren.

   -   **Bulletin-ID**: Bulletin-IDs werden üblicherweise, aber nicht immer, durch die Updateanbieter bereitgestellt.

   -   **Artikel-ID**: Wenn ein Artikel zum Softwareupdate verfügbar ist, kann die Artikel-ID nützlich für Benutzer sein, die zusätzliche Informationen zum Update suchen.

   -   **CVE-IDs**: Eine Liste der CVE-IDs (Common Vulnerabilities and Exposures), die Sicherheitsinformationen zum Update oder Updatepaket bereitstellen. Trennen Sie mehrere Einträge durch ein Semikolon, wie in diesem Beispiel: *CVE1;CVE2*.

   -   **Support-URL**: Geben Sie die URL an, über die Supportinformationen für dieses Update bereitgestellt werden (sofern verfügbar). Sie müssen Kleinbuchstaben für **https** oder **http** verwenden, wenn Sie diese URL eingeben.

   -   **Schweregrad**: Hiermit wird der Schweregrad für dieses Update festgelegt.

   -   **Auswirkung**: Die folgenden Optionen können verwendet werden, um die Auswirkung anzugeben:
       -   **Normal**: Verwenden Sie diesen Wert, um anzugeben, dass das Update typische Installationsverfahren erfordert.
       -   **Gering**: Verwenden Sie diesen Wert, um anzugeben, dass das Update minimale Installationsverfahren erfordert.
       -   **Erfordert exklusive Handhabung**: Verwenden Sie diesen Wert, um anzugeben, dass das Update separat von anderen Updates installiert werden muss.   <br /><br />

   -   **Neustartverhalten**: Verwenden Sie diesen Wert, um Informationen zum Neustartverhalten anzugeben. Diese Einstellung hat keine Auswirkung auf das tatsächliche Verhalten der Updateinstallation.

       -   **Nie neu starten**: Der Computer führt nach dem Installieren des Softwareupdates niemals einen Neustart durch.
       -   **Neustart immer erforderlich**: Der Computer führt nach dem Installieren des Softwareupdates immer einen Systemneustart durch.
       -   **Neustart kann angefordert werden**: Nach dem Installieren des Softwareupdates fordert der Computer nur dann einen Neustart an, wenn dieser erforderlich ist. Der Benutzer hat die Möglichkeit, den Neustart zu verschieben. Dies ist der Standardwert. <br /><br />

5. Geben Sie auf der Seite **Voraussetzung** die erforderlichen Komponenten an, die auf dem Computer installiert werden müssen, bevor dieses Update installiert werden kann. Erforderliche Komponenten können **Detectoids** oder andere Updates sein. Detectoids sind Regeln hoher Ebene, z.B. die Anforderung, dass es sich bei der Computer-CPU um einen 64-Bit-Prozessor handeln muss. Detectoids können auch angeben, dass bestimmte Updates installiert sein müssen, bevor dieses Update installiert werden kann.

   -   Verwenden Sie für eine bessere Leistung Detectoids, statt Regeln für *installierbare* und *installierte Elemente* zu erstellen, die dieselbe Überprüfung oder Aktion ausführen.

   Verwenden Sie die Suchoption für **verfügbare Softwareupdates und Detectoids**, um bestimmte Updates oder Detectoids zu finden. Suchen Sie beispielsweise nach **CPU**, um die Detectoids zu finden, mit der Sie die Installation basierend auf einer bestimmten CPU-Architektur einschränken können.

   Sie können in einem Arbeitsschritt mehrere Elemente als Voraussetzung hinzufügen. Beim Hinzufügen von Voraussetzungen werden die ausgewählten Detectoids als eine oder mehrere Gruppen hinzugefügt. Zur Qualifizierung für eine Installation muss ein Computer die Anforderung mindestens eines Mitglieds jeder konfigurierten Gruppe erfüllen:

   -   Wenn Sie auf **Voraussetzung hinzufügen** klicken, werden alle ausgewählten Elemente in einzelnen getrennten Gruppen hinzugefügt. Um sich für dieses Update zu qualifizieren, muss ein Computer die Voraussetzung in dieser Gruppe erfüllen und den Anforderungen für alle weiteren konfigurierten Gruppen entsprechen.

   -   Wenn Sie auf **Gruppe hinzufügen** klicken, werden alle ausgewählten Elemente einer einzelnen Gruppe hinzugefügt. Um sich für dieses Update zu qualifizieren, muss ein Computer mindestens eine der Voraussetzungen in dieser Gruppe erfüllen und den Anforderungen für alle weiteren konfigurierten Gruppen entsprechen.

6. Geben Sie auf der Seite **Ablösung** die Updates an, die durch dieses Update ersetzt (abgelöst) werden. Wenn dieses Update veröffentlicht wird, markiert Configuration Manager jedes abgelöste Update als **Abgelaufen**. Clients installieren dann dieses Update anstelle des abgelösten Updates.

7. Verwenden Sie den **Regel-Editor** auf der Seite **Anwendbarkeit**, um einen Satz an Regeln zu definieren, die bestimmen, ob ein Gerät das Update benötigt. (Diese Seite ähnelt der Seite **Installiert**, die auf die Seite folgt.)

   Um eine neue Regel hinzuzufügen, klicken Sie auf ![„Neue Regel“](media/newrule.png). Daraufhin wird die Seite „Anwendbarkeitsregel“ geöffnet, auf der Sie Regeln konfigurieren können.

   Sie können u.a. die folgenden Arten von Regeln erstellen:

   -   **Datei**: Verwenden Sie diese Regel, wenn ein Gerät über eine Datei mit Eigenschaften verfügen muss, die ein oder mehrere Kriterien erfüllen, die Sie angeben, bevor dieses Update angewendet werden kann.

   -   **Registrierung**: Verwenden Sie diesen Typ, um Registrierungsinformationen anzugeben, die vorliegen müssen, bevor ein Gerät dieses Update installieren kann.

   -   **System**: Diese Regel bestimmt die Anwendbarkeit mithilfe von Systemdetails. Sie können wählen zwischen der Definition einer Windows-Version, einer Windows-Sprache und einer Prozessorarchitektur sowie dem Angeben einer WMI-Abfrage, um das Betriebssystem des Geräts zu identifizieren.

   -   **Windows Installer**: Verwenden Sie diesen Regeltyp, um die Anwendbarkeit basierend auf einem installierten MSI- oder Windows Installer-Patch (MSP) zu bestimmen. Sie können auch bestimmen, ob bestimmte Komponenten oder Funktionen als Teil der Anforderung installiert sind.

       > [!IMPORTANT]  
       > Auf verwalteten Geräten kann der Windows Update-Agent keine Windows Installer-Pakete erkennen, die auf Pro-Benutzer-Basis installiert sind. Wenn Sie diesen Regeltyp verwenden, konfigurieren Sie zusätzliche Anwendbarkeitsregeln wie Dateiversionen oder Registrierungsschlüsselwerte, damit das Windows Installer-Paket unabhängig von einer Pro-Benutzer- oder Pro-System-Basis ordnungsgemäß erkannt werden kann.

   -   **Gespeicherte Regel**: Mit dieser Option können Sie Regeln suchen und verwenden, die Sie *im Arbeitsbereich „Regeln“ erstellt haben*.

       Nachdem Sie eine Regel erstellt haben, können Sie die weiteren Symbole zum Ändern der Regel verwenden. Wenn mehrere Regeln vorliegen, können Sie hierüber außerdem die Beziehungen zwischen diesen Regeln definieren.

   Wenn Sie alle gewünschten Regeln erstellt und hinzugefügt haben, klicken Sie im Dialogfeld **Regelsatz erstellen** auf **OK**, um diesen Satz zu speichern. Sie können anschließend eine **neue** Regel erstellen und diese ebenfalls zum Satz hinzufügen.

   Wenn Sie über mehrere Regeln oder Regelsätze verfügen, die einem Update hinzugefügt werden sollen, können Sie die logischen Operatoren im **Regel-Editor** verwenden, um Bedingungen zwischen den Regeln sowie die Reihenfolge der Verarbeitung festzulegen.

8. Verwenden Sie den **Regel-Editor** auf der Seite **Installiert**, um einen Satz an Regeln zu definieren, mit dem bestimmt wird, ob ein Gerät das von Ihnen konfigurierte Update bereits installiert hat. (Diese Seite ähnelt der Seite **Anwendbarkeit**, die dieser Seite vorangeht.)

   Auf dieser Seite des Assistenten können Regeln mit denselben Optionen und Kriterien wie auf der Seite **Anwendbarkeit** konfiguriert werden.

   Wenn der Assistent abgeschlossen wird, wird das neue Update zu einem Knoten im **Arbeitsbereich „Updates“** hinzugefügt, der durch die Namen für **Anbieter** und **Produkt** identifiziert wird, die Sie für dieses Update verwendet haben.

## <a name="use-the-create-bundle-wizard"></a>Verwenden des Assistenten zum Erstellen von Paketen
Dieser Assistent verwendet denselben Workflow wie der [Assistent zum Erstellen von Updates](#use-the-create-update-wizard). Verwenden Sie deshalb diesen Workflow, aber berücksichtigen Sie die folgenden Unterschiede für Pakete:

1.  Um den Assistenten zu starten, wechseln Sie in der Konsole zum **Arbeitsbereich „Updates“** , und wählen Sie dann auf der Registerkarte **Start** im Menüband die Option **Paket** aus.

2.  Im Gegensatz zum Assistenten zum Erstellen von Updates ist beim Erstellen eines Pakets keine Seite „Paket“ vorhanden.

3.  Geben Sie auf der Seite **Informationen** Details zum Updatepaket an, die beim Veröffentlichen oder Exportieren des Updates eingeschlossen werden.

4.  Auf der Seite **Optionale Informationen** können Sie Details mit zusätzlichen Informationen zum Updatepaket konfigurieren. Die verfügbaren Optionen sind dieselben wie beim Erstellen eines Updates. Es stehen jedoch keine Optionen für Auswirkung und Neustartverhalten zur Verfügung, weil diese auf Pakete nicht anwendbar sind.

5.  Geben Sie auf der Seite **Voraussetzung** die erforderlichen Komponenten an, die auf dem Computer installiert werden müssen, bevor dieses Paket installiert werden kann. Diese Regeln sind dieselben wie für einzelne Updates.

6.  Geben Sie auf der Seite **Ablösung** die Updates an, die durch dieses Updatepaket ersetzt (abgelöst) werden. Diese Regeln sind dieselben wie für einzelne Updates.

7.  Auf der Seite **Mitglieder** wählen Sie die Updates aus, die dem Updatepaket hinzugefügt werden sollen. Es sind nur Updates verfügbar, die Sie in Updates Publisher erstellt oder dorthin importiert haben.

Wenn der Assistent abgeschlossen wird, wird das neue Updatepaket zu einem Knoten im **Arbeitsbereich „Updates“** hinzugefügt, der durch den Wert des Namens **Anbieter** identifiziert wird, den Sie für dieses Updatepaket verwendet haben.
