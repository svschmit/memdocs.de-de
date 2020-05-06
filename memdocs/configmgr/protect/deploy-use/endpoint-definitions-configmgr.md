---
title: Malwaredefinitionsupdates für Endpoint Protection
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Configuration Manager-Softwareupdates zum Übermitteln von Definitionsupdates an Clientcomputer konfigurieren.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126080"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Verwenden von Configuration Manager zum Übermitteln von Definitionsupdates

*Gilt für: Configuration Manager (Current Branch)*

Konfigurieren Sie Configuration Manager-Softwareupdates so, dass Definitionsupdates automatisch an Clientcomputer übermittelt werden. Bevor Sie mit dem Erstellen von Regeln für die automatische Bereitstellung beginnen, stellen Sie sicher, dass Sie Configuration Manager-Softwareupdates konfiguriert haben. Weitere Informationen finden Sie unter [Einführung in Softwareupdates](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Dieses Verfahren ist spezifisch für Endpoint Protection. Allgemeinere Informationen zu Regeln für die automatische Bereitstellung finden Sie unter [Automatisches Bereitstellen von Softwareupdates](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie dann auf **Regeln für die automatische Bereitstellung**.

1. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Regel für die automatische Bereitstellung erstellen** aus.

1. Geben Sie im **Assistenten zum Erstellen automatischer Bereitstellungsregeln** auf der Seite **Allgemein**die folgenden Informationen an:

    - **Name:** Geben Sie einen eindeutigen Namen für die automatische Bereitstellungsregel ein.

    - **Sammlung:** Wählen Sie die Gerätesammlung aus, für die Sie Definitionsupdates bereitstellen möchten.

        > [!NOTE]
        > Sie können keine Definitionsupdates für eine Benutzersammlung bereitstellen.

1. Klicken Sie auf **Zu einer vorhandenen Softwareupdategruppe hinzufügen**.

1. Klicken Sie auf **Bereitstellung nach Ausführung dieser Regel aktivieren**.

1. Wählen Sie im Assistenten auf der Seite **Bereitstellungseinstellungen** für die **Detailstufe** die Option **Nur Fehlermeldungen** aus.

    > [!NOTE]
    > Wenn Sie **Nur Fehlermeldungen** auswählen, wird die Anzahl der Zustandsmeldungen reduziert, die von der Definitionsbereitstellung gesendet werden. Durch diese Konfiguration wird die Prozessorauslastung der Configuration Manager-Server reduziert.

1. Auf der Seite **Softwareupdates**:

    1. Wählen Sie den Eigenschaftenfilter **Updateklassifizierung** aus. Wählen Sie in der Liste **Suchkriterien** **<zu suchende Elemente\>** aus.

        Klicken Sie im Fenster **Suchkriterien** auf **Definitionsupdates** und dann auf **OK**.

    1. Wählen Sie den **Produkt**-Eigenschaftenfilter aus. Wählen Sie in der Liste **Suchkriterien** **<zu suchende Elemente\>** aus.

        Wählen Sie im Fenster **Suchkriterien** die Option **System Center Endpoint Protection** für Windows 8.1 und früher bzw. die Option **Windows Defender** für Windows 10 und höher aus, und klicken Sie dann auf **OK**.

    > [!NOTE]
    > Filtern Sie optional abgelöste Updates heraus. Wählen Sie den Eigenschaftenfilter **Abgelöst** aus. Wählen Sie in der Liste **Suchkriterien** **<zu suchende Elemente\>** aus. Klicken Sie im Fenster **Suchkriterien** auf **Nein** und dann auf **OK**.

1. Wählen Sie auf der Seite **Auswertungszeitplan** des Assistenten die Option **Regel nach jeder Synchronisierung der Softwareupdatepunkte ausführen** aus.

1. Konfigurieren Sie im Assistenten auf der Seite **Bereitstellungszeitplan** die folgenden Einstellungen:

    - **Zeit basiert auf**: Wenn die neuesten Definitionen von allen Clients zur selben Zeit installiert werden sollen, wählen Sie die Option **UTC** aus. Die tatsächliche Installationszeit variiert im Bereich von zwei Stunden.

    - **Zeitpunkt der Verfügbarkeit der Software**: Geben Sie die verfügbare Zeit für die von dieser Regel erstellte Bereitstellung an. Der angegebene Zeitpunkt muss mindestens eine Stunde nach der Ausführung der automatischen Bereitstellungsregel liegen. Durch diese Konfiguration wird sichergestellt, dass genügend Zeit zum Replizieren des Inhalts auf die Verteilungspunkte zur Verfügung steht. In einigen Definitionsupdates können auch Antischadsoftware-Engine-Updates enthalten sein, für die zum Erreichen der Verteilungspunkte mehr Zeit erforderlich sein kann.

    - **Installationsstichtag**: Wählen Sie **So bald wie möglich** aus.

        > [!NOTE]
        > Die Fristen der Softwareupdates variieren in einem Bereich von zwei Stunden. Dieses Verhalten verhindert, dass alle Clients gleichzeitig ein Update anfordern.

1. Wählen Sie im Assistenten auf der Seite **Benutzerfreundlichkeit** für **Benutzerbenachrichtigungen** die Option **In Softwarecenter und allen Benachrichtigungen ausblenden** aus. Bei dieser Konfiguration werden die Definitionsupdates im Hintergrund installiert.

1. Wählen Sie im Assistenten auf der Seite **Bereitstellungspaket** ein vorhandenes Bereitstellungspaket aus, oder erstellen Sie ein neues.

    > [!NOTE]
    > Es kann ratsam sein, Definitionsupdates in einem Paket anzuordnen, das keine anderen Softwareupdates enthält. Dadurch wird ein kleineres Definitionsupdatepaket erreicht, das somit schneller an die Verteilungspunkte repliziert werden kann.

1. Wenn Sie ein neues Bereitstellungspaket erstellen, wählen Sie im Assistenten auf der Seite **Verteilungspunkte** mindestens einen Verteilungspunkt aus. Der Inhalt für dieses Paket wird vom Standort in diese Verteilungspunkte kopiert.

1. Wählen Sie auf der Seite **Downloadort** die Option **Softwareupdates aus dem Internet herunterladen** aus.

1. Wählen Sie auf der Seite **Sprachauswahl** die gewünschten Sprachversionen der herunterzuladenden Updates aus.

1. Wählen Sie auf der Seite **Downloadeinstellungen** das erforderliche Downloadverhalten der Softwareupdates aus.

1. Schließen Sie den Assistenten ab.

Vergewissern Sie sich, dass im Knoten **Regeln für die automatische Bereitstellung** der Configuration Manager-Konsole die neue Regel angezeigt wird.

> [!div class="nextstepaction"]
> [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md)
