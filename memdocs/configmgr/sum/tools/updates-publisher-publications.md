---
title: Verwalten von Veröffentlichungen
titleSuffix: Configuration Manager
description: Verwalten von Softwareupdates als Veröffentlichung mit System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b79e0ec67fa7c1d7ede0af1549c8cda4dd3ee3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700038"
---
# <a name="manage-publications-in-updates-publisher"></a>Verwalten von Veröffentlichungen in Updates Publisher

*Gilt für: System Center Updates Publisher*

Sie können Veröffentlichungen zum Verwalten von Update- und Paketgruppen als einzelnes Objekt verwenden. Dazu gehört das Veröffentlichen der Updates auf einem Verwaltungsserver und das Exportieren der Veröffentlichung als Gruppe für die Verwendung mit einer anderen Installation von Updates Publisher.

## <a name="create-publications"></a>Erstellen von Veröffentlichungen
Veröffentlichungen werden auf zwei Arten erstellt:

-   Bei der Verwaltung von Updates und Paketen im **Arbeitsbereich „Updates“** können Sie diese einer neuen Veröffentlichung [zuweisen](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication), die zu diesem Zeitpunkt erstellt wird.

-   Im **Arbeitsbereich „Veröffentlichungen“** können Sie die Schaltfläche **Erstellen** auf der Registerkarte **Veröffentlichung** des Menübands verwenden. Mit dieser Methode können Sie eine Veröffentlichung zur zukünftigen Verwendung erstellen. Wenn Sie später Updates zuweisen, können Sie diese Veröffentlichung verwenden.

## <a name="rename-a-publication"></a>Umbenennen einer Veröffentlichung
Um eine Veröffentlichung umzubenennen, wählen Sie die Veröffentlichung im **Arbeitsbereich „Veröffentlichungen“** aus, und wählen Sie dann auf der Registerkarte **Veröffentlichung** des Menübands **Bearbeiten** aus.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Ändern des Veröffentlichungstyps von Updates in einer Veröffentlichung
Vom **Arbeitsbereich „Veröffentlichungen“** aus können Sie den **Veröffentlichungstyp** von Updates und Paketen ändern, die einer Veröffentlichung zugeordnet sind.

1. Wählen Sie die Veröffentlichung aus, die die Updates enthält, die Sie ändern möchten, und wählen Sie ein oder mehrere Updates bzw. Pakete aus der Liste **All &lt;Publikationsname> member updates** (Alle <Publikationsname>-Mitgliedupdates).

2. Wählen Sie dann auf der Registerkarte **Start** eine der folgenden Optionen aus. Die verfügbaren Optionen richten sich nach dem Veröffentlichungstyp der Updates, die Sie ausgewählt haben.

   -   **Automatisch**
   -   **Vollständiger Inhalt**
   -   **Nur Metadaten**

Nach einer Änderung müssen Sie die Veröffentlichungsansicht aktualisieren, um die neuen Werte anzuzeigen.

Informationen zu den verschiedenen Veröffentlichungstypen finden Sie unter [Assign updates and bundles to a publication](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) (Zuweisen von Updates und Paketen zu einer Veröffentlichung).

> [!TIP]    
> Wenn Sie den Veröffentlichungstyp eines Pakets festlegen, werden alle Softwareupdates in dem Paket mit dem Veröffentlichungstyp dieses Pakets veröffentlicht.

## <a name="remove-updates-from-a-publication"></a>Entfernen von Updates aus einer Veröffentlichung
Um Updates oder Pakete aus einer Veröffentlichung zu entfernen, wählen Sie im **Arbeitsbereich „Veröffentlichungen“** die Veröffentlichung aus, die Sie ändern möchten, und wählen Sie dann die Updates und Pakete aus, die Sie entfernen möchten. Wählen Sie als Nächstes auf der Registerkarte **Start** des Menübands **Entfernen** aus.

Nachdem Updates aus einer Veröffentlichung entfernt worden sind, bleiben sie im Updates Publisher-Repository verfügbar.

## <a name="publish-publications"></a>Veröffentlichen von Veröffentlichungen
Bei der Veröffentlichung von Updates und Paketen fügt Updates Publisher Informationen (Metadaten) zu diesen Updates und Paketen und möglicherweise Binärdateien für die Updates (vollständiger Inhalt) einem Updateserver zur Bereitstellung auf Geräten hinzu.

