---
title: Erstellen von Anwendungsgruppen
titleSuffix: Configuration Manager
description: Erstellen Sie in Configuration Manager eine Gruppe von Anwendungen, die Sie als einzelne Bereitstellung an eine Benutzer- oder Gerätesammlung senden können.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a20ee62fefd401e56abbf86beed0c4685b19ea39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689738"
---
# <a name="create-application-groups"></a>Erstellen von Anwendungsgruppen

*Gilt für: Configuration Manager (Current Branch)*

<!--3555907-->

Ab Version 1906 können Sie eine Gruppe von Anwendungen erstellen, die Sie als einzelne Bereitstellung an eine Benutzer- oder Gerätesammlung senden können. Die Metadaten, die Sie für die App-Gruppe angeben, werden im Softwarecenter als Einheit dargestellt. Sie können die Apps in der Gruppe so anordnen, dass der Client sie in einer bestimmten Reihenfolge installiert.

> [!Note]  
> In dieser Version von Configuration Manager sind App-Gruppen Vorabfeatures. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../core/servers/manage/pre-release-features.md).  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Anwendungsverwaltung**, und wählen den Knoten **Anwendungsgruppe** aus.  

1. Wählen Sie im Menüband unter „Gruppe erstellen“ die Option **Anwendungsgruppe erstellen** aus.

1. Geben Sie auf der Seite **Allgemeine Informationen** Informationen zur App-Gruppe an.  

1. Fügen Sie auf der Seite **Softwarecenter** Informationen hinzu, die im Softwarecenter angezeigt werden.  

1. Klicken Sie auf der Seite **Anwendungsgruppe** auf **Hinzufügen**. Wählen Sie eine oder mehrere Apps für diese Gruppe aus. Ändern Sie ihre Reihenfolge über die Schaltflächen **Nach oben** und **Nach unten**.  

1. Schließen Sie den Assistenten ab.  

Stellen Sie die App-Gruppe auf die gleiche Weise wie eine Anwendung bereit. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](deploy-applications.md). Ab Version 1910 können Sie eine App-Gruppe für Geräte- oder Benutzersammlungen bereitstellen.

Nach dem Bereitstellen der Gruppe:

- Wenn Sie der Gruppe eine neue App hinzufügen, müssen Sie den neuen Anwendungsinhalt separat an Verteilungspunkte verteilen.

- Wenn Sie eine App in der App-Gruppe ändern, verteilen Sie den Inhalt neu.

Um Probleme bei der Bereitstellung einer App-Gruppe zu behandeln, verwenden Sie die folgenden Protokolldateien auf dem Client:

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!Important]  
> Erstellen Sie keine App-Gruppe, und stellen Sie keine App-Gruppe bereit, bevor Sie nicht die gesamte Hierarchie und die Zielkunden auf mindestens Version 1906 aktualisiert haben.

### <a name="known-issues"></a>Bekannte Probleme

- *Version 1906*: Apps in der Gruppe können nur **Windows Installer**- oder **Skript**-Bereitstellungstypen enthalten.
  - *Version 1906*: Legen Sie das Installationsverhalten des Bereitstellungstyps auf **Für System installieren** fest.
- Die folgenden Bereitstellungsoptionen funktionieren möglicherweise nicht: Warnungen, Genehmigung, stufenweise Bereitstellung, Reparatur.
- App-Gruppen können nicht exportiert oder importiert werden.
- Nehmen Sie keine Apps in die Gruppe auf, die einen Neustart erfordern, da sonst bei der Gruppenbereitstellung Fehler auftreten können.
- *Version 1906*: Sie können die App-Gruppe nicht für eine Benutzersammlung bereitstellen.
- *Version 1906*: Benutzer können die App-Gruppe im Softwarecenter nicht **deinstallieren**.
