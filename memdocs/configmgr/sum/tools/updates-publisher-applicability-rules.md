---
title: Anwendbarkeitsregeln
titleSuffix: Configuration Manager
description: Verwalten von Anwendbarkeitsregeln für System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2a3d810fa2a3b8630b50b702e03ab9666661560d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700148"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Verwalten von Anwendbarkeitsregeln in Updates Publisher

*Gilt für: System Center Updates Publisher*

In Updates Publisher definieren Anwendbarkeitsregeln Anforderungen, die erfüllt sein müssen, bevor ein Gerät ein Update installieren kann. Mit den Regeln wird auch bestimmt, ob auf dem Computer ein Update installiert wurde. Eine komplexe Anwendbarkeitsregel mit mehreren Teilen wird als Regelsatz bezeichnet.

Updatepakete verwenden keine Anwendbarkeitsregeln.

## <a name="overview-of-applicability-rules"></a>Übersicht der Anwendbarkeitsregeln
Sie verwalten Anwendbarkeitsregeln vom **Arbeitsbereich „Regeln“** aus. Wenn Sie eine Regel erstellen, legen Sie mindestens eine Bedingung fest. Wenn mehrere Bedingungen angegeben werden, können Sie Beziehungen zwischen den Bedingungen konfigurieren, damit diese nacheinander ausgewertet oder in logischen **And**- oder **Or**-Anweisungen zusammengefasst werden.

Der folgende Regelsatz enthält z.B. drei Regeln. Die erste Regel überprüft, ob die *MyFile*-Datei vorhanden ist, und die zweite und dritte Regel stellen sicher, dass die Sprache des Windows-Betriebssystems entweder Englisch oder Japanisch ist.

