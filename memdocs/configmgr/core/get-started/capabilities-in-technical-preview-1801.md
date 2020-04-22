---
title: Technical Preview 1801 | Microsoft-Dokumentation
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1801 zur Verfügung stehen.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9b60c8f170b68e85474cf55515a5739d412ac868
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705038"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Funktionen in der Technical Preview 1801 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1801 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. 

Lesen Sie sich die Informationen unter [Technical Preview für Configuration Manager](technical-preview.md) durch, bevor Sie diese Technical Preview-Version installieren. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Bekannte Probleme in dieser Technical Preview:**
- **Beim Update auf die Vorschauversion tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie über einen [primären Standortserver im Modus „Passiv“](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) verfügen, müssen Sie den Standortserver im Modus „Passiv“ deinstallieren, bevor Sie ein Update auf diese neue Preview-Version durchführen. Sie können den Standortserver im passiven Modus erneut installieren, wenn das Update an Ihrem Standort abgeschlossen wurde.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Configuration Manager-Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im Modus „Passiv“ aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen** aus.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.
  <!--sms 489412-->


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Bereitstellung in Phasen
<!-- 1357405 -->
Die Bereitstellung in Phasen automatisiert ein koordiniertes Rollout von Software in Sequenzen. Dabei werden allerdings nicht mehrere Bereitstellungen erstellt. In dieser Technical Preview-Version kann der Assistent für die Bereitstellung in Phasen für Tasksequenzen in der Verwaltungskonsole fertig gestellt werden. Es werden dabei allerdings keine Bereitstellungen erstellt. 

### <a name="try-it-out"></a>Probieren Sie es aus!  
  Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.
 
**Erstellen Sie eine Bereitstellung in Phasen für eine Tasksequenz** </br>
1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.
2. Klicken Sie mit der rechten Maustaste auf eine bereits vorhandene Tasksequenz, und klicken Sie auf **Create Phased Deployment** (Bereitstellung in Phasen). 
3. Benennen Sie in der Registerkarte **Allgemein** die Bereitstellung in Phasen, fügen Sie falls gewünscht eine Beschreibung hinzu, und klicken Sie auf **Automatically create default pilot and production phases** (Standardpilotphasen und Produktionsphasen automatisch erstellen). 
4. Füllen Sie die Felder **Pilotauflistung** und **Produktionsauflistung** auf. Wählen Sie **Weiter** aus.
5. Wählen Sie in der Registerkarte **Einstellungen** für jede Einstellung des Zeitplans eine Option aus, und klicken Sie anschließend auf **Weiter**. 
6. Bearbeiten Sie die Phasen falls nötig in der Registerkarte **Phasen**, und klicken Sie auf **Weiter**.
7. Bestätigen Sie Ihre Auswahl in der Registerkarte **Zusammenfassung**, und klicken Sie auf **Weiter**, um fortzufahren.

## <a name="co-management-reporting"></a>Berichterstellung zur Co-Verwaltung
<!-- 1356648 -->
Wenn Sie die Funktionen der [Co-Verwaltung](../../comanage/overview.md) verwenden, können Sie nun ein Dashboard abrufen, das Informationen zur Co-Verwaltung in Ihrer Umgebung enthält. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, erweitern Sie das Feld **Upgradebereitschaft**, und klicken Sie anschließend auf das Dashboard **Co-Verwaltung**. Das Dashboard umfasst die folgenden Kacheln:
- **Co-verwaltete Geräte:** Der Anteil von Geräten in Ihrer Umgebung in Prozent, für die Sie die Co-Verwaltung aktiviert haben.
- **Betriebssystemverteilung:** Aufschlüsselung der Betriebssystemversionen nach Version. In diesem Diagramm werden die folgenden Gruppierungen verwendet:
  - Windows 7 und 8.x
  - Windows 10 niedriger als 1709
  - Windows 10 1709 und höher
    > [!NOTE] 
    > Windows 10 Version 1709 und höher ist eine Voraussetzung für die Co-Verwaltung.
- **Co-Verwaltungsstatus:** Erfolgreiche oder fehlgeschlagene Aufschlüsselung des Geräts in den folgenden Kategorien:
   - Erfolgreich, in Hybrid-Azure AD eingebunden
   - Erfolgreich, in Azure AD eingebunden
   - Fehler: Fehler bei automatischer Registrierung
- **Workloadübergang:** ein Balkendiagramm, das die Anzahl der von Ihnen in Microsoft Intune für die drei folgenden verfügbaren Workloads übertragenen Geräte darstellt. 
   - Kompatibilitätsrichtlinien
   - Ressourcenzugriff
   - Windows Update for Business

