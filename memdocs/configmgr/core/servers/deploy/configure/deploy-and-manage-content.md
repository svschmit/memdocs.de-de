---
title: Bereitstellen von Inhalten
titleSuffix: Configuration Manager
description: Hier finden Sie eine Anleitung zur Bereitstellung von Inhalten, nachdem Sie Verteilungspunkte für Configuration Manager installiert haben.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df26fe91f009a1a4f5d3c5a4f4adb5fe45bbd245
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343149"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Bereitstellen und Verwalten von Inhalt mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nach der Installation von Verteilungspunkten für Configuration Manager können Sie mit der Bereitstellung von Inhalten beginnen. In der Regel werden Inhalte über das Netzwerk an Verteilungspunkte übertragen. Es gibt aber auch andere Optionen zum Übermitteln von Inhalten an die Verteilungspunkte. Nachdem Inhalt an einen Verteilungspunkt übertragen wurde, können Sie ihn auf Verteilungspunkten aktualisieren, neu verteilen, entfernen und überprüfen.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a> Treiberpakete  
Normalerweise verteilen Sie Inhalte an Verteilungspunkte, damit diese für Clientcomputer verfügbar sind. (Ausnahme: Verwendung einer bedarfsgesteuerten Verteilung von Inhalten für eine bestimmte Bereitstellung.) Wenn Sie Inhalt verteilen, werden Inhaltsdateien von Configuration Manager in einem Paket gespeichert, das anschließend an den Verteilungspunkt verteilt wird. Der Inhalt für das Paket wird aus der Inhaltsbibliothek des Standortservers abgerufen. Die verteilbaren Inhaltstypen lauten z.B.:  

- Anwendungsbereitstellungstypen  

- Pakete  

- Bereitstellungspakete  

- Treiberpakete  

- Betriebssystemabbilder  

- Betriebssysteminstallationspakete  

- Startabbilder  

- Tasksequenzen  

Wenn Sie ein Paket erstellen, das Quelldateien enthält, wie z. B. einen Anwendungsbereitstellungstyp oder ein Bereitstellungspaket, wird der Standort, an dem das Paket erstellt wird, zum Besitzer der Paketinhaltsquelle. Die Quelldateien werden von Configuration Manager aus dem Quelldateipfad, den Sie für das Objekt angegeben haben, in die Inhaltsbibliothek auf dem Standortserver kopiert, der Besitzer der Paketinhaltsquelle ist.  Anschließend werden die Informationen von Configuration Manager an zusätzliche Standorte repliziert. (Weitere Informationen dazu finden Sie unter [Die Inhaltsbibliothek](../../../../core/plan-design/hierarchy/the-content-library.md).)  

Wenden Sie das folgende Verfahren an, um Inhalt an Verteilungspunkte zu verteilen.  

#### <a name="to-distribute-content-on-distribution-points"></a>So verteilen Sie Inhalt an Verteilungspunkte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem zu verteilenden Inhaltstyp einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung** > **Anwendungen**, und wählen Sie dann die zu verteilenden Anwendungen aus.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung** >  **Pakete**, und wählen Sie dann die zu verteilenden Pakete aus.  

    - **Bereitstellungspakete:** Erweitern Sie **Softwareupdates** >  **Bereitstellungspakete**, und wählen Sie dann die zu verteilenden Bereitstellungspakete aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme** >  **Treiberpakete**, und wählen Sie dann die zu verteilenden Treiberpakete aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme** >  **Betriebssystemimages**, und wählen Sie dann die zu verteilenden Betriebssystemimages aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme** > **Betriebssysteminstallationspakete**, und wählen Sie dann die zu verteilenden Betriebssysteminstallationspakete aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme** >  **Startimages**, und wählen Sie dann die zu verteilenden Startimages aus.  

    - **Tasksequenzen:** Erweitern Sie **Betriebssysteme** >  **Tasksequenzen**, und wählen Sie dann die zu verteilenden Tasksequenzen aus. Tasksequenzen enthalten zwar keinen Inhalt, doch ihnen sind Inhaltsabhängigkeiten zugeordnet, die verteilt werden.  

      > [!NOTE]  
      > Wenn Sie eine Tasksequenz ändern, müssen Sie den Inhalt erneut verteilen.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Inhalt verteilen**. Der Assistent für die Verteilung von Inhalt wird geöffnet.  

4.  Überprüfen Sie auf der Seite **Allgemein**, ob es sich bei dem aufgeführten Inhalt um den Inhalt handelt, den Sie verteilen möchten. Geben Sie an, ob von Configuration Manager Inhaltsabhängigkeiten erkannt werden sollen, die dem ausgewählten Inhalt zugeordnet sind, und fügen Sie der Verteilung die Abhängigkeiten hinzu. Klicken Sie dann auf **Weiter**.  

    > [!NOTE]  
    > Sie haben die Möglichkeit, die Einstellung **Zugeordnete Inhaltsabhängigkeiten erkennen und zu dieser Verteilung hinzufügen** nur für den Inhaltstyp "Anwendungen" zu konfigurieren. Configuration Manager konfiguriert Tasksequenzen automatisch und kann nicht geändert werden.  

5.  Falls die Registerkarte **Inhalt** angezeigt wird, überprüfen Sie, ob es sich bei dem aufgeführten Inhalt um den Inhalt handelt, den Sie verteilen möchten. Klicken Sie dann auf **Weiter**.  

    > [!NOTE]  
    > Die Seite **Inhalt** wird nur dann angezeigt, wenn im Assistenten auf der Seite **Allgemein** die Einstellung **Zugeordnete Inhaltsabhängigkeiten erkennen und zu dieser Verteilung hinzufügen** ausgewählt wurde.  

