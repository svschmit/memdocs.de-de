---
title: Remoteverwaltung von Windows-Computern
titleSuffix: Configuration Manager
description: Configuration Manager ermöglicht die Remoteverwaltung von Windows-Clientcomputern.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696408"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Remoteverwaltung eines Windows-Clientcomputers mithilfe von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)* Configuration Manager ermöglicht es Ihnen, über **Configuration Manager-Remotesteuerung** eine Verbindung mit Clientcomputern herzustellen. Bevor Sie die Remotesteuerung einsetzen, sollten Sie die Informationen in folgenden Artikeln lesen:  

-   [Voraussetzungen für die Remotesteuerung](prerequisites-for-remote-control.md)  

-   [Konfigurieren der Remotesteuerung](configuring-remote-control.md)  

Im Folgenden finden Sie drei Möglichkeiten, den Remotesteuerungsviewer zu starten:  

-   In der Configuration Manager-Konsole.  

-   In einer Windows-Eingabeaufforderung.  

-   Über das Windows-Menü **Start** auf einem Computer, auf dem die Configuration Manager-Konsole in der Programmgruppe **Microsoft System Center** ausgeführt wird.  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>So verwalten Sie einen Clientcomputer remote mit der Configuration Manager-Konsole  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Geräte** oder **Gerätesammlungen** aus.  

3.  Wählen Sie den Computer aus, der remote verwaltet werden soll. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Geräte** die Option **Starten** > **Remotesteuerung** aus.  

    > [!IMPORTANT]  
    >  Wenn die Clienteinstellung **Benutzer zur Vergabe der Berechtigung für Remotesteuerung auffordern** auf **Wahr**festgelegt ist, wird eine Verbindung erst dann hergestellt, wenn der Benutzer am Remotecomputer der Remotesteuerungsaufforderung zustimmt. Weitere Informationen finden Sie unter [Konfigurieren der Remotesteuerung](configuring-remote-control.md).  

4.  Wenn das Fenster **Configuration Manager-Remotesteuerung** geöffnet ist, können Sie den Clientcomputer remote verwalten. Verwenden Sie die folgenden Optionen zum Konfigurieren der Verbindung.  

    > [!NOTE]  
    >  Wenn der Computer, mit dem eine Verbindung hergestellt wird, über mehrere Monitore verfügt, wird der Inhalt all dieser Monitore im Remotesteuerungsfenster angezeigt.  

    -   **File**
        - **Verbinden** – Verbinden mit einem anderen Computer. Diese Option ist nicht verfügbar, wenn eine Remotesteuerungssitzung aktiv ist.  
        -   **Verbindung trennen** – Beendet die aktive Remotesteuerungssitzung, schließt aber nicht das Fenster **Configuration Manager-Remotesteuerung**.  
        - **Beenden** – Beendet die aktive Remotesteuerungssitzung und schließt das Fenster **Configuration Manager-Remotesteuerung**.  

        > [!NOTE]  
        >  Wenn eine Remotesteuerungssitzung beendet wird, werden die Inhalte der Zwischenablage von Windows auf dem Computer gelöscht, der angezeigt wird.


    - **Anzeigen**
      - **Farbtiefe** – Wählen Sie 16 Bits oder 32 Bits pro Pixel aus.
      -  **Vollbild**: Maximiert das Fenster **Configuration Manager-Remotesteuerung**. Drücken Sie STRG+ALT+UNTBR, um den Vollbildmodus zu beenden.  
      - **Für Verbindungen mit niedriger Bandbreite optimieren** – Wählen Sie diese Option aus, wenn die Verbindung eine niedrige Bandbreite hat.
      - **Anzeigen:**
        - **Alle Bildschirme** – In Configuration Manager 1902 hinzugefügt. Wenn der Computer, mit dem eine Verbindung hergestellt wird, über mehrere Monitore verfügt, wird der Inhalt all dieser Monitore im Remotesteuerungsfenster angezeigt. **Alle Bildschirme** ist die einzige Ansicht für Computer mit mehreren Monitoren vor 1902.
        -  **Erster Bildschirm** – In Configuration Manager 1902 hinzugefügt. Der *erste Bildschirm* befindet sich wie in den Windows-Anzeigeeinstellungen dargestellt ganz oben links. Sie können keinen bestimmten Bildschirm auswählen. Wenn Sie die Konfiguration des Viewers ändern, müssen Sie erneut eine Verbindung zur Remotesitzung herstellen. Der Viewer speichert Ihre Einstellung für zukünftige Verbindungen.
        -  **Skalierung anpassen** – Skaliert die Anzeige des Remotecomputers auf die Größe des Fensters **Configuration Manager-Remotesteuerung**.
        - **Statusleiste** – Schaltet die Anzeige der Statusleiste des Fensters **Configuration Manager-Remotesteuerung** ein/aus.  

       > [!NOTE]  
       >  Der Viewer speichert Ihre Einstellung für zukünftige Verbindungen.

    -   **Aktion**
        - **STRG+ALT+ENTF senden** – Sendet die Tastenkombination STRG+ALT+ENTF an den Remotecomputer. 
        - **Freigabe der Zwischenablage aktivieren** – Lässt das Kopieren und Einfügen von Elementen vom/auf dem Remotecomputer zu. Wenn dieser Wert geändert wird, muss die Remotesteuerungssitzung neu gestartet werden, damit die Änderung wirksam wird.   
          - Wenn die Freigabe der Zwischenablage in der Configuration Manager-Konsole nicht aktiviert sein soll, legen Sie auf dem Computer, auf dem die Konsole ausgeführt wird, den Wert des Registrierungsschlüssels **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** auf **0**fest.
        - **Tastaturübersetzung aktivieren** – Übersetzt das Tastaturlayout des Computers, auf dem die Konsole ausgeführt wird, in das Layout des verbundenen Geräts.
        - **Remotetastatur und Maus sperren**: Sperrt die Remotetastatur und Remotemaus, um den Benutzer an der Bedienung des Remotecomputers zu hindern.  

    -   **Hilfe**
        - **Info** – Zeigt die aktuelle Version des Viewers.  