### <a name="prerequisites"></a>Voraussetzungen
- Auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, muss Internet Explorer 9 oder höher installiert sein.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Verbesserungen des Zeitplans für die Auswertung der automatischen Bereitstellungsregel
<!-- 1357133 -->
Auf der Grundlage des [Feedbacks von Benutzern](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling) können Sie jetzt die Auswertung der automatischen Bereitstellungsregel so planen, dass sie immer in einem bestimmten Abstand von einem festgelegten Tag durchgeführt wird. Beispielsweise wird die Regel am Donnerstag ausgewertet, wenn festgelegt ist, dass dies zwei Tage nach dem zweiten Dienstag im Monat geschehen soll. 

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen. <br/>

**Erstellen eines benutzerdefinierten Zeitplans, der in einem bestimmten Abstand von einem festgelegten Tag eine automatischen Bereitstellungsregel überprüft** </br>
1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Eintrag **Softwareupdates**, und klicken Sie auf **Automatische Bereitstellungsregeln**.
2. Klicken Sie mit der rechten Maustaste auf **Automatische Bereitstellungsregeln**, und klicken Sie dann auf **Automatische Bereitstellungsregel erstellen**. 
3. Befolgen Sie die Anweisungen, um die Registerkarten **Allgemein**, **Bereitstellungseinstellungen** und **Softwareupdates** abzuschließen. 
4. Klicken Sie in der Registerkarte **Auswertungszeitraum** auf **Regel nach Zeitplan ausführen** > **Anpassen**.
5. Wählen Sie für den angepassten Zeitplan **Monatlich** aus, und legen Sie einen festen Tag wie den zweiten Dienstag im Monat fest. 
6. Aktivieren Sie das Feld **Verschoben (Tage)** , und legen Sie die Anzahl von Tagen fest. Klicken Sie anschließend auf **OK**.  
7. Schließen Sie den **Assistenten zum Erstellen automatischer Bereitstellungsregeln** ab. 



## <a name="reassign-distribution-point"></a>Verteilungspunkt neu zuweisen
<!-- 1306937 -->
Viele Kunden verfügen über eine ausgeprägte Configuration Manager-Infrastruktur und verringern die Anzahl von primären und sekundären Standorten, um ihre Umgebung einfacher zu gestalten. Sie benötigen allerdings weiterhin Verteilungspunkte für die Standorte ihrer Zweigstellen, um Inhalte für verwaltete Clients bereitzustellen. Diese Verteilungspunkte enthalten häufig mehrere Terabytes an Inhalt. Dieser Inhalt nimmt viel Zeit in Anspruch, und es wird eine hohe Netzwerk-Bandbreite benötigt, um die Daten an die Remoteserver zu übermitteln. 

Mithilfe dieses Features können Sie einen Verteilungspunkt einem anderen primären Standort neu zuweisen, ohne dabei den Inhalt neu zuweisen zu müssen. Über diese Aktion wird ein Update für die Standortsystemzuweisung ausgeführt. Gleichzeitig wird der gesamte Inhalt dauerhaft auf dem Server gespeichert. Wenn Sie mehrere Verteilungspunkte neu zuweisen müssen, führen Sie zunächst diese Aktion auf einem einzelnen Verteilungspunkt aus, und fügen Sie anschließend einen Server nach dem anderen hinzu.

> [!IMPORTANT]
> Der Standortsystemserver kann nur die Rolle des Verteilungspunkts hosten. Wenn der Standortsystemserver eine andere Serverrolle von Configuration Manager hostet (z.B. den Zustandsmigrationspunkt), können Sie den Verteilungspunkt nicht neu zuweisen. Außerdem können Sie keinen Verteilunspunkt für die Cloud neu zuweisen. 

Diese Option funktioniert mit diesem Release nicht, da die Technical Preview eines einzelnen primären Standorts eingeschränkt ist. Ziehen Sie das Szenario in Betracht, und senden Sie **Feedback** zu den Funktionen dieser Aktion über die Registerkarte **Start** des Menübands.
1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie dann den Knoten **Verteilungspunkte** aus.
2. Klicken Sie mit der rechten Maustaste auf den Zielverteilungspunkt, und klicken Sie anschließend auf **Verteilungspunkt neu zuweisen**. 
  ![Verteilungspunkt neu zuweisen](media/1306937-reassign-dp.png)