Damit die Option zum Veröffentlichen angezeigt wird, müssen Sie die Option [Updateserver](updates-publisher-options.md#update-server) für Updates Publisher konfigurieren. Um diese Konfigurationsoption zu öffnen, wechseln Sie zum **Arbeitsbereich „Updates“** &gt; **Übersicht**, und wählen Sie **WSUS-Server und Signaturzertifikat konfigurieren** aus. Sie können auch in den Updates Publisher-Optionen zur Seite „Updateserver“ wechseln.

> [!NOTE]   
> Updates Publisher kann nur Updates mit einer Größe von max. 375 Megabyte (MB) veröffentlichen.

### <a name="to-publish-a-publication"></a>So veröffentlichen Sie eine Veröffentlichung

1. Wechseln Sie zum **Arbeitsbereich „Veröffentlichungen“** , und wählen Sie dann eine Veröffentlichung aus, die die Gruppe von Updates und Paketen enthält, die Sie veröffentlichen oder exportieren möchten. Wählen Sie dann auf der Registerkarte **Start** des Menübands die Option **Veröffentlichen**.

2. Auf der Seite **Auswählen** des **Veröffentlichungs**-Assistenten können Sie wählen, alle Updates mit einem neuen Veröffentlichungszertifikat zu signieren, aber Sie können den Veröffentlichungstyp nicht ändern.

3. Schließen Sie den Assistenten ab.

   Wenn bei der Veröffentlichung ein Fehler auftritt, wird ein Link zur UpdatesPublisher.log-Datei angezeigt, die weitere Informationen bereitstellen kann.

## <a name="export-a-publication"></a>Exportieren einer Veröffentlichung
Sie können eine Veröffentlichung aus Ihrem Updates Publisher-Repository exportieren. Auf diese Weise werden die Updates und Pakete exportiert, die dieser Veröffentlichung zugewiesen sind, und ein Updatekatalog erstellt. Anschließend können Sie diesen Katalog [hinzufügen](updates-publisher-catalogs.md#add-software-update-catalogs) und dann in eine andere Instanz von Updates Publisher [importieren](updates-publisher-catalogs.md#import-updates). Sie können auch [Updates exportieren](manage-updates-with-updates-publisher.md#export-updates), die nicht Teil einer Veröffentlichung sind.

Um eine Veröffentlichung zu exportieren, wechseln Sie zum **Arbeitsbereich „Veröffentlichungen“** , und wählen Sie die Veröffentlichung aus, die Updates enthält, die Sie exportieren möchten. Sie können nur jeweils eine Veröffentlichung auswählen.

Wählen Sie nach der Veröffentlichungenauswahl auf der Registerkarte **Start** des Menübands die Option **Exportieren**, und geben Sie dann einen Pfad und Dateinamen für den Katalogexport an.

Sie können auch abhängige Softwareupdates als Teil des Exports exportieren (einzuschließen).

## <a name="rename-a-publication"></a>Umbenennen einer Veröffentlichung
Um eine Veröffentlichung umzubenennen, wählen Sie die Veröffentlichung im **Arbeitsbereich „Veröffentlichungen“** aus, und wählen Sie dann auf der Registerkarte **Veröffentlichung** des Menübands **Bearbeiten** aus.

## <a name="delete-a-publication"></a>Löschen einer Veröffentlichung
Um eine Veröffentlichung zu löschen, wählen Sie die Veröffentlichung im **Arbeitsbereich „Veröffentlichungen“** aus, und wählen Sie dann auf der Registerkarte **Veröffentlichung** des Menübands **Löschen** aus.

Wenn die Veröffentlichung aus Updates Publisher entfernt worden ist, bleiben die Updates, die sich in der Veröffentlichung befanden, im Updates Publisher-Repository verfügbar.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Ablaufen oder erneutes Aktivieren von Updates und Paketen
Sie können im **Arbeitsbereich „Updates“** Updates und Pakete auswählen und dann ablaufen lassen oder erneut aktivieren. Sie können Updates und Pakete so oft wie gewünscht ablaufen lassen und erneut aktivieren.

-   **Um Updates oder Pakete ablaufen zu lassen**, wählen Sie im „Arbeitsbereich „Updates““ ein oder mehrere Updates oder Pakete aus, die nicht abgelaufen sind, und wählen Sie dann **Ablaufen** auf der Registerkarte **Start**. Bis Sie das Update oder Paket als abgelaufen im Configuration Manager veröffentlichen, können Sie es erneut aktivieren.

    Bevor Sie ein benutzerdefiniertes Update oder Paket aus dem Configuration Manager entfernen (löschen) können, müssen Sie es ablaufen lassen und dann den abgelaufenen Status im Configuration Manager veröffentlichen. Nachdem Updates oder Pakete im Configuration Manager abgelaufen sind, können Sie sie nicht mehr bereitstellen oder erneut aktivieren.

-   **Um Updates oder Pakete erneut zu aktivieren**, wählen Sie im „Arbeitsbereich „Updates““ ein oder mehrere Updates oder Pakete aus, die abgelaufen sind, und wählen Sie dann **Erneut aktivieren** auf der Registerkarte **Start**. Wenn das abgelaufene Update zuvor als abgelaufen im Configuration Manager veröffentlicht wurde, kann es nicht erneut aktiviert werden.