5.  Benutzer am Remotecomputer können mehr Informationen zur Remotesteuerungssitzung anzeigen, wenn sie in Configuration Manager auf das Symbol **Remotesteuerung** klicken. Dabei handelt es sich um das Symbol im Infobereich von Windows oder das Symbol auf der Leiste der Remotesteuerungssitzung.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>So starten Sie den Remotesteuerungsviewer von der Windows-Befehlszeile aus  

-   Geben Sie bei der Windows-Eingabeaufforderung _<Configuration Manager-Installationsordner\>_ **\AdminConsole\Bin\i386\CmRcViewer.exe** ein.  

Folgende Befehlszeilenoptionen werden von CmRcViewer.exe unterstützt:  

- *Adresse*: Geben Sie den NetBIOS-Namen, den vollqualifizierten Domänennamen (FQDN) oder die IP-Adresse des Clientcomputers an, mit dem eine Verbindung hergestellt werden soll.
- *Standortservername*: Geben Sie den Namen des Configuration Manager-Standortservers an, an den Statusmeldungen im Zusammenhang mit der Remotesteuerungssitzung gesendet werden sollen.
- **/?** : Zeigt die Befehlszeilenoptionen für den Remotesteuerungsviewer an.  
     
**Beispiel: CmRcViewer.exe** *<Adresse\>* *<\\\Name des Standortservers>* 

> [!NOTE]  
> Der Remotesteuerungsviewer wird auf allen Betriebssystemen unterstützt, die für die Configuration Manager-Konsole unterstützt werden. Weitere Informationen finden Sie unter [Unterstützte Konfigurationen für Configuration Manager-Konsolen](../../../plan-design/configs/supported-operating-systems-consoles.md) und [Voraussetzungen für die Remotesteuerung](prerequisites-for-remote-control.md).

## <a name="next-steps"></a>Nächste Schritte

[Überwachen der Verwendung der Remotesteuerung](audit-remote-control-usage.md)