6.  Klicken Sie auf der Seite **Inhaltsziel** auf **Hinzufügen**, wählen Sie eine der folgenden Optionen aus, und führen Sie die entsprechenden Schritte aus:  

    - **Sammlungen:** Wählen Sie **Benutzersammlungen** oder **Gerätesammlungen**aus, und klicken Sie auf die Sammlung, die einer oder mehreren Verteilungspunktgruppen zugeordnet ist. Klicken Sie dann auf **OK**.  

        > [!NOTE]  
        > Es werden nur die Sammlungen, die einer Verteilungspunktgruppe zugeordnet sind, angezeigt. Weitere Informationen zum Zuordnen von Sammlungen zu Verteilungspunktgruppen finden Sie im Abschnitt [Verwalten von Verteilungspunktgruppen](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) des Themas [Installieren und Konfigurieren von Verteilungspunkten in Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    - **Verteilungspunkt:** Wählen Sie einen vorhandenen Verteilungspunkt aus, und klicken Sie dann auf **OK**. Verteilungspunkte, die den Inhalt bereits empfangen haben, werden nicht angezeigt.  

    - **Verteilungspunktgruppe:** Wählen Sie eine vorhandene Verteilungspunktgruppe aus, und klicken Sie dann auf **OK**. Verteilungspunktgruppen, die den Inhalt bereits empfangen haben, werden nicht angezeigt.  

    Nachdem Sie alle gewünschten Inhaltsziele hinzugefügt haben, klicken Sie auf **Weiter**.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen für die Verteilung, bevor Sie fortfahren. Klicken Sie auf **Weiter**, um den Inhalt an die ausgewählten Ziele zu verteilen.  

8.  Auf der Seite **Status** wird der Fortschritt der Verteilung angezeigt.  

9. Auf der Seite **Bestätigung** wird angezeigt, ob der Inhalt den Punkten erfolgreich zugewiesen wurde. Informationen zum Überwachen der Verteilung von Inhalten finden Sie unter [Überwachen von mit Configuration Manager verteilten Inhalten](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a> Verwenden von vorab bereitgestellten Inhalten  
Sie können Inhaltsdateien für Anwendungen und Pakettypen vorab bereitstellen:  

- Wählen Sie den erforderlichen Inhalt in der Configuration Manager-Konsole aus, und verwenden Sie dann den **Assistenten zum Erstellen von vorab bereitgestellten Inhaltsdateien**, um eine komprimierte vorab bereitgestellte Inhaltsdatei zu erstellen, die die Dateien und die zugehörigen Metadaten für den ausgewählten Inhalt enthält.  

- Sie können den Inhalt dann manuell in einen Standortserver, sekundären Standort oder Verteilungspunkt importieren.  

- Wenn Sie die vorab bereitgestellte Inhaltsdatei in einen Standortserver importieren, wird sie der Inhaltsbibliothek auf dem Standortserver hinzugefügt und dann in der Datenbank des Standortservers registriert.  

- Wenn Sie die vorab bereitgestellte Inhaltsdatei in einen Verteilungspunkt importieren, wird sie der Inhaltsbibliothek des Verteilungspunkts hinzugefügt, und an den Standortserver wird eine Statusmeldung über die Verfügbarkeit des Inhalts am Verteilungspunkt gesendet.  

**Einschränkungen und Überlegungen zu vorab bereitgestelltem Inhalt:**  

- **Wenn sich der Verteilungspunkt auf dem Standortserver befindet**, dürfen Sie den Verteilungspunkt nicht für vorab bereitgestellten Inhalt aktivieren. Verwenden Sie stattdessen die in [Vorabbereitstellen von Inhalt auf einem Verteilungspunkt auf einem Standortserver](#bkmk_dpsiteserver) beschriebene Prozedur.  

- Aktivieren Sie den Verteilungspunkt niemals für vorab bereitgestellte Inhalte, **wenn der Verteilungspunkt als Pullverteilungspunkt konfiguriert ist**. Mit der Konfiguration für vorab bereitgestellten Inhalt eines Verteilungspunkts wird die Konfiguration des Pullverteilungspunkts überschrieben. Von einem Pullverteilungspunkt, der für vorab bereitgestellten Inhalt konfiguriert ist, wird Inhalt nicht per Pullvorgang von einem Quellverteilungspunkt abgerufen, und es wird kein Inhalt vom Standortserver empfangen.  

- **Die Inhaltsbibliothek muss am Verteilungspunkt erstellt werden, bevor Sie Inhalt am Verteilungspunkt vorab bereitstellen können**. Verteilen Sie mindestens einmal Inhalt über das Netzwerk, bevor Sie Inhalt am Verteilungspunkt vorab bereitstellen.  

- **Wenn Sie Inhalt für ein Paket mit einem langen Paketquellpfad (z.B. mehr als 140 Zeichen) vorab bereitstellen**, ist es für das Befehlszeilentool „ExtractContent“ ggf. nicht möglich, den Inhalt für das Paket in die Inhaltsbibliothek zu extrahieren.  

Informationen zum Vorabbereitstellen von Inhaltsdateien finden Sie unter *Prestaged content (vorab bereitgestellter Inhalt)* im Thema [Manage network bandwidth for content management (Verwalten der Netzwerkbandbreite für das Content Management)](../../../plan-design/hierarchy/manage-network-bandwidth.md).  

Gehen Sie wie in den folgenden Abschnitten beschrieben vor, um Inhalt vorab bereitzustellen.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a> Schritt 1: Erstellen einer vorab bereitgestellten Inhaltsdatei  
Sie können eine komprimierte, vorab bereitgestellte Inhaltsdatei erstellen, die die Dateien und zugeordneten Metadaten für den in der Configuration Manager-Konsole ausgewählten Inhalt umfasst. Gehen Sie wie folgt vor, um eine vorab bereitgestellte Inhaltsdatei zu erstellen.  

##### <a name="to-create-a-prestaged-content-file"></a>So erstellen Sie eine vorab bereitgestellte Inhaltsdatei  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem vorab bereitzustellenden Inhaltstyp einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Anwendungen**, und wählen Sie dann die vorab bereitzustellenden Anwendungen aus.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Pakete**, und wählen Sie dann die vorab bereitzustellenden Pakete aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Treiberpakete**, und wählen Sie dann die vorab bereitzustellenden Treiberpakete aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssystemimages**, und wählen Sie dann die vorab bereitzustellenden Betriebssystemimages aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssysteminstallationspakete**, und wählen Sie dann die vorab bereitzustellenden Betriebssysteminstallationspakete aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Startimages**, und wählen Sie dann die vorab bereitzustellenden Startimages aus.  

    - **Tasksequenzen:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Tasksequenzen**, und wählen Sie dann die vorab bereitzustellenden Tasksequenzen aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Datei für vorab bereitgestellten Inhalt erstellen**. Der Assistent zum Erstellen von vorab bereitgestellten Inhaltsdateien wird geöffnet.  

    > [!NOTE]  
    > **Für Anwendungen:** Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Anwendung** auf **Vorab bereitgestellte Inhaltsdatei erstellen**.  
    >   
    > **Für Pakete:** Klicken Sie auf der Registerkarte **Startseite** in der Gruppe &lt;*Paketname*> auf **Vorab bereitgestellte Inhaltsdatei erstellen**.  

4.  Klicken Sie auf der Seite **Allgemein** auf **Durchsuchen**, und wählen Sie den Speicherort für die vorab bereitgestellte Inhaltsdatei aus. Geben Sie für die Datei einen Namen ein, und klicken Sie dann auf **Speichern**. Diese vorab bereitgestellte Inhaltsdatei setzen Sie auf primären Standortservern, sekundären Standortservern oder Verteilungspunkten zum Importieren des Inhalts und der Metadaten ein.  

5.  Wählen Sie für Anwendungen **Alle Abhängigkeiten exportieren** aus, damit die der Anwendung zugeordneten Abhängigkeiten von Configuration Manager erkannt und der vorab bereitgestellten Inhaltsdatei hinzugefügt werden. Diese Einstellung ist standardmäßig aktiviert.  

6.  Geben Sie unter **Administratorkommentare**optionale Kommentare zur vorab bereitgestellten Inhaltsdatei ein, und klicken Sie dann auf **Weiter**.  

7.  Überprüfen Sie auf der Seite **Inhalt** , ob es sich bei dem aufgeführten Inhalt um den Inhalt handelt, den Sie der vorab bereitgestellten Inhaltsdatei hinzufügen möchten. Klicken Sie dann auf **Weiter**.  

8.  Geben Sie auf der Seite **Inhaltsorte** die Verteilungspunkte an, von denen die Inhaltsdateien für die vorab bereitgestellte Inhaltsdatei abgerufen werden sollen. Sie können mehrere Verteilungspunkte zum Abrufen des Inhalts auswählen. Die Verteilungspunkte sind im Abschnitt Inhaltsorte aufgeführt. In der Spalte **Inhalt** wird angegeben, wie viele der ausgewählten Pakete oder Anwendungen auf jedem Verteilungspunkt verfügbar sind. Configuration Manager ruft zunächst vom ersten Verteilungspunkt in der Liste den ausgewählten Inhalt ab. Der restliche Inhalt für die vorab bereitgestellte Inhaltsdatei wird dann von den nachfolgenden Verteilungspunkten in der Liste nacheinander abgerufen. Klicken Sie auf **Nach oben** oder **Nach unten** , um die Prioritätsreihenfolge der Verteilungspunkte zu ändern. Wenn die Verteilungspunkte in der Liste nicht den gesamten ausgewählten Inhalt enthalten, müssen Sie der Liste Verteilungspunkte hinzufügen, die den Inhalt enthalten. Alternativ können Sie den Assistenten beenden, den Inhalt an mindestens einen Verteilungspunkt verteilen und dann den Assistenten neu starten.  

9. Bestätigen Sie die Details auf der Seite **Zusammenfassung** . Sie können zu vorhergehenden Seiten zurückkehren und Änderungen vornehmen. Klicken Sie auf **Weiter** , um die vorab bereitgestellte Inhaltsdatei zu erstellen.  

10. Auf der Seite **Status** wird der Inhalt angezeigt, der der vorab bereitgestellten Inhaltsdatei gerade hinzugefügt wird.  

11. Überprüfen Sie auf der Seite **Abschluss des Vorgangs** , ob die vorab bereitgestellte Inhaltsdatei erfolgreich erstellt wurde. Klicken Sie dann auf **Schließen**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a> Schritt 2: Zuweisen des Inhalts zu Verteilungspunkten  
 Nachdem Sie die Inhaltsdatei vorab bereitgestellt haben, weisen Sie den Inhalt Verteilungspunkten zu.  

> [!NOTE]  
> Wenn Sie mithilfe einer vorab bereitgestellten Inhaltsdatei die Inhaltsbibliothek auf einem Standortserver wiederherstellen und Sie die Inhaltsdateien nicht auf einem Verteilungspunkt vorab bereitstellen müssen, können Sie dieses Verfahren überspringen.  

 Gehen Sie wie folgt vor, um den Inhalt in der vorab bereitgestellten Inhaltsdatei Verteilungspunkten zuzuweisen.  

> [!IMPORTANT]  
> Stellen Sie sicher, dass die Verteilungspunkte, die Sie vorab bereitstellen möchten, als vorab bereitgestellte Verteilungspunkte konfiguriert sind bzw. dass der Inhalt über das Netzwerk an die Verteilungspunkte verteilt wird.  

##### <a name="to-assign-the-content-to-distribution-points"></a>So weisen Sie den Inhalt Verteilungspunkten zu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem Inhaltstyp, den Sie beim Erstellen der vorab bereitgestellten Inhaltsdatei ausgewählt haben, einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Anwendungen**, und wählen Sie dann die vorab bereitgestellten Anwendungen aus.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Pakete**, und wählen Sie dann die vorab bereitgestellten Pakete aus.  

    - **Bereitstellungspakete:** Erweitern Sie **Softwareupdates**, klicken Sie auf **Bereitstellungspakete**, und wählen Sie dann die vorab bereitgestellten Bereitstellungspakete aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Treiberpakete**, und wählen Sie dann die vorab bereitgestellten Treiberpakete aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssystemimages**, und wählen Sie dann die vorab bereitgestellten Betriebssystemimages aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssysteminstallationspakete**, und wählen Sie dann die vorab bereitgestellten Betriebssysteminstallationspakete aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Startimages**, und wählen Sie dann die vorab bereitgestellten Startimages aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Inhalt verteilen**. Der Assistent für die Verteilung von Inhalt wird geöffnet.  

4.  Überprüfen Sie auf der Seite **Allgemein**, ob es sich bei dem aufgeführten Inhalt um den von Ihnen vorab bereitgestellten Inhalt handelt. Geben Sie an, ob von Configuration Manager Inhaltsabhängigkeiten erkannt werden sollen, die dem ausgewählten Inhalt zugeordnet sind, und fügen Sie die Abhängigkeiten der Verteilung hinzu. Klicken Sie dann auf **Weiter**.  

    > [!NOTE]  
    > Sie haben die Möglichkeit, die Einstellung **Zugeordnete Inhaltsabhängigkeiten erkennen und zu dieser Verteilung hinzufügen** nur für den Inhaltstyp "Anwendungen" zu konfigurieren. Configuration Manager konfiguriert Tasksequenzen automatisch und kann nicht geändert werden.  

5.  Falls die Seite **Inhalt** angezeigt wird, überprüfen Sie, ob es sich bei dem aufgeführten Inhalt um den Inhalt handelt, den Sie verteilen möchten. Klicken Sie dann auf **Weiter**.  

    > [!NOTE]  
    > Die Seite **Inhalt** wird nur dann angezeigt, wenn im Assistenten auf der Seite **Allgemein** die Einstellung **Zugeordnete Inhaltsabhängigkeiten erkennen und zu dieser Verteilung hinzufügen** ausgewählt wurde.  

6.  Klicken Sie auf der Seite **Inhaltsziel** auf **Hinzufügen**, wählen Sie eine der folgenden Komponenten aus, in der die vorab bereitzustellenden Verteilungspunkte enthalten sind, und führen Sie die zugeordneten Schritte aus:  

    - **Sammlungen:** Wählen Sie **Benutzersammlungen** oder **Gerätesammlungen**aus, und klicken Sie auf die Sammlung, die einer oder mehreren Verteilungspunktgruppen zugeordnet ist. Klicken Sie dann auf **OK**.  

      > [!NOTE]  
      > Es werden nur die Sammlungen, die einer Verteilungspunktgruppe zugeordnet sind, angezeigt.  Informationen hierzu finden Sie im Abschnitt [Verwalten von Verteilungspunktgruppen](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) in dem Artikel [Installieren und Konfigurieren von Verteilungspunkten in Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    - **Verteilungspunkt:** Wählen Sie einen vorhandenen Verteilungspunkt aus, und klicken Sie dann auf **OK**. Verteilungspunkte, die den Inhalt bereits empfangen haben, werden nicht angezeigt.  

    - **Verteilungspunktgruppe:** Wählen Sie eine vorhandene Verteilungspunktgruppe aus, und klicken Sie dann auf **OK**. Verteilungspunktgruppen, die den Inhalt bereits empfangen haben, werden nicht angezeigt.  

    Nachdem Sie alle gewünschten Inhaltsziele hinzugefügt haben, klicken Sie auf **Weiter**.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen für die Verteilung, bevor Sie fortfahren. Klicken Sie auf **Weiter**, um den Inhalt an die ausgewählten Ziele zu verteilen.  

8.  Auf der Seite **Status** wird der Fortschritt der Verteilung angezeigt.  

9. Auf der Seite **Bestätigung** wird angezeigt, ob der Inhalt den Verteilungspunkten erfolgreich zugewiesen wurde. Informationen zum Überwachen der Verteilung von Inhalten finden Sie unter [Überwachen von mit Configuration Manager verteilten Inhalten](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a> Schritt 3: Extrahieren des Inhalts aus der vorab bereitgestellten Inhaltsdatei  
Nachdem Sie die vorab bereitgestellte Inhaltsdatei erstellt und den Inhalt Verteilungspunkten zugewiesen haben, können Sie die Inhaltsdateien in die Inhaltsbibliothek auf einem Standortserver oder Verteilungspunkt extrahieren. In der Regel dürften Sie die vorab bereitgestellte Inhaltsdatei auf ein tragbares Laufwerk wie ein USB-Laufwerk kopiert oder den Inhalt auf Medien wie eine DVD gebrannt haben. Die Inhaltsdatei bzw. der Inhalt müsste am Ort des Standortservers oder Verteilungspunkts, für den der Inhalt erforderlich ist, zur Verfügung stehen.  

Gehen Sie wie folgt vor, um die Inhaltsdateien mit dem Befehlszeilentool „ExtractContent“ manuell aus der vorab bereitgestellten Inhaltsdatei zu exportieren.  

> [!IMPORTANT]  
> Wenn Sie das Befehlszeilentool „ExtractContent“ ausführen, wird vom Tool während der Erstellung der vorab bereitgestellten Inhaltsdatei eine temporäre Datei erstellt. Anschließend wird die Datei in den Zielordner kopiert und die temporäre Datei gelöscht. Für diese temporäre Datei muss genügend Festplattenspeicher vorhanden sein. Andernfalls tritt während des Vorgangs ein Fehler auf. Die temporäre Datei wird am folgenden Speicherort erstellt:  
>   
> - Die temporäre Datei wird in dem Ordner erstellt, den Sie als Zielordner für die vorab bereitgestellte Inhaltsdatei angeben.  

> [!IMPORTANT]  
> Der Benutzer, der das Befehlszeilentool „ExtractContent“ ausführt, muss auf dem Computer, auf dem Sie den vorab bereitgestellten Inhalt extrahieren, über **Administratorrechte** verfügen.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>So extrahieren Sie die Inhaltsdateien aus der vorab bereitgestellten Inhaltsdatei  

1.  Kopieren Sie die vorab bereitgestellte Inhaltsdatei auf den Computer, auf dem Sie den Inhalt extrahieren möchten.  

2.  Kopieren Sie das Befehlszeilentool „ExtractContent“ aus &lt;*Configuration Manager-Installationspfad*>\bin\\&lt;*Plattform*> auf den Computer, auf dem Sie die vorab bereitgestellte Inhaltsdatei extrahieren möchten.  

3.  Öffnen Sie die Eingabeaufforderung, und suchen Sie den Ordner, der die vorab bereitgestellte Inhaltsdatei und das Tool „ExtractContent“ enthält.  

    > [!NOTE]  
    > Sie können mehrere vorab bereitgestellte Inhaltsdateien auf einem Standortserver, sekundären Standortserver oder Verteilungspunkt extrahieren.  

4.  Geben Sie Folgendes ein, um eine einzelne Datei zu importieren: **extractcontent /P:** &lt;*Speicherort der vorab bereitgestellten Datei*> **\\** &lt;*Name der vorab bereitgestellten Datei*>  **/S**.  

    Geben Sie Folgendes ein, um alle vorab bereitgestellten Dateien in den angegebenen Ordner zu importieren: **extractcontent /P:** &lt;*Speicherort der vorab bereitgestellten Datei*>  **/S**.  

    Geben Sie beispielsweise **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** ein. Dabei ist `D:\PrestagedFiles\` der Ordner für die vorab bereitgestellte Datei und `MyPrestagedFile.pkgx` der Name der vorab bereitgestellten Datei. Mit `/S` wird Configuration Manager angewiesen, nur Inhaltsdateien zu extrahieren, die neuer als die auf dem Verteilungspunkt vorhandenen Dateien sind.  

    Wenn Sie die vorab bereitgestellte Inhaltsdatei auf einem Standortserver extrahieren, werden die Inhaltsdateien der Inhaltsbibliothek auf dem Standortserver hinzugefügt. Anschließend wird die Verfügbarkeit des Inhalts in der Datenbank des Standortservers registriert. Wenn Sie die vorab bereitgestellte Inhaltsdatei auf einem Verteilungspunkt exportieren, werden die Inhaltsdateien der Inhaltsbibliothek auf dem Verteilungspunkt hinzugefügt. Vom Verteilungspunkt wird eine Statusmeldung an den übergeordneten primären Standortserver gesendet, und dann wird die Verfügbarkeit des Inhalts in der Standortdatenbank registriert.  

    > [!IMPORTANT]  
    > Im folgenden Szenario müssen Sie für den Inhalt, den Sie aus einer vorab bereitgestellten Inhaltsdatei extrahiert haben, ein Update ausführen, wenn ein Update des Inhalts auf eine neue Version ausgeführt wird:  
    >   
    >  1.  Sie erstellen eine vorab bereitgestellte Inhaltsdatei für Version 1 eines Pakets.  
    >  2.  Sie führen für die Quelldateien des Pakets ein Update mit Version 2 aus.  
    >  3.  Sie extrahieren die vorab bereitgestellte Inhaltsdatei (Version 1 des Pakets) auf einem Verteilungspunkt.  
    >   
    > Configuration Manager verteilt nicht automatisch Paketversion 2 an den Verteilungspunkt. Sie müssen eine neue vorab bereitgestellte Inhaltsdatei erstellen, die die neue Dateiversion enthält, und dann den Inhalt extrahieren, für den Verteilungspunkt ein Update ausführen, um die geänderten Dateien zu verteilen, oder alle Dateien im Paket erneut verteilen.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a> So stellen Sie Inhalt vorab auf einem Verteilungspunkt an einem Standortserver bereit  
Wenn ein Verteilungspunkt auf einem Standortserver installiert ist, müssen Sie wie folgt vorgehen, um Inhalte erfolgreich vorab bereitstellen zu können. Grund hierfür ist, dass die Inhaltsdateien sich bereits in der Inhaltsbibliothek befinden.  

Wenn der Verteilungspunkt nicht für die Vorabbereitstellung konfiguriert ist oder sich nicht auf einem Standortserver befindet, folgen Sie den Hinweisen im Abschnitt [Verwenden von vorab bereitgestellten Inhalten](#bkmk_prestage) dieses Themas.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>So stellen Sie Inhalte auf Verteilungspunkten auf einem Standortserver vorab bereit  

1.  Stellen Sie folgendermaßen sicher, dass der Verteilungspunkt nicht für die Vorabbereitstellung von Inhalten konfiguriert ist.  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

    2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Verteilungspunkte**, und wählen Sie dann den Verteilungspunkt aus, der sich auf dem Standortserver befindet.  

    3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

    4.  Vergewissern Sie sich, dass auf der Registerkarte **Allgemein** das Kontrollkästchen **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren** deaktiviert ist.  

2.  Erstellen Sie eine vorab bereitgestellte Inhaltsdatei anhand der im Abschnitt [Schritt 1: Erstellen einer vorab bereitgestellten Inhaltsdatei](#BKMK_CreatePrestagedContentFile) beschriebenen Vorgehensweise.  

3.  Weisen Sie den Inhalt dem Verteilungspunkt anhand der im Abschnitt [Schritt 2: Zuweisen des Inhalts zu Verteilungspunkten](#BKMK_AssignContentToDistributionPoint) beschriebenen Vorgehensweise zu.  

4.  Extrahieren Sie den Inhalt aus der vorab bereitgestellten Inhaltsdatei auf dem Standortserver, indem Sie die Vorgehensweise des Abschnitts [Schritt 3: Extrahieren des Inhalts aus der vorab bereitgestellten Inhaltsdatei](#BKMK_ExportContentFromPrestagedContentFile) durchführen.  

    > [!NOTE]  
    > Wenn der Verteilungspunkt sich an einem sekundären Standort befindet, warten Sie mindestens 10 Minuten. Verwenden Sie dann eine mit dem übergeordneten primären Standort verbundene Configuration Manager-Konsole, um den Inhalt dem Verteilungspunkt auf dem sekundären Standort zuzuweisen.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a> Verwalten der Inhalte, die Sie verteilt haben  
Für das Verwalten von Inhalten haben Sie die folgenden Optionen:  
- [Inhalt aktualisieren](#update-content)
- [Inhalt neu verteilen](#redistribute-content)
- [Inhalt entfernen](#remove-content)
- [Inhalt prüfen](#validate-content)

### <a name="update-content"></a>Inhalt aktualisieren
Wenn der Speicherort der Quelldatei für eine Bereitstellung aktualisiert wird, indem neue Dateien hinzugefügt oder vorhandene Dateien durch aktuellere Versionen ersetzt werden, können Sie die Inhaltsdateien an den Verteilungspunkten aktualisieren, indem Sie die Aktionen **Verteilungspunkte aktualisieren** oder **Inhalt aktualisieren** ausführen.  
- Die Inhaltsdateien werden vom Quellspeicherort des Originalpakets in die Inhaltsbibliothek auf dem Standort kopiert, der Besitzer der Paketinhaltsquelle ist.
- Die Paketversion wird erhöht  
- Für jede Instanz der Inhaltsbibliothek auf Standortservern und Verteilungspunkten werden nur die geänderten Dateien aktualisiert.  

> [!WARNING]  
> Die Paketversion von Clientanwendungen ist immer 1. Wenn Sie den Inhalt eines Anwendungsbereitstellungstyps aktualisieren, erstellt Configuration Manager eine neue Inhalts-ID für den Bereitstellungstyp, und im Paket wird auf die neue Inhalts-ID verwiesen.  

#### <a name="to-update-content-on-distribution-points"></a>So führen Sie ein Update für Inhalt an Verteilungspunkten aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem zu verteilenden Inhaltstyp einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung** > **Anwendungen**, und wählen Sie dann die zu verteilenden Anwendungen aus. Klicken Sie auf die Registerkarte **Bereitstellungstypen** , und wählen Sie dann die Bereitstellungstypen aus, für die Sie ein Update ausführen möchten.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung** > **Pakete**, und wählen Sie dann die zu aktualisierenden Pakete aus.  

    - **Bereitstellungspakete:** Erweitern Sie **Softwareupdates** > **Bereitstellungspakete**, und wählen Sie dann die zu aktualisierenden Bereitstellungspakete aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme** > **Treiberpakete**, und wählen Sie dann die zu aktualisierenden Treiberpakete aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme** > **Betriebssystemimages**, und wählen Sie dann die zu aktualisierenden Betriebssystemimages aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme** > **Betriebssysteminstallationspakete**, und wählen Sie dann die zu aktualisierenden Betriebssysteminstallationspakete aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme** >  **Startimages**, und wählen Sie dann die zu aktualisierenden Startimages aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Verteilungspunkte aktualisieren**, und klicken Sie dann auf **OK** , um zu bestätigen, dass Sie das Update ausführen möchten.  

    > [!NOTE]  
    > Wenn Sie ein Update für Anwendungsinhalt ausführen möchten, klicken Sie auf die Registerkarte **Bereitstellungstypen** , klicken mit der rechten Maustaste auf den Bereitstellungstyp, klicken auf **Inhalt aktualisieren**und dann auf **OK** , um das Inhaltsupdate zu bestätigen.  

    > [!NOTE]  
    > Wenn Sie Updates für Startabbildinhalte ausführen, wird der Assistent zum Verwalten von Verteilungspunkten geöffnet. Überprüfen Sie die Informationen auf der Seite **Zusammenfassung** , und schließen Sie den Assistenten ab, um das Update auszuführen.  

### <a name="redistribute-content"></a>Inhalt neu verteilen
Sie können ein Paket neu verteilen, um alle Inhaltsdateien im Paket an Verteilungspunkte oder Verteilungspunktgruppen zu kopieren und damit die vorhandenen Dateien zu überschreiben.  

Verwenden Sie diesen Vorgang, um Inhaltsdateien im Paket zu reparieren oder den Inhalt erneut zu senden, wenn die erste Verteilung nicht erfolgreich war. Sie können ein Paket über die folgenden Optionen neu verteilen:  

- Paketeigenschaften  
- Verteilungspunkteigenschaften  
- Eigenschaften für Verteilungspunktgruppen  


#### <a name="to-redistribute-content-from-package-properties"></a>So verteilen Sie Inhalt mithilfe der Paketeigenschaften neu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem zu verteilenden Inhaltstyp einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung** >  **Anwendungen**, und wählen Sie dann die neu zu verteilende Anwendung aus.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung** > **Pakete**, und wählen Sie dann das neu zu verteilende Paket aus.  

    - **Bereitstellungspakete:** Erweitern Sie **Softwareupdates** >  **Bereitstellungspakete**, und wählen Sie dann die neu zu verteilenden Bereitstellungspakete aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme** > **Treiberpakete**, und wählen Sie dann die neu zu verteilenden Treiberpakete aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme** > **Betriebssystemimages**, und wählen Sie dann das neu zu verteilende Betriebssystemimage aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme** > **Betriebssysteminstallationspakete**, und wählen Sie dann das neu zu verteilende Betriebssysteminstallationspaket aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme** >  **Startimages**, und wählen Sie dann das neu zu verteilende Startimage aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Inhaltsorte** . Wählen Sie den Verteilungspunkt oder die Verteilungspunktgruppe aus, an die Sie den Inhalt erneut verteilen möchten, und klicken Sie auf **Neu verteilen**. Klicken Sie dann auf **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>So verteilen Sie Inhalt mithilfe der Verteilungspunkteigenschaften neu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Verteilungspunkte**, und wählen Sie dann den Verteilungspunkt aus, an dem Sie Inhalt neu verteilen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Inhalt** , wählen Sie den neu zu verteilenden Inhalt aus, und klicken Sie auf **Neu verteilen**. Klicken Sie dann auf **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>So verteilen Sie Inhalt über die Eigenschaften für Verteilungspunktgruppen neu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Verteilungspunktgruppen**, und wählen Sie dann die Verteilungspunktgruppe aus, in der Sie Inhalt neu verteilen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Inhalt** , wählen Sie den neu zu verteilenden Inhalt aus, und klicken Sie auf **Neu verteilen**. Klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    > Der Paketinhalt wird an alle Verteilungspunkte in der Verteilungspunktgruppe neu verteilt.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Verwenden des SDKs zum Erzwingen der Inhaltsreplikation
Sie können die Windows Management Instrumentation-Klassenmethode (WMI) **RetryContentReplication** aus dem Configuration Manager-SDK verwenden, um den Verteilungs-Manager dazu zu zwingen, Inhalt in die Inhaltsbibliothek vom Quellspeicherort zu kopieren.  

Verwenden Sie diese Methode nur, um Replikation zu erzwingen, wenn Sie Inhalt erneut verteilen müssen, nachdem es Probleme mit der normalen Inhaltsreplikation gab (In der Regel wird dies mit der Verwendung des Überwachungsknotens der Konsole bestätigt).   

Weitere Informationen zu dieser SDK-Option finden Sie unter der [„RetryContentReplication“-Methode in der Klasse „SMS_CM_UpdatePackages“](../../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md).

### <a name="remove-content"></a>Inhalt entfernen
Wenn Sie an Verteilungspunkten keinen Inhalt mehr benötigen, können Sie die Inhaltsdateien vom Verteilungspunkt entfernen.  

- Paketeigenschaften  
- Verteilungspunkteigenschaften  
- Eigenschaften für Verteilungspunktgruppen  

Wenn der Inhalt jedoch einem anderen Paket zugeordnet ist, das an den gleichen Verteilungspunkt verteilt wurde, können Sie den Inhalt nicht entfernen.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>So entfernen Sie Paketinhaltsdateien aus Verteilungspunkten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem zu löschenden Inhaltstyp einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung** > **Anwendungen**, und wählen Sie dann die zu entfernende Anwendung aus.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung** > **Pakete**, und wählen Sie dann das zu entfernende Paket aus.  

    - **Bereitstellungspakete:** Erweitern Sie **Softwareupdates** > **Bereitstellungspakete**, und wählen Sie dann das zu entfernende Bereitstellungspaket aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme** > **Treiberpakete**, und wählen Sie dann das zu entfernende Treiberpaket aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme** > **Betriebssystemimages**, und wählen Sie dann das zu entfernende Betriebssystemimage aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme** > **Betriebssysteminstallationspakete**, und wählen Sie dann das zu entfernende Betriebssysteminstallationspaket aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme** > **Startimages**, und wählen Sie dann das zu entfernende Startimage aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Inhaltsorte** . Wählen Sie den Verteilungspunkt oder die Verteilungspunktgruppe aus, aus dem bzw. der Sie den Inhalt entfernen möchten, und klicken Sie auf **Entfernen**. Klicken Sie dann auf **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>So entfernen Sie Paketinhalt über die Verteilungspunkteigenschaften  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Verteilungspunkte**, und wählen Sie dann den Verteilungspunkt aus, aus dem Sie Inhalt löschen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Inhalt** , wählen Sie den zu entfernenden Inhalt aus, und klicken Sie auf **Entfernen**. Klicken Sie dann auf **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>So entfernen Sie Inhalt über die Eigenschaften für Verteilungspunktgruppen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Verteilungspunktgruppen**, und wählen Sie dann die Verteilungspunktgruppe aus, aus der Sie Inhalt entfernen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Klicken Sie auf die Registerkarte **Inhalt** , wählen Sie den zu entfernenden Inhalt aus, und klicken Sie auf **Entfernen**. Klicken Sie dann auf **OK**.  


### <a name="validate-content"></a>Inhalt prüfen
Bei der Inhaltsprüfung wird die Integrität der Inhaltsdateien auf Verteilungspunkten überprüft. Die Inhaltsprüfung wird nach einem Zeitplan ausgeführt, oder Sie können die Inhaltsprüfung über die Eigenschaften von Verteilungspunkten und Paketen manuell initiieren.  

Zu Beginn der Inhaltsprüfung werden die Inhaltsdateien auf Verteilungspunkten von Configuration Manager überprüft. Wenn der Dateihash für die Dateien auf dem Verteilungspunkt nicht den Erwartungen entspricht, gibt Configuration Manager eine Statusmeldung aus, die Sie im Arbeitsbereich **Überwachung** überprüfen können.  

Weitere Informationen zum Konfigurieren des Zeitplans für die Inhaltsprüfung finden Sie unter [Konfigurationen von Verteilungspunkten](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) im Thema [Installieren und Konfigurieren von Verteilungspunkten in Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>So initiieren Sie die Inhaltsprüfung für alle Inhalte auf einem Verteilungspunkt  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Verteilungspunkte**, und wählen Sie dann den Verteilungspunkt aus, auf dem Sie den Inhalt prüfen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie auf der Registerkarte **Inhalt** das Paket mit dem zu überprüfenden Inhalt aus, klicken Sie auf **Überprüfen**und dann auf **OK**. Klicken Sie anschließend erneut auf **OK**. Die Inhaltsprüfung für das Paket auf dem Verteilungspunkt wird initiiert.  

5.  Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie im Arbeitsbereich **Überwachung** den Knoten **Verteilungsstatus**, und klicken Sie dann auf den Knoten **Inhaltsstatus** . Der Inhalt jedes Pakettyps (z. B. Anwendung, Softwareupdatepaket und Startabbild) wird angezeigt. Weitere Informationen zum Überwachen des Status von Inhalten finden Sie unter [Überwachen von mit Configuration Manager verteilten Inhalten](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>So initiieren Sie die Inhaltsprüfung für ein Paket  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Wählen Sie im Arbeitsbereich **Softwarebibliothek** je nach dem zu überprüfenden Inhaltstyp einen der folgenden Schritte aus:  

    - **Anwendungen:** Erweitern Sie **Anwendungsverwaltung** > **Anwendungen**, und wählen Sie dann die zu prüfende Anwendung aus.  

    - **Pakete:** Erweitern Sie **Anwendungsverwaltung** > **Pakete**, und wählen Sie dann das zu prüfende Paket aus.  

    - **Bereitstellungspakete:** Erweitern Sie **Softwareupdates** > **Bereitstellungspakete**, und wählen Sie dann das zu prüfende Bereitstellungspaket aus.  

    - **Treiberpakete:** Erweitern Sie **Betriebssysteme** > **Treiberpakete**, und wählen Sie dann das zu prüfende Treiberpaket aus.  

    - **Betriebssystemimages:** Erweitern Sie **Betriebssysteme** > **Betriebssystemimages**, und wählen Sie dann das zu prüfende Betriebssystemimage aus.  

    - **Betriebssysteminstallationspakete:** Erweitern Sie **Betriebssysteme** >  **Betriebssysteminstallationspakete**, und wählen Sie dann das zu prüfende Betriebssysteminstallationspaket aus.  

    - **Startimages:** Erweitern Sie **Betriebssysteme** > **Startimages**, und wählen Sie dann das zu prüfende Startimage aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie auf der Registerkarte **Inhaltsorte** den Verteilungspunkt bzw. die Verteilungspunktgruppe mit dem zu überprüfenden Inhalt aus, klicken Sie auf **Überprüfen**und dann auf **OK**. Klicken Sie anschließend erneut auf **OK**. Die Inhaltsprüfung für den ausgewählten Verteilungspunkt bzw. die ausgewählte Verteilungspunktgruppe wird initiiert.  

5.  Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie im Arbeitsbereich **Überwachung** den Knoten **Verteilungsstatus**, und klicken Sie dann auf den Knoten **Inhaltsstatus** . Der Inhalt jedes Pakettyps (z. B. Anwendung, Softwareupdatepaket und Startabbild) wird angezeigt. Weitere Informationen zum Überwachen des Status von Inhalten finden Sie unter [Überwachen von mit Configuration Manager verteilten Inhalten](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
