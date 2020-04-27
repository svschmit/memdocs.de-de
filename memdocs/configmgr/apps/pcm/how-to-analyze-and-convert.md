---
title: Analysieren und Konvertieren von Paketen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Pakete mit dem Paketkonvertierungs-Manager in Configuration Manager analysiert und konvertiert werden.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689038"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Analysieren und Konvertieren von Paketen mit dem Paketkonvertierungs-Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1357861-->

Bevor Sie ein Paket konvertieren können, müssen Sie es zunächst analysieren. Je nach den Ergebnissen der Analyse können Sie dann eine der folgenden Aufgaben ausführen:

- **Konvertieren** Sie das Paket in einer Anwendung. In der Liste **Paket** in der Konsole zeigt der Bereitschaftsstatus **Automatisch**an.  

- **Korrigieren und konvertieren** Sie das Paket, fügen Sie Sammlungen hinzu, und erstellen Sie globale Bedingungen. In der Liste **Paket** in der Konsole zeigt der Bereitschaftsstatus **Automatisch**an.  

- **Korrigieren und konvertieren** Sie das Paket. In der Liste **Paket** in der Konsole zeigt der Bereitschaftsstatus **Manuell**an.  

- Konvertieren Sie das Paket nicht. In der Liste **Paket** in der Konsole zeigt der Bereitschaftsstatus **Nicht anwendbar**an.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a> Analysieren von Paketen

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Anwendungsverwaltung**, und klicken Sie auf den Knoten **Pakete**.  

2. Wählen Sie das zu konvertierende Paket aus. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Paketkonvertierung** die Option **Paket analysieren** aus. Der Paketkonvertierungs-Manager analysiert das Paket.  

