---
title: Funktionen in Technical Preview 1608
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1608 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: ab5ad2af9b1cad051346eca28c186e7223e8253a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705498"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Funktionen in der Technical Preview 1608 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1608 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Verbesserungen am Tasksequenzschritt „ConfigMgr-Client für Erfassung vorbereiten“  
Im Schritt „Configuration Manager-Client vorbereiten“ wird der Configuration Manager-Client nun vollständig entfernt, und nicht nur die wichtigen Informationen. Wenn die Tasksequenz das erfasste Betriebssystemimage bereitstellt, wird jedes Mal ein neuer Configuration Manager-Client installiert.  


## <a name="improvements-to-software-center"></a>Verbesserungen für Software Center
* Die Registerkarten **Anwendungen**, **Updates** und **Betriebssysteme** in Software Center zeigen nun an, welche Software kürzlich hinzugefügt wurde. Zahlen im Navigationsbereich zeigen an, wie viel neue Software sich auf den Registerkarten befindet.
* Benutzer können nun Genehmigungen für Anwendungen anfordern und sich anschließend den Anforderungsverlauf in der Sicht **Anwendungsdetails** in Software Center anzeigen lassen. Die Schaltfläche **Anforderung** in **Anwendungsdetails** leitet nicht mehr an den webbasierten Anwendungskatalog weiter.

## <a name="improvements-to-asset-intelligence"></a>Verbesserungen bei Asset Intelligence
Wir haben bei den Eigenschaften für inventarisierte Software ein Feld hinzugefügt, durch das Sie eine Über-/Untergeordnet-Beziehung mit anderer Software festlegen können. In der Liste „Inventarisierte Software“ können Sie anschließend das übergeordnete Element einer beliebigen Software anzeigen und zudem die gesamte untergeordnete Software ausblenden.

### <a name="configure-a-parent-to-child-relationship"></a>Konfigurieren einer Über-/Untergeordnet-Beziehung
  1. Klicken Sie im Knoten „Inventarisierte Software“ mit der rechten Maustaste auf ein Softwareelement in der Liste **Inventarisierte Software**, und wählen Sie **Eigenschaften** aus, um übergeordnete Software festzulegen.
  2. Wählen Sie im Dialogfeld, das geöffnet wird, die Software aus, die Sie als übergeordnete Software für Ihre ursprüngliche Auswahl festlegen möchten.

### <a name="filter-the-software-display"></a>Filtern der Softwareanzeige
Nachdem Sie eine Über-/Untergeordnet-Beziehung definiert haben, können Sie Ihre Anzeige so filtern, dass sie nur Software anzeigt, die übergeordnet ist oder für die keine Beziehung definiert wurde. Dadurch wird die Software ausgeblendet, die als untergeordnetes Element einer anderen inventarisierten Software festgelegt wurde. Gehen Sie hierzu folgendermaßen vor:
   1. Wählen Sie für die Suchleiste **Kriterien hinzufügen** aus.
   2. Wählen Sie **Übergeordnete Software** aus, ändern Sie anschließend den Kriterienwert in **Ist leer**, und klicken Sie dann auf **Suchen**.

Die Anzeige zeigt jetzt nur die übergeordneten Softwareelemente oder Software an, für die keine Beziehung definiert wurde. Software, die nur einem anderen Titel untergeordnet ist, wird nicht angezeigt.

## <a name="remote-control-keyboard-translation"></a>Tastaturübersetzung bei Remotesteuerung
In der Vergangenheit übertrug Configuration Manager die Schlüsselposition vom Standort des anzeigenden Benutzers an den Standort des freigebenden Benutzers. Dies war problematisch, wenn die Tastaturkonfiguration des anzeigenden Benutzers von der des freigebenden Benutzers abwich. Beispielsweise würde ein anzeigender Benutzer mit einer englischen Tastatur ein „A“ eingeben, die französische Tastatur des freigebenden Benutzers würde jedoch ein „Q“ bereitstellen. Wir ändern das Standardverhalten dahingehend, dass das Zeichen selbst von der Tastatur des anzeigenden Benutzers an den freigebenden Benutzer übertragen wird, und beim freigebenden Benutzer kommt das an, was der anzeigende Benutzer beabsichtigt einzugeben.

Dieses Verhalten kann durch den anzeigenden Benutzer deaktiviert werden, wenn dieser bevorzugt, seine Eingabe entsprechend der Tastaturanordnung des freigebenden Benutzers vorzunehmen. Wählen Sie zum Ändern des Verhaltens in der **Configuration Manager-Remotesteuerung** **Aktion** und **Tastaturübersetzung aktivieren** aus, um die Schlüsselposition zu übertragen.

> [!NOTE]
>
> Spezielle Schlüssel wie z.B. ~!#@$% werden nicht richtig übersetzt.