``` Example
And  
  File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Alle Updates erfordern mindestens eine Anwendbarkeitsregel. Auf Updates, die Sie bereits importiert haben, sind Anwendbarkeitsregeln angewendet worden, und wenn Sie eigene Updates erstellen, müssen Sie eine oder mehrere Regeln hinzufügen. Sie können die Regeln für jedes Update in Updates Publisher ändern und erweitern.

Um Regeln anzuzeigen, die Sie erstellt haben, wählen Sie im **Arbeitsbereich „Regeln“** eine Regel aus der Liste **My saved rules** (Eigene gespeicherte Regeln). Die einzelnen Bedingungen und logischen Operationen für diese Regel werden im Bereich **Anwendbarkeitsregeln** der Konsole angezeigt. Regeln für Updates, die Sie importieren, können nur angezeigt und geändert werden, wenn Sie das Update bearbeiten.

Sie können an zwei Orten in Updates Publisher Regeln erstellen:

-   Im **Arbeitsbereich „Regeln“** erstellen und **speichern** Sie Regelsätze, die Sie später verwenden können. Beim Bearbeiten oder Erstellen eines Updates können Sie **Gespeicherte Regel** als **Regeltyp** auswählen und dann in einer Liste Ihrer zuvor erstellten Regelsätze Ihre Auswahl treffen.

-   Sie können auch neue Regeln erstellen, wenn Sie ein Update erstellen oder bearbeiten. Auf diese Weise erstellte Regeln werden nicht für die zukünftige Verwendung gespeichert.

## <a name="create-applicability-rule"></a>Erstellen einer Anwendbarkeitsregel
Die folgenden Informationen entsprechen denen zum Erstellen von Regeln im [Create Update wizard](create-updates-with-updates-publisher.md#use-the-create-update-wizard) (Updateerstellungs-Assistenten). Aber im Gegensatz zum Assistenten haben Sie die Möglichkeit, Ihre Regelsätze für die zukünftige Verwendung zu speichern.

1. Wählen Sie im **Arbeitsbereich „Regeln“** **Erstellen**, um den **Regel erstellen**-Assistenten zu öffnen.

2. Geben Sie einen Namen für die Regel ein, und klicken Sie dann auf ![Neue Regel](media/newrule.png). Daraufhin wird die Seite **Anwendbarkeitsregel** geöffnet, wo Sie Regeln konfigurieren können.

3. Wählen Sie für **Regeltyp** eine der folgenden Einstellungen aus. Die Optionen, die Sie konfigurieren müssen, variieren je nach Typ:

   - **Datei**: Verwenden Sie diese Regel, wenn ein Gerät über eine Datei mit Eigenschaften verfügen muss, die ein oder mehrere Kriterien erfüllen, die Sie angeben, bevor dieses Update angewendet werden kann.

   - **Registrierung**: Verwenden Sie diesen Typ, um Registrierungsinformationen anzugeben, die vorliegen müssen, bevor ein Gerät dieses Update installieren kann.

   - **System**: Diese Regel bestimmt die Anwendbarkeit mithilfe von Systemdetails. Sie können wählen zwischen der Definition einer Windows-Version, einer Windows-Sprache und einer Prozessorarchitektur sowie dem Angeben einer WMI-Abfrage, um das Betriebssystem des Geräts zu identifizieren.

   - **Windows Installer**: Verwenden Sie diesen Regeltyp, um die Anwendbarkeit basierend auf einem installierten MSI- oder Windows Installer-Patch (MSP) zu bestimmen. Sie können auch bestimmen, ob bestimmte Komponenten oder Funktionen als Teil der Anforderung installiert sind.

     > [!IMPORTANT]   
     > Auf verwalteten Geräten kann der Windows Update-Agent keine Windows Installer-Pakete erkennen, die auf Pro-Benutzer-Basis installiert sind. Wenn Sie diesen Regeltyp verwenden, konfigurieren Sie zusätzliche Anwendbarkeitsregeln wie Dateiversionen oder Registrierungsschlüsselwerte, damit das Windows Installer-Paket unabhängig von einer Pro-Benutzer- oder Pro-System-Basis ordnungsgemäß erkannt werden kann.

   - **Gespeicherte Regel**: Mit dieser Option können Sie Regeln suchen und verwenden, die Sie zuvor konfiguriert und gespeichert haben.

4. Fahren Sie fort, zusätzliche Regeln nach Bedarf hinzuzufügen und zu konfigurieren.

5. Verwenden Sie die Schaltflächen für logische Operationen, um unterschiedliche Regeln anzuordnen und zu gruppieren, um komplexere Voraussetzungsprüfungen zu erstellen.

6. Wenn der Regelsatz abgeschlossen ist, klicken Sie zum Speichern auf **OK**. Der Regelsatz wird jetzt in der Liste **My saved rules** (Eigene gespeicherte Regeln) angezeigt.

## <a name="edit-applicability-rule-sets"></a>Bearbeiten von Anwendbarkeitsregelsätzen
Um eine Anwendbarkeitsregel zu bearbeiten, wählen Sie im **Arbeitsbereich „Regeln“** eine in der Liste **My saved rules** (Eigene gespeicherte Regeln) gespeicherte Regel aus, und wählen Sie dann im Menüband **Bearbeiten**. Daraufhin wird der **Regel bearbeiten**-Assistent geöffnet.

Der **Regel bearbeiten**-Assistent zeigt die aktuellen Regeln für den Regelsatz an. Sie bearbeiten Regeln auf die gleiche Weise, wie Sie den **Regel erstellen**-Assistenten verwenden, um neue Regeln zu erstellen. Mit diesem Assistenten können Sie den Regelsatz umbenennen, Regeln löschen, Regeln und Beziehungen neu anordnen oder neue Regeln hinzufügen.

Nachdem Sie Änderungen vorgenommen haben, wählen Sie **OK**, um die Änderungen zu speichern und den Assistenten zu schließen.

Weitere Informationen zum Verwenden des Regel-Assistenten finden Sie unter **Schritt 7**, der Anwendbarkeitsseite, des [Create Update wizard](create-updates-with-updates-publisher.md#use-the-create-update-wizard) (Updateerstellungs-Assistenten).

## <a name="delete-applicability-rules"></a>Löschen von Anwendbarkeitsregeln
Um eine gespeicherte Anwendbarkeitsregel zu löschen, wählen Sie im **Arbeitsbereich „Regeln“** die Regel bzw. den Regelsatz in der Liste **My saved rules** (Eigene gespeicherte Regeln) aus, und wählen Sie dann im Menüband **Löschen**. Dies entfernt die gespeicherte Regel bzw. den Regelsatz aus Updates Publisher.

Um eine Regel aus einem bestimmten Update zu löschen, müssen Sie [das Update bearbeiten](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).