3. Um den Bereitschaftsstatus des Pakets zu veranschaulichen, fügen der Liste der Pakete die Spalte **Bereitschaft** hinzu. Der Bereitschaftsstatus des Pakets bestimmt die nächste Aktion:  

    - **Automatisch:** [Konvertieren von Paketen](#bkmk_convert)  

        Informationen zum Anfügen von Sammlungen und Erstellen globaler Bedingungen beim Bereitschaftsstatus **Automatisch** finden Sie unter [Korrigieren und Konvertieren von Paketen](#bkmk_fix).  

    - **Manuell:** [Korrigieren und Konvertieren von Paketen](#bkmk_fix)

    - **Nicht zutreffend:** Diesem Paket fehlt ein erforderlicher Inhalt oder ein Programm. Fügen Sie die fehlenden Inhalte oder Programme hinzu, und wiederholen Sie die Analyse. Oder lassen Sie die Pakete in einem nicht konvertierten Zustand, und setzen Sie die Bereitstellung als Paket fort.  

    - **Unbekannt**: Führen Sie zuerst den Task **Analyze** (Analysieren) aus, oder warten Sie auf die nächste geplante Analyse. Wenn sich der Zustand nicht ändert, finden Sie weitere Informationen unter [Beheben von Problemen mit dem Paketkonvertierungs-Manager](troubleshoot-pcm.md).<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a> Konvertieren von Paketen

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Anwendungsverwaltung**, und klicken Sie auf den Knoten **Pakete**.  

2. Wählen Sie das zu konvertierende Paket mit dem Bereitschaftsstatus **Automatisch** aus. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Paketkonvertierung** die Option **Paket konvertieren** aus. Der Assistent „Paket in Anwendung konvertieren“ wird geöffnet.  

3. Überprüfen Sie im Assistenten „Paket in Anwendung konvertieren“ die Liste mit den ausgewählten Paketen. Entfernen Sie alle Pakete, die Sie nicht konvertieren möchten, und klicken Sie auf **OK**. Der Paketkonvertierungs-Manager konvertiert das Paket. Im Fenster „Konvertierung abgeschlossen“ ist der Konvertierungsstatus der neuen Anwendungen aufgeführt.  

    > [!Note]  
    > Wenn Sie ein Paket konvertieren, zeichnet der Standort Datum und Uhrzeit der Konvertierung im UTC-Format auf.  

4. Befolgen Sie die Anweisungen im Fenster. Wählen Sie entweder **Anwendungen anzeigen** oder **Schließen** aus.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a> Korrigieren und Konvertieren von Paketen

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Anwendungsverwaltung**, und klicken Sie auf den Knoten **Pakete**.  

2. Wählen Sie ein Paket mit dem Bereitschaftsstatus **Manuell** oder **Automatisch** aus. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Paketkonvertierung** die Option **Korrigieren und konvertieren** aus.  

3. Überprüfen Sie im Assistenten „Paket in Anwendung konvertieren“ die Informationen auf der Seite **Paketauswahl**, und notieren Sie sich **die zu korrigierenden Elemente**. Klicken Sie dann auf **Weiter**.  

4. Überprüfen Sie auf der Seite **Abhängigkeitsüberprüfung**, ob das zu konvertierende Paket von anderen aufgeführten Paketen abhängig ist. Klicken Sie dann auf **Weiter**.  

    > [!Note]  
    > Wenn Sie keines der aufgeführten abhängigen Pakete konvertiert haben, müssen Sie diese zuerst konvertieren. Starten Sie dann die Paketkonvertierung neu.  
    >  
    > Wenn eine Abhängigkeit nicht erforderlich ist, können Sie sie löschen oder ignorieren und die Konvertierung fortsetzen.  

5. Überprüfen Sie auf der Seite **Bereitstellungstyp** die Bereitstellungstypen für die neue Anwendung. Ändern Sie ihre Prioritäten, oder löschen Sie die Bereitstellungstypen.  

6. Wenn einer der neuen Bereitstellungstypen keine zugehörige Erkennungsmethode hat, wird in der Spalte **Erkennungsmethode** ein Warnsymbol angezeigt. Führen Sie die folgenden Aktionen aus:  

    1. Klicken Sie auf **Erkennungsmethode bearbeiten**.  

    2. Klicken Sie auf **Hinzufügen**.  

    3. Geben Sie im Dialogfeld „Erkennungsregel“ einen **Einstellungstyp** an.  

    4. Geben Sie für den angegebenen Einstellungstyp die für die Erkennungsregel erforderlichen zusätzlichen Informationen ein.  

    5. Klicken Sie auf **OK**. Wiederholen Sie diesen Vorgang bei Bedarf, um für jeden Bereitstellungstyp mehrere Erkennungsmethoden hinzuzufügen.  

    6. Klicken Sie auf **OK**. Überprüfen Sie, ob in der Spalte **Erkennungsmethode** ein Symbol angezeigt wird, um eine ordnungsgemäß angegebene Erkennungsmethode zu bestätigen.  

7. Wählen Sie **Weiter** aus.  

8. Überprüfen Sie auf der Seite **Auswahl der Anforderungen** die Bereitstellungstypen für die neue Anwendung. Wählen Sie einen Bereitstellungstyp aus, und überprüfen Sie die Anforderungen für diesen Bereitstellungstyp.  

    > [!Note]  
    > Der Assistent zeigt nur die Anforderungen an, die der Paketkonvertierungs-Manager konvertiert. Es werden nicht alle WQL-Abfragen in Gerätesammlungen in Anforderungen konvertiert.  

9. Fügen Sie bei Bedarf Anforderungen für einen ausgewählten Bereitstellungstyp hinzu.  

10. Wählen Sie **Weiter** aus.  

11. Schließen Sie den Assistenten zum Erstellen der Anwendung ab.  

    > [!Note]  
    > Wenn Sie ein Paket konvertieren, zeichnet der Standort Datum und Uhrzeit der Konvertierung im UTC-Format auf.  



## <a name="monitor"></a><a name="bkmk_monitor"></a> Überwachung

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie **Paketkonvertierungsstatus** aus. Das Dashboard zeigt die Gesamtanalyse und den Konvertierungsstatus der Pakete im Standort an. Eine neue Hintergrundaufgabe fasst die Daten der Analyse automatisch zusammen.

> [!Tip]  
> Der in Configuration Manager integrierte Paketkonvertierungs-Manager verlangt von Ihnen nicht die Zeitplanung der Analyse von Paketen. Diese Aufgabe wird vom integrierten Zusammenfassungstask übernommen.

![Screenshot des Beispieldashboards für den Status der Paketkonvertierung](media/1357861-pcm-dashboard.png)
