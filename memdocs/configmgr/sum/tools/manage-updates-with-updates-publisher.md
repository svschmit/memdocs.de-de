---
title: Verwalten von Updates
titleSuffix: Configuration Manager
description: Verwalten von mit System Center Updates Publisher bereitgestellten und erstellten Updates
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700188"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Verwalten von Softwareupdates in Updates Publisher

*Gilt für: System Center Updates Publisher*     

Im **Arbeitsbereich „Updates“** von System Center Updates Publisher verwalten Sie Softwareupdates und -pakete, die Sie in das Repository importiert haben.  

Zu den Verwaltungsaufgaben zählen das Duplizieren, Bearbeiten, Ablaufenlassen oder erneute Aktivieren von Updates und Paketen, sowie das Zuweisen von Updates und Paketen zu Veröffentlichungen. Sie können auch benutzerdefinierte Kataloge für die Verwendung mit anderen Updates Publisher-Installationen exportieren.

So rufen Sie Updates ab, die Sie verwalten können:
-  [Fügen Sie ein Updatekatalog](updates-publisher-catalogs.md#add-software-update-catalogs) zu Ihrer Updates Publisher-Installation hinzu.
-  [Importieren](updates-publisher-catalogs.md#import-updates) Sie die Updates aus diesem Katalog in Ihr Repository.

Sie können auch [eigene Updates erstellen](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Erstellen eines Duplikats von Updates
Sie können Duplikate oder Kopien von Updates, die sich in Ihrem Repository befinden, erstellen. Dann können Sie die Kopie anstelle des ursprünglichen Updates ändern. Sie können keine Kopien von Updatepaketen erstellen.

Um eine Kopie zu erstellen, wählen Sie ein Update im **Arbeitsbereich „Updates“** und anschließend **Duplizieren** aus. Die Kopie des Updates wird an derselben Stelle im Arbeitsbereich „Updates“ angezeigt, wobei der Name mit dem Zusatz *Kopie von* versehen ist.

Neue Kopien, die Sie erstellen, weisen den Status **Nicht abgelaufen** auf, behalten jedoch die Einstellungen des Originals bei.

## <a name="edit-updates-and-bundles"></a>Bearbeiten von Updates und Paketen
Sie können Updates und Pakete in Ihrem Repository auswählen, um diese zu ändern.

Wählen Sie im **Arbeitsbereich „Updates“** ein Update oder Paket aus, und anschließend **Bearbeiten** auf der Registerkarte **Start**, um den Bearbeitungsassistenten zu öffnen. Für Updates und Pakete stehen separate, aber eng verwandte Assistenten zur Verfügung, die dieselben Optionen aufweisen wie die Assistenten [Update erstellen](create-updates-with-updates-publisher.md#use-the-create-update-wizard) oder [Bündel erstellen](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard).

Bei der Bearbeitung können Sie alle verfügbaren Details zum Update oder Paket ändern, um sie in Ihrer Umgebung verwenden zu können. Beispielsweise können Sie die Regeln für die Anwendbarkeit oder Rangfolge bearbeiten, oder die Sprache ändern. Zudem können Sie das Produkt und den Anbieter ändern, um das Update oder das Paket in einen benutzerdefinierten Ordner zu verschieben und so Updates für den eigenen Gebrauch gruppieren.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Zuweisen von Updates und Paketen zu einer Veröffentlichung
Im **Arbeitsbereich „Updates“** können Sie Updates und Pakete auswählen und zum Hinzufügen zu einer Veröffentlichung anschließend auf der Registerkarte **Start** des Menübands die Option **Zuweisen** wählen. Daraufhin wird der Assistent **Softwareupdates zuweisen** gestartet.
-  Unter [Veröffentlichen von Updates und Paketen](#publish-updates-and-bundles-from-the-updates-workspace) finden Sie Informationen zum Auswählen und Veröffentlichen von Updates und Paketen als einzelne Aufgabe.
-  Informationen zum Verwalten von Update- und Paketgruppen als einzelnes Objekt finden Sie unter [Verwalten von Veröffentlichungen](updates-publisher-publications.md). Nachdem Sie einer Veröffentlichung Updates zugewiesen haben, können Sie diese Veröffentlichung verwalten, die wiederum alle zugewiesenen Updates enthält.

Bei der Zuweisung von Updates zu einer Veröffentlichung gilt Folgendes:

-   Sie können abgelaufene und nicht abgelaufene Updates und Pakete in derselben Veröffentlichung einschließen.

-   Legen Sie den Veröffentlichungstyp fest:

    -   **Vollständiger Inhalt** – Diese Option veröffentlicht den vollständigen Inhalt des Updates auf Ihrem WSUS-Server. Dazu gehören Metadaten und die Updatebinärdateien.

    -   **Nur Metadaten** – Diese Option veröffentlicht nur die Metadaten; Updatebinärdateien werden nicht veröffentlicht. Sie können diese Option auswählen, wenn Sie Kompatibilitätsinformationen sammeln möchten.

    -   **Automatisch** – Dieser Modus ist nur verfügbar, wenn Sie eine Verbindung zwischen Updates Publisher und Configuration Manager hergestellt haben (siehe [ConfigMgr-Server](updates-publisher-options.md#configmgr-server)-Option).

    Bei diesem Typ fragt Updates Publisher Configuration Manager ab, um festzustellen, ob die Updates oder Pakete mit vollständigem Inhalt oder nur mit Metadaten veröffentlicht werden sollen. Die vollständigen Inhalte eines Updates werden nur veröffentlicht, wenn dieses Update den **Schwellenwert für die geforderte Clientanzahl** und den **Schwellenwert für die Paketquellgröße** erfüllt, die auf der Seite **ConfigMgr-Server** der Updates Publisher-Optionen festgelegt werden.

-   Wählen Sie eine Veröffentlichung aus:

    -   Verwenden Sie die Option **Softwareupdate zu vorhandenen Veröffentlichungen** zuweisen, wenn Sie bereits eine Veröffentlichung erstellt haben, die Sie verwenden möchten. Diese Option ist erst verfügbar, wenn mindestens eine Veröffentlichung vorhanden ist.

    -   Verwenden Sie die Option **Softwareupdate einer neuen Veröffentlichung zuweisen**, wenn Sie keine geeignete Veröffentlichung besitzen. Daraufhin wird eine neue Veröffentlichung mit dem von Ihnen festgelegten Namen erstellt.

Nachdem Sie einer Veröffentlichung Updates zugewiesen haben, können Sie die Veröffentlichung über den **Arbeitsbereich „Veröffentlichung“** als Gruppe [veröffentlichen](updates-publisher-publications.md#publish-publications) oder [exportieren](updates-publisher-publications.md#export-a-publication).

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Veröffentlichen von Updates und Paketen über den Arbeitsbereich „Updates“
Bei der Veröffentlichung von Updates und Paketen fügt Updates Publisher Informationen zu diesen Updates und Paketen (Metadaten) und möglicherweise Binärdateien für die Updates (vollständiger Inhalt) zu einem Updateserver für die Bereitstellung auf Geräten hinzu.

Damit die Option zum Veröffentlichen angezeigt wird, müssen Sie die Option [Updateserver](updates-publisher-options.md#update-server) für Updates Publisher konfigurieren. Um diese Konfigurationsoption zu öffnen, wechseln Sie zum **Arbeitsbereich „Updates“** &gt; **Übersicht**, und wählen Sie **WSUS-Server und Signaturzertifikat konfigurieren** aus. Sie können auch in den Updates Publisher-Optionen zur Seite „Updateserver“ wechseln.

Es gibt zwei Möglichkeiten zum Veröffentlichen von Updates und Paketen:
-   Direkt über den Arbeitsbereich „Updates“ (siehe folgendes Verfahren zum *Veröffentlichen von Updates und Paketen*)
-   Als [Veröffentlichung](updates-publisher-publications.md#publish-publications) über den Arbeitsbereich „Veröffentlichungen“  

> [!NOTE]   
> Updates Publisher kann nur Updates mit einer Größe von max. 375 Megabyte (MB) veröffentlichen.

### <a name="to-publish-updates-and-bundles"></a>Veröffentlichen von Updates und Paketen
1.  Wechseln Sie zum **Arbeitsbereich „Updates“** , und wählen Sie ein oder mehrere Updates und Pakete aus, die Sie veröffentlichen möchten. Wählen Sie dann auf der Registerkarte **Start** des Menübands die Option **Veröffentlichen**.

2.  Wählen Sie auf der Seite **Auswählen** im **Veröffentlichungs-Assistenten** aus, wie die Updates veröffentlicht werden sollen. Die Optionen sind mit denen für die [Zuweisung von Updates](#assign-updates-and-bundles-to-a-publication) identisch: **Vollständiger Inhalt**, **Nur Metadaten** oder **Automatisch**.

    Sie können auch festlegen, dass alle Updates mit einem neuen Herausgeberzertifikat signiert werden.

3.  Schließen Sie den Assistenten ab.

Wenn die Veröffentlichung fehlschlägt, wird ein Link zur UpdatesPublisher.log-Datei angezeigt, die weitere Informationen bereitstellen kann.

## <a name="export-updates"></a>Exportieren von Updates
Sie können Updates und Pakete aus Ihrem Updates Publisher-Repository exportieren, um einen benutzerdefinierten Updatekatalog zu erstellen. Anschließend können Sie diesen Katalog [hinzufügen](updates-publisher-catalogs.md#add-software-update-catalogs) und dann in eine andere Instanz von Updates Publisher [importieren](updates-publisher-catalogs.md#import-updates). (Sie können [Updates auch als Veröffentlichung exportieren](updates-publisher-publications.md#export-a-publication).)

Navigieren Sie zum direkten Exportieren zum **Arbeitsbereich „Updates“**  > **Alle Softwareupdates**, und wählen Sie ein oder mehrere Updates und Pakete aus. Sie können keinen Anbieter- oder Produktordner exportieren, jedoch einen Ordner und anschließend die Updates in diesem Ordner für den Export auswählen.

Nachdem Sie ein oder mehrere Updates ausgewählt haben, wählen Sie auf der Registerkarte **Start** des Menübands die Option **Exportieren**, und geben Sie dann einen Pfad und Dateinamen für den Katalogexport an.

Sie haben dann die Option abhängige Softwareupdates zu exportieren (einzuschließen).

## <a name="delete-updates-and-bundles"></a>Löschen von Updates und Paketen
Sie können Updates und Pakete von Updates löschen, um sie aus dem Updates Publisher-Repository zu entfernen.

Navigieren Sie zum **Arbeitsbereich „Updates“**  > **Alle Softwareupdates**, und wählen Sie ein oder mehrere einzelne Updates aus. Wählen Sie dann auf der Registerkarte **Start** des Menübands die Option **Löschen**.

-   Wenn Ihre Auswahl nur Softwareupdates oder -pakete enthält, die nicht veröffentlicht wurden oder abgelaufen sind, werden Sie aufgefordert, den Löschvorgang zu bestätigen, bevor sie entfernt werden.

-   Wenn Ihre Auswahl ein Update oder ein Paket enthält, das veröffentlicht wurde und noch nicht abgelaufen ist, wird eine Warnung angezeigt. Bevor Sie Updates aus dem Repository löschen, sollten Sie diese [ablaufen](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) lassen und die Änderung dann veröffentlichen.  

Wenn Sie ein Update oder Paket von einem Anbieter löschen und diesen Katalog dann wieder importieren, wird dieses Update in Ihrem Repository wiederhergestellt.

## <a name="manage-vendor-and-product-folders"></a>Verwalten von Anbieter- und Produktordnern
Um eine Liste von Anbietern und Produkten für jeden Anbieter, für den Sie Updates importiert oder erstellt haben, anzuzeigen, navigieren Sie zum **Arbeitsbereich „Updates“**  > **Übersicht** > **Alle Softwareupdates**.

Ordner für Anbieter und Produkte werden automatisch von Updates Publisher erstellt, wenn Sie einen Assistenten zum Importieren oder Erstellen eines Softwareupdates oder -pakets verwenden. Sie können diese Ordner auch manuell erstellen.

-   Um einen Anbieterordner zu erstellen, klicken Sie im Navigationsbereich im **Arbeitsbereich „Updates“** mit der rechten Maustaste auf **Alle Softwareupdates**, und wählen Sie dann **Anbieter erstellen**.

-   Um einen Produktordner in einem Anbieterordner zu erstellen, klicken Sie mit der rechten Maustaste auf den Anbieterordner, und wählen Sie **Produkt erstellen** aus.

Neben der Erstellung von Ordnern können Sie einen beliebigen Anbieter- oder Produktordner in Ihrem Repository umbenennen oder löschen. Klicken Sie hierzu mit der rechten Maustaste auf den Ordner, und wählen Sie die gewünschte Option **Umbenennen** oder **Löschen** aus. Durch das Löschen eines Ordners werden alle Updates und Pakete in diesem Ordner und den jeweiligen Produktordnern aus dem Updates Publisher-Repository entfernt.

Sie können Updates zwischen Anbieter- und Produktordnern verschieben, einschließlich in die von Ihnen erstellten Ordner. Um ein Update oder ein Paket in einen neuen Ordner zu verschieben, müssen Sie das Update oder Paket auswählen und dann auf **Bearbeiten** klicken. Auf der Seite **Informationen** des Assistenten „Update bearbeiten“ können Sie dann den Anbieter und das Produkt neu zuweisen. Wenn der Assistent **Update bearbeiten** abgeschlossen ist, wird die Änderung angewendet und das Update wird in den neuen Ordner verschoben.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Anzeigen des XML-Codes eines Updates oder Pakets
Im **Arbeitsbereich „Updates“** können Sie ein einzelnes Update oder Paket auswählen, und dann auf **XML anzeigen** klicken, um die XML-Struktur dieses Updates anzuzeigen. Es sind keine Optionen zum direkten Bearbeiten der XML-Struktur vorhanden.
