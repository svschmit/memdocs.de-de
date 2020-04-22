---
title: Verwalten von Updatekatalogen
titleSuffix: Configuration Manager
description: Verwalten von Softwareupdatekatalogen für System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700128"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Verwalten von Softwareupdatekatalogen in Updates Publisher

*Gilt für: System Center Updates Publisher*

Verwenden Sie den **Arbeitsbereich** **Kataloge** zum Verwalten von Softwareupdatekatalogen. Hierzu gehört das Hinzufügen neuer Kataloge, Verwalten vorhandener Katalogabonnements und Importieren von Informationen zu den Updates aus einem Katalog in das Updates Publisher-Repository.

Softwareupdatekataloge enthalten Informationen über die zugehörigen Updates, die von anderen Organisationen als Microsoft erstellt werden. Zu anderen Organisationen zählen Ihre eigene Organisation und Drittanbieter-Softwarehersteller, die ihre Kataloge bei Microsoft registriert haben. Registrierte Kataloge von Softwareherstellern werden als *Partnerkataloge* bezeichnet. Von Ihnen erstellte Kataloge, die nicht bei Microsoft registriert sind, werden als *Benutzerkataloge* bezeichnet.

## <a name="add-software-update-catalogs"></a>Hinzufügen von Softwareupdatekatalogen
Sie müssen einen Updatekatalog zu Updates Publisher hinzufügen, bevor Sie die darin enthaltenen Updates verwalten können. Wenn Sie einen Katalog hinzufügen, führt Updates Publisher folgende Aktionen aus:
-   Erstellen eines Abonnements für diesen Katalog, um nach Updates dieses Katalogs zu suchen.
-   Hinzufügen des Katalogs zu einer Liste im Fenster **My Software Update Catalogs** (Eigene Softwareupdatekataloge) des **Arbeitsbereichs „Kataloge“** .  

Informationen zu jedem abonnierten Katalog sind in der Konsole verfügbar. Zu den Informationen zählen Download-URL oder -Speicherort, der Name des Unternehmens bzw. der Organisation, das bzw. die den Katalog erstellt hat, und wann er zuletzt importiert oder geändert wurde.