3. Wählen Sie den Standortserver und den Standortcode aus, denen Sie diesen Verteilungspunkt neu zuweisen möchten. 
  ![Standortserver auswählen](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Verbesserungen der Hardwareinventur
<!-- 1357389 -->
Für neu hinzugefügte Klassen können Zeichenfolgen von mehr als 255 Zeichen für Eigenschaften der Hardwareinventur angegeben werden, bei denen es sich nicht um Schlüssel handelt.

### <a name="try-it-out"></a>Probieren Sie es aus!  
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.<br/>

1. Klicken Sie im Arbeitsbereich **Verwaltung** auf die **Clienteinstellungen**, markieren Sie eine Einstellung des Clientgeräts, um diese zu bearbeiten, führen Sie einen Rechtsklick durch, und klicken Sie auf **Eigenschaften**. 
2. Klicken Sie auf **Hardwareinventur** > **Klassen festlegen** > **Hinzufügen**.
3. Klicken Sie auf die Schaltfläche **Verbinden**.
4. Geben Sie einen **Computernamen** und einen **WMI-Namespace** ein, und klicken Sie ggf. auf **Rekursiv**. Geben Sie ggf. Anmeldeinformationen ein, um eine Verbindung herzustellen. Klicken Sie auf **Verbinden**, um die Namespaceklassen abzurufen.
5. Wählen Sie eine neue Klasse aus, und klicken Sie dann auf **Bearbeiten**.
6. Ändern Sie die **Länge** mindestens einer Eigenschaft, bei der es sich um eine Zeichenfolge und nicht um einen Schlüssel handelt, der aus mehr als 255 Zeichen besteht. Klicken Sie auf **OK**. 
7. Vergewissern Sie sich, dass die bearbeitete Eigenschaft für **Hardwareinventurklasse hinzufügen** ausgewählt ist, und klicken Sie auf **OK**. 
8. Erfassen Sie Hardwareinventar mit der neu hinzugefügten Klasse, die eine Eigenschaft enthält, die länger als 255 Zeichen ist. 



## <a name="improvements-to-client-settings-for-software-center"></a>Verbesserungen der Clienteinstellungen für das Softwarecenter
<!-- 1351224 & 1355146 -->
Diese Version der Technical Preview enthält Verbesserungen für das Anpassen des Softwarecenters in den Clienteinstellungen. 

1. In den Clienteinstellungen des Softwarecenter finden Sie jetzt die Schaltfläche **Verbinden**.
2. Es wurde eine Vorschau hinzugefügt, damit Sie sich ein Bild von dem Banner des Softwarecenters machen können.<!--1351224-->
    - Wenn kein Logo ausgewählt ist, wird in der Vorschau der Name des Unternehmens und die Unternehmensfarbe angezeigt.
    - Wenn ein Logo ausgewählt ist, wird in der Vorschau das Logo und der Name des Unternehmens angezeigt.  
3.  Außerdem wurde die neue Einstellung **Hide unapproved applications in Software Center** (Nicht genehmigte Anwendungen im Softwarecenter ausblenden) hinzugefügt. Wenn diese Option aktiviert ist, werden Anwendungen, die zwar für den Benutzer verfügbar sind, für die aber eine Genehmigung benötigt wird, im Softwarecenter ausgeblendet.<!--1355146-->

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**. Klicken Sie auf eine Einstellung des Clientgeräts, um diese zu bearbeiten. Klicken Sie darauf mit der rechten Maustaste, und wählen Sie **Eigenschaften** > **Softwarecenter** aus.
2.  Klicken Sie auf die Schaltfläche **Anpassen**. Testen Sie die verschiedenen Anpassungseinstellungen wie die Vorschau.
3. Aktivieren Sie die Einstellung **Hide unapproved applications in Software Center** (Nicht genehmigte Anwendungen im Softwarecenter ausblenden). Überprüfen Sie die Änderungen im Softwarecenter. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Neue Einstellungen für Windows Defender Application Guard
<!-- 1356256 -->
Es gibt zwei neue Einstellungen für die Hostinteraktion für [Windows Defender Application Guard](../../protect/deploy-use/create-deploy-application-guard-policy.md) für Windows 10 Version 1709. 
1. Sie können Websites Zugriff auf den virtuellen Grafikprozessor des Hosts erteilen. 
2. Dateien, die im Container heruntergeladen werden, können dauerhaft auf dem Host gespeichert werden. </br>



## <a name="improvements-to-run-scripts"></a>Verbesserungen für die Funktion „Skripts ausführen“
<!-- 1236459 -->
Mithilfe des [Features **Skripts ausführen**](../../apps/deploy-use/create-deploy-scripts.md) können Sie signierte PowerShell-Skripte importieren und ausführen. 
- Skripte müssen importiert anstatt kopiert und eingefügt werden, damit ihre Integrität gewahrt bleibt. 
- Importierte signierte Skripts können nach dem Import nicht bearbeitet werden.
    
>[!IMPORTANT]
>Es gibt in dieser Technical Preview zwei temporäre Einschränkungen.
>- Skripts können nur über das Feature „Skripts ausführen“ importiert werden und können nicht über die Konsole direkt bearbeitet werden.
>- Skripts mit einer Codierung, die nicht von Unicode unterstützt werden, werden möglicherweise nicht korrekt in der Konsole angezeigt. Das Skript wird trotzdem wie obenstehend beschrieben ausgeführt.





## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