Updates Publisher kann automatisch bei jedem Start Ihre Abonnements auf Änderungen überprüfen. Dies wird als [Erweiterte Option](updates-publisher-options.md#advanced) konfiguriert. Sofern konfiguriert, referenziert Updates Publisher auf die Informationen zum Download-URL oder -Speicherort für das Abonnement und warnt Sie bei Änderungen des Katalogs, die vorgenommen wurden, seit Sie ihn zuletzt in das Repository importiert haben.

Um manuell nach einem Katalogupdate zu suchen, wählen Sie den Katalog in der Liste **My Software Update Catalogs** (Eigene Softwareupdatekataloge) aus, und wählen Sie dann im Menüband **Aktualisieren**.

Zusätzlich zum Hinzufügen von Katalogen und Anzeigen von Informationen zu abonnierten Kataloge können Sie folgende Aktionen ausführen:
-  **Bearbeiten** von Informationen für *Benutzerkataloge*.
-  **Löschen** (Entfernen) eines Katalogs aus Updates Publisher.
-  **Importieren** von Updates aus einem Katalog in das Updates Publisher-Repository. Wenn Sie Updates importieren, importieren Sie alle Updates, die im Katalog enthalten sind. Sie können dann die Updates im „Arbeitsbereich „Updates““ anzeigen, wo Sie dann Updates auswählen und auf Ihrem Updateserver veröffentlichen können.

> [!NOTE]   
> Beim Löschen eines Katalogs aus Updates Publisher werden die Updates in diesem Katalog aus Ihrem Repository entfernt. Dies betrifft nicht die Updates, die Sie auf Ihrem Updateserver veröffentlicht haben. Informationen zum Entfernen von Updates von Ihrem Updateserver, die sich nicht mehr in Ihrem Repository befinden, finden Sie unter [Ablaufen nicht referenzierter Softwareupdates](updates-publisher-options.md#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Verwalten von Updatekatalogen
Sie können die Listenkataloge, die Sie importiert haben, im Fenster **My Software Update Catalogs** (Eigene Softwareupdatekataloge) des **Arbeitsbereichs „Kataloge“** anzeigen. Von diesem Arbeitsbereich aus können Sie folgende Aktionen ausführen:

-   **Hinzufügen eines Partnerkatalogs**: Um neue Partnerkataloge zu finden, verwenden Sie eine der folgenden Methoden:

    -   Wechseln Sie in der Konsole zu **Arbeitsbereich „Updates“**  > **Übersicht**. Wählen Sie im **Erste Schritte**-Fenster **Add Partner Software Updates Catalogs** (Softwareupdatekataloge von Partnern hinzufügen).

    -   Wechseln Sie in der Konsole zu **Arbeitsbereich „Kataloge“**  > **My Catalogs** (Eigene Kataloge). Wählen Sie dann aus dem Menüband **Kataloge hinzufügen**.

-   **Hinzufügen eines Benutzerkatalogs**: Wechseln Sie in der Konsole zu **Arbeitsbereich „Kataloge“**  > **My Catalogs** (Eigene Kataloge). Wählen Sie dann aus dem Menüband **Kataloge hinzufügen**. Zusätzlich zum Speicherort der CAB-Datei müssen Sie einen Herausgeber, Namen und eine Beschreibung zum Identifizieren des Katalogs angeben.


-   **Check for updates to catalogs** (Nach Updates dieses Katalogs suchen): Wählen Sie einen oder mehrere Kataloge aus, und wählen Sie dann **Aktualisieren** aus dem Menüband.

-   **Bearbeiten eines Benutzerkatalogs**: Wählen Sie einen *Benutzerkatalog* aus, und wählen Sie dann **Bearbeiten** aus dem Menüband. Sie können dann die benutzerdefinierten Eigenschaften ändern.

-   **Löschen von Katalogen**: Wählen Sie einen oder mehrere Kataloge aus, und wählen Sie dann **Entfernen** aus dem Menüband. Damit werden der Katalog, Ihr Abonnement und die Updates aus diesen Katalogen aus dem Updates Publisher-Repository entfernt.

-   **Hinzufügen von Updates aus einem Katalog in Ihr Repository**: Wählen Sie **Importieren** aus dem Menüband, um den **Katalog importieren**-Assistenten zu starten. Weitere Informationen hierzu finden Sie unter [Importieren von Updates](#import-updates).

## <a name="import-updates"></a>Importieren von Updates
Wenn Sie einen Katalog importieren, fügt der Updates-Manager die Updates aus diesem Katalog dem Updates Publisher-Repository hinzu. Nach dem Importieren der Updates können Sie sie auf Ihrem Updateserver veröffentlichen, damit sie für verwaltete Geräte verfügbar sind.

### <a name="to-import-updates"></a>So importieren Sie Updates
1. Um den **Katalog importieren**-Assistenten zu starten, wählen Sie in einem der folgenden Arbeitsbereiche aus dem Menüband **Importieren**:

   -   Arbeitsbereich „Kataloge“

   -   Arbeitsbereich „Updates“

2. Wählen Sie auf der **Importtyp**-Seite einen oder mehrere Kataloge aus, die Sie Updates Publisher hinzugefügt haben, oder geben Sie einen Pfad zu einem Katalog an, den Sie noch nicht als Abonnement hinzugefügt haben. Wählen Sie **Weiter**, um die Zusammenfassung anzuzeigen, und sobald Sie bereit sind, wählen Sie **Weiter**, um den Importvorgang zu starten.

3. Überprüfen Sie im Fenster **Security Warning – Catalog Validation** (Sicherheitswarnung – Katalogüberprüfung) das Katalogzertifikat, und sobald Sie bereit sind, wählen Sie **Annehmen**, um die Updates zu importieren.

   > [!CAUTION]
   > Akzeptieren Sie nur Updates von Herausgebern, denen Sie vertrauen. Softwareupdates von Herausgebern, die nicht vertrauenswürdig sind, können potenziell Clientcomputer bei der Überprüfung auf Updates beschädigen.
   > 
   >  Wenn Sie einem Herausgeber nicht mehr vertrauen, entfernen Sie ihn aus der Liste vertrauenswürdiger Herausgeber. Um weitere Informationen zum Akzeptieren von Katalogen zu finden, klicken Sie auf **Weitere Informationen** im Dialogfeld **Security Warning – Catalog Validation** (Sicherheitswarnung – Katalogüberprüfung).

   Wenn Sie sich entscheiden, die Kataloge eines Herausgebers immer zu akzeptieren, wird dieser Herausgeber der [Liste vertrauenswürdiger Herausgeber](updates-publisher-options.md#trusted-publishers) hinzugefügt. Sie können diese Liste als Updates Publisher-Option überprüfen und bearbeiten.

4. Beim Importieren wird das Importieren eines Updates übersprungen, wenn das Update sich bereits im Repository befindet und eine der folgenden Aussagen zutrifft:

   -   Das Update ist seit dem letzten Import nicht geändert worden.

   -   Das Update wurde bearbeitet und verfügt über einen neuen digitalen Hash. Das Bearbeiten eines Updates verhindert, dass ein neues Update das ursprüngliche überschreibt, da so Änderungen überschrieben würden, die Sie bereitgestellt haben könnten.

5. Überprüfen Sie auf der Seite **Bestätigung** die Importergebnisse.

6. Klicken Sie auf **Schließen**, um den Assistenten abzuschließen. Sie können jetzt die Updates für diesen Katalog im Arbeitsbereich „Updates“ anzeigen.

## <a name="next-steps"></a>Nächste Schritte
Nach dem Importieren von Updates sind folgende Aktionen üblich:
-   [Verwalten Sie Updates](manage-updates-with-updates-publisher.md), um sie zusammenzustellen, zuzuweisen und für Ihren Updateserver bereitzustellen.
-   [Erstellen Sie Anwendbarkeitsregeln](updates-publisher-applicability-rules.md), um zu bestimmen, wann Updates für Ihren Updateserver bereitgestellt werden müssen.
