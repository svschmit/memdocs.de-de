---
title: Manuelles Bereitstellen von Softwareupdates
titleSuffix: Configuration Manager
description: Erstellen Sie manuell Softwarebereitstellungen, um Ihre Clients mit erforderlichen Softwareupdates auf dem neuesten Stand zu halten oder Out-of-Band-Updates bereitzustellen.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699238"
---
# <a name="manually-deploy-software-updates"></a>Manuelles Bereitstellen von Softwareupdates  

*Gilt für: Configuration Manager (Current Branch)*

Bei der manuellen Bereitstellung von Softwareupdates werden Softwareupdates in der Configuration Manager-Konsole ausgewählt, und der Bereitstellungsprozess wird manuell gestartet. Alternativ können Sie ausgewählte Softwareupdates zu einer Updategruppe hinzufügen und dann die Updategruppe manuell bereitstellen. Üblicherweise verwenden Sie manuelle Bereitstellungen, um Ihre Clients mit erforderlichen Softwareupdates auf dem neuesten Stand zu halten. Anschließend verwenden Sie Regeln für die automatische Bereitstellung (ADR), um laufende monatliche Softwareupdatebereitstellungen zu verwalten. Diese manuelle Methode dient ferner dazu, Out-of-Band-Softwareupdates bereitzustellen. Weitere Informationen zu der für Sie geeigneten Bereitstellungsmethode finden Sie unter [Bereitstellen von Softwareupdates](deploy-software-updates.md).



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a> Schritt 1: Festlegen der Suchkriterien für Softwareupdates  

Je nach der Kombination von Produkten und Klassifizierungen, die Ihr Standort synchronisiert, werden möglicherweise Tausende von Softwareupdates in der Configuration Manager-Konsole angezeigt. Der erste Schritt des Workflows für die manuelle Bereitstellung von Softwareupdates besteht daher darin, die Softwareupdates zu suchen, die Sie bereitstellen möchten. Sie können beispielsweise alle Softwareupdates anzeigen, die auf mehr als 50 Clientgeräten benötigt werden und die Klassifizierung **Sicherheit** oder **Kritisch** aufweisen.  

> [!IMPORTANT]  
>  Eine einzelne Softwareupdatebereitstellung ist auf 1000 Softwareupdates begrenzt.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Angeben von Suchkriterien für Softwareupdates  

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Softwareupdates**, und klicken Sie auf **Alle Softwareupdates**. Unter diesem Knoten werden alle synchronisierten Softwareupdates angezeigt.  

    > [!NOTE]  
    >  Unter dem Knoten **Alle Softwareupdates** werden nur Softwareupdates mit der Klassifizierung **Kritisch** bzw. **Sicherheit** angezeigt, die in den letzten 30 Tagen veröffentlicht wurden.  

2.  Filtern Sie im Suchbereich die erforderlichen Softwareupdate heraus. Verwenden Sie dazu eine der beiden folgenden Optionen:  

    -   Geben Sie im Suchtextfeld eine Suchzeichenfolge ein, anhand derer die Softwareupdates gefiltert werden. Geben Sie beispielsweise die Artikel- oder Bulletin-ID für ein bestimmtes Softwareupdate ein. Oder geben Sie eine Zeichenfolge ein, die im Titel mehrerer Softwareupdates angezeigt wird.  

    -   Klicken Sie auf **Kriterien hinzufügen**, und wählen Sie die Kriterien aus, anhand derer die Softwareupdates gefiltert werden sollen. Klicken Sie auf **Hinzufügen**, und geben Sie die Werte für die Kriterien ein.  

3.  Klicken Sie auf **Suchen** , um die Softwareupdates zu filtern.  

    > [!TIP]  
    >  Speichern Sie häufig verwendete Filterkriterien. Klicken Sie auf dem Menüband auf die Option **Aktuelle Suche speichern**. Rufen Sie vorherige Suchvorgänge ab, indem Sie auf **Gespeicherte Suchvorgänge** klicken.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a> Schritt 2: Erstellen einer Softwareupdategruppe, die die Softwareupdates enthält   

Mithilfe von Softwareupdategruppen können Sie Softwareupdates für die Bereitstellung vorbereiten. Gehen Sie wie folgt vor, um Softwareupdates manuell zu einer neuen Softwareupdategruppe hinzuzufügen.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Manuelles Hinzufügen von Softwareupdates zu einer neuen Softwareupdategruppe  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, und wählen Sie **Softwareupdates** aus. Wählen Sie die gewünschten Softwareupdates aus.  

2.  Klicken Sie im Menüband auf **Softwareupdategruppe erstellen**.  

3.  Geben Sie den Namen und optional eine Beschreibung für die Softwareupdategruppe ein. Achten Sie darauf, dass der Name und die Beschreibung aussagekräftig sind, damit Sie den Typ der einzelnen Updates in der Softwareupdategruppe schnell ermitteln können. Klicken Sie auf **Erstellen**.  

4.  Wählen Sie den Knoten **Softwareupdategruppen** aus, und wählen Sie dann die neue Softwareupdategruppe aus. Klicken Sie zum Anzeigen der Liste der Updates in der Gruppe im Menüband auf **Mitglieder anzeigen**.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a> Schritt 3: Herunterladen der Inhalte für die Softwareupdategruppe  

Bevor Sie die Softwareupdates bereitstellen, laden Sie den Inhalt für die Softwareupdates in die Softwareupdategruppe herunter. Mit diesem Schritt können Sie prüfen, ob der Inhalt auf Verteilungspunkten verfügbar ist, bevor Sie die Softwareupdates bereitstellen. Außerdem können Sie so unerwartete Probleme bei der Verteilung von Inhalten vermeiden. Wenn Sie diesen Schritt überspringen, lädt der Standort den Inhalt im Rahmen des Bereitstellungsprozesses herunter und stellt ihn auf den Verteilungspunkten bereit. Gehen Sie wie folgt vor, um den Inhalt für Softwareupdates in die Softwareupdategruppe herunterzuladen.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Herunterladen von Inhalt für die Softwareupdategruppe
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Überwachen des Inhaltsstatus
1. Zur Überwachung des Inhaltsstatus der Softwareupdates wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Verteilungsstatus**, und wählen Sie dann den Knoten **Inhaltsstatus** aus.  

2. Wählen Sie das Softwareupdatepaket aus, das Sie bereits zum Herunterladen der Softwareupdates in die Softwareupdategruppe ausgewählt haben.  

3. Klicken Sie im Menüband auf **Status anzeigen**.  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a> Schritt 4: Bereitstellen der Softwareupdategruppe  

Nachdem Sie festgelegt haben, welche Updates Sie bereitstellen möchten, und diese Updates zu einer Softwareupdategruppe hinzugefügt haben, können Sie die Softwareupdategruppe manuell bereitstellen.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Manuelles Bereitstellen der Softwareupdates in einer Softwareupdategruppe  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Softwareupdates**, und wählen Sie den Knoten **Softwareupdategruppen** aus.  

2. Wählen Sie die Softwareupdategruppe aus, die Sie bereitstellen möchten. Klicken Sie im Menüband auf **Bereitstellen**.   

3. Geben Sie im Assistenten zum Bereitstellen von Softwareupdates auf der Seite **Allgemein** die folgenden Einstellungen an:  

   -   **Name:** Geben Sie den Namen der Bereitstellung an. Der Name der Bereitstellung muss eindeutig sein, den Zweck der Bereitstellung angeben und sich von anderen Bereitstellungen am Standort unterscheiden lassen. Dieses Namensfeld darf maximal 256 Zeichen umfassen. Standardmäßig wird von Configuration Manager für die Bereitstellung automatisch ein Name mit folgendem Format vorgegeben: `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Beschreibung:** Geben Sie eine Beschreibung der Bereitstellung ein. Die Beschreibung ist optional, gibt aber einen Überblick über die Bereitstellung. Fügen Sie ggf. weitere relevante Informationen hinzu, die dabei helfen, die Bereitstellung am Standort zu identifizieren und von anderen Bereitstellungen zu unterscheiden. Das Feld „Beschreibung“ hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.  

   -   **Softwareupdate/Softwareupdategruppe:** Überprüfen Sie, ob die angezeigte Softwareupdategruppe bzw. das angezeigte Softwareupdate richtig ist.  

   -   **Bereitstellungsvorlage auswählen:** Geben Sie an, ob eine zuvor gespeicherte Bereitstellungsvorlage angewendet werden soll. Konfigurieren Sie eine Bereitstellungsvorlage, um allgemeine Softwareupdate-Bereitstellungseigenschaften zu speichern. Wenden Sie dann die Vorlage an, wenn Sie künftig Softwareupdates bereitstellen. Mit diesen Vorlagen sparen Sie nicht nur Zeit, sondern sorgen auch für Konsistenz bei ähnlichen Bereitstellungen.  

   -   **Sammlung:** Geben Sie die Sammlung für die Bereitstellung an. Geräte in der Sammlung erhalten die Softwareupdates in dieser Bereitstellung.  

4. Konfigurieren Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Einstellungen:  

   -   **Bereitstellungstyp:** Geben Sie den Bereitstellungstyp der Softwareupdatebereitstellung an.  

       > [!IMPORTANT]  
       >  Nachdem Sie die Softwareupdatebereitstellung erstellt haben, können Sie den Bereitstellungstyp später nicht mehr ändern.  

        - Wählen Sie **Erforderlich** aus, um eine obligatorische Softwareupdatebereitstellung zu erstellen. Die Softwareupdates werden automatisch vor dem von Ihnen konfigurierten Installationsstichtag auf Clients installiert.  

        - Wählen Sie **Verfügbar** aus, um eine optionale Softwareupdatebereitstellung zu erstellen. Diese Bereitstellung ist für Benutzer verfügbar, sodass diese die Installation über das Softwarecenter durchführen können.  

       > [!NOTE]  
       >  Wenn Sie eine als **Erforderlich** gekennzeichnete Softwareupdategruppe bereitstellen, laden Clients den Inhalt im Hintergrund herunter und berücksichtigen dabei etwaige konfigurierte BITS-Einstellungen.  
       > 
       > Als **Verfügbar** bereitgestellte Softwareupdategruppen werden von Clients im Vordergrund heruntergeladen, dabei ignorieren sie BITS-Einstellungen.  

   -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren:** Gibt an, ob Wake-On-LAN am Stichtag aktiviert werden soll. Wake-On-LAN sendet Aktivierungspakete an Computer, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Der Standort aktiviert alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, damit die Installation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert. Sie ist nur für Bereitstellungen des Typs **Erforderlich** verfügbar. Bevor Sie diese Option verwenden, müssen Sie Computer und Netzwerke für Wake-On-LAN konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Detailstufe:** Geben Sie die Detailstufe für die Zustandsmeldungen an, die Clients an den Standort melden.  

5. Konfigurieren Sie auf der Seite **Zeitplanung** die folgenden Einstellungen:  

   -   **Auswertung planen:** Geben Sie den Zeitpunkt an, zu dem Configuration Manager die verfügbare Uhrzeit und die Installationsstichtage auswertet. Wählen Sie die koordinierte Weltzeit (UTC) oder die lokale Zeit des Computers aus, auf dem die Configuration Manager-Konsole ausgeführt wird.  

       - Wenn Sie hier **Lokale Zeit des Clients** auswählen und anschließend **So bald wie möglich** als **Zeitpunkt der Verfügbarkeit der Software** auswählen, wird die aktuelle Uhrzeit des Computers mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind. Dieses Verhalten deckt sich mit dem **Installationsstichtag** und dem Zeitpunkt, wann Updates auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

   -   **Zeitpunkt der Verfügbarkeit der Software:** Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung gestellt werden sollen:  

       -   **So bald wie möglich**: Die Softwareupdates in der Bereitstellung werden den Clients so bald wie möglich zur Verfügung gestellt. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie über die Bereitstellung benachrichtigt. Die Softwareupdates sind dann für die Installation verfügbar.  

       -   **Bestimmte Zeit:** Dadurch werden die Softwareupdates, die in der für Clients verfügbaren Bereitstellung enthalten sind, zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie über die Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

   -   **Installationsstichtag:** Diese Optionen sind nur für Bereitstellungen vom Typ **Erforderlich** verfügbar. Wählen Sie eine der folgenden Einstellungen, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

       -   **So bald wie möglich:** Wählen Sie diese Einstellung aus, damit die Softwareupdates so bald wie möglich automatisch in der Bereitstellung installiert werden.  

       -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates zu einem bestimmten Termin (Datum und Uhrzeit) automatisch in der Bereitstellung installiert werden.  

           - Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines zufälligen Zeitraums von bis zu zwei Stunden. Durch die zufällige Stichtaganordnung werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Updates in der Bereitstellung durch alle Clients in der Sammlung einhergehen.   

           - Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für die Gruppe **Computer-Agent** konfigurieren, um die zufällige Installationsverzögerung für erforderliche Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Clienteinstellungen des Computer-Agents](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen innerhalb der Karenzzeit verzögern, die in den Clienteinstellungen definiert ist:** Aktivieren Sie diese Einstellung, damit Benutzern mehr Zeit zur Verfügung steht, um erforderliche Softwareupdates vor dem Stichtag zu installieren.  

       - Dieses Verhalten ist in der Regel erforderlich, wenn ein Computer lange Zeit ausgeschaltet war und viele Softwareupdates oder Anwendungen installiert werden müssen. Dieser Fall kann beispielsweise eintreten, wenn ein Benutzer aus dem Urlaub zurückkehrt und lange warten muss, während der Client überfällige Bereitstellungen installiert.  

       - Konfigurieren Sie diese Karenzzeit mit der Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** in den Clienteinstellungen. Weitere Informationen finden Sie im Abschnitt [Computer-Agent](../../core/clients/deploy/about-client-settings.md#computer-agent). Die Karenzzeit für die Erzwingung gilt für alle Bereitstellungen, für die diese Option aktiviert wird, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben.  

       - Nach Ablauf der Frist installiert der Client die Softwareupdates im ersten Zeitraum, der außerhalb der Geschäftszeiten liegt, der vom Benutzer in der Karenzzeit konfiguriert wurde. Der Benutzer kann jedoch weiterhin das Softwarecenter öffnen und die Softwareupdates zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt.  

6. Konfigurieren Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Einstellungen:  

   -   **Benutzerbenachrichtigungen:** Geben Sie an, ob die Benachrichtigung im Softwarecenter zum konfigurierten **Zeitpunkt der Verfügbarkeit der Software** angezeigt werden soll. Mit dieser Einstellung wird auch gesteuert, ob Benutzer auf den Clientcomputern benachrichtigt werden sollen. Für Bereitstellungen des Typs **Verfügbar** können Sie die Option **In Softwarecenter und allen Benachrichtigungen ausblenden** nicht auswählen.  

   -   **Verhalten am Stichtag:** Diese Einstellung ist nur für Bereitstellungen vom Typ **Erforderlich** verfügbar. Geben Sie das gewünschte Verhalten an, wenn die Bereitstellung eines Softwareupdates den Ablauf der Frist außerhalb von definierten Wartungsfenstern erreicht. Zu den Optionen gehört die Festlegung, ob die Softwareupdates installiert werden sollen und ob das System nach der Installation neu gestartet werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md). 
  
       > [!Note]
       > Dies gilt nur, wenn das Wartungsfenster für das Clientgerät konfiguriert ist. Wenn auf dem Gerät kein Wartungsfenster definiert ist, finden das Update der Installation und der Neustart immer nach Ablauf der Frist statt.

   -   **Verhalten beim Geräteneustart**: Diese Einstellung ist nur für Bereitstellungen vom Typ **Erforderlich** verfügbar. Geben Sie an, ob ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn zum Abschließen der Updateinstallation ein Systemneustart erforderlich ist.  

       > [!WARNING]  
       >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen nützlich sein oder wenn Sie nicht möchten, dass die Zielcomputer standardmäßig neu gestartet werden. Allerdings können Computer dadurch in einem unsicheren Computerzustand verbleiben. Wenn Sie zulassen, dass ein Neustart erzwungen wird, gewährleisten Sie, dass die Softwareupdateinstallation umgehend abgeschlossen wird.  

   -   **Schreibfilterverarbeitung für Windows Embedded-Geräte:** Diese Einstellung steuert das Installationsverhalten auf Windows Embedded-Geräten, auf denen ein Schreibfilter aktiviert ist. Wählen Sie diese Option aus, um Änderungen am Installationsstichtag oder während eines Wartungsfensters vorzunehmen. Die Auswahl dieser Option erfordert einen Neustart. Die Änderungen werden auf dem Gerät beibehalten. Andernfalls wird das Update installiert, auf die temporäre Überlagerung angewendet und später committet.  

       -  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert wurde.  

   - **Verhalten für erneute Auswertung der Bereitstellung von Softwareupdates bei Neustart:** Aktivieren Sie diese Einstellung, um Softwareupdatebereitstellungen so zu konfigurieren, dass auf Clients gleich nach dem Installieren von Softwareupdates und nach dem Ausführen eines Neustarts eine Kompatibilitätsprüfung für Softwareupdates durchgeführt wird. Mithilfe dieser Einstellung kann der Client nach zusätzlichen Updates suchen, die nach dem Neustart des Clients relevant werden, und diese im gleichen Wartungsfenster installieren.  

7. Konfigurieren Sie auf der Seite **Warnungen**, wie Configuration Manager Warnungen für diese Bereitstellung generiert. Prüfen Sie die letzten Warnungen von Configuration Manager zu Softwareupdates im Knoten **Softwareupdates** des Arbeitsbereichs **Softwarebibliothek**. Wenn Sie auch System Center Operations Manager verwenden, konfigurieren Sie diese Warnungen ebenso. Sie können nur Warnungen für Bereitstellungen vom Typ **Erforderlich** konfigurieren.  

8. Konfigurieren Sie auf der Seite **Downloadeinstellungen** die folgenden Einstellungen:  

    > [!NOTE]  
    >  Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben.  

    - Geben Sie an, ob Clients die Updates herunterladen und installieren sollen, wenn sie einen Verteilungspunkt in einer benachbarten oder in der standardmäßigen Standortbegrenzungsgruppe verwenden.  

    - Geben Sie an, ob Clients die Updates von einem Verteilungspunkt in der standardmäßig festgelegten Standortbegrenzungsgruppe herunterladen und installieren dürfen, wenn der Inhalt für die Softwareupdates nicht über einen Verteilungspunkt in der aktuellen oder benachbarten Begrenzungsgruppe verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob beim Download von Inhalten BranchCache verwendet werden soll. Weitere Informationen finden Sie unter [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Ab Version 1802 ist BranchCache stets auf Clients aktiviert. Diese Einstellung wurde entfernt, da Clients BranchCache verwenden, sofern diese Option vom Verteilungspunkt unterstützt wird.  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind:** Aktivieren Sie diese Einstellung, damit über das Intranet verbundene Clients Updates von Microsoft Update herunterladen, wenn diese nicht über Verteilungspunkte verfügbar sind. Internetbasierte Clients laden Softwareupdates immer von Microsoft Update herunter.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Verbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

9. Wählen Sie auf der Seite **Bereitstellungspaket** eine der folgenden Optionen aus:  

    > [!Note]  
    > Wenn Sie [Schritt 3: Herunterladen des Inhalts für die Softwareupdategruppe](#BKMK_3DownloadContent) bereits durchgeführt haben, werden die Seiten **Bereitstellungspaket**, **Verteilungspunkte** und **Sprachauswahl** im Assistenten nicht angezeigt. Fahren Sie direkt mit der Seite [Zusammenfassung](#bkmk_summary) des Assistenten fort.  
    > 
    >  Softwareupdates, die bereits in die Inhaltsbibliothek auf dem Standortserver heruntergeladen wurden, werden nicht erneut heruntergeladen. Dies ist auch der Fall, wenn Sie für die Softwareupdates ein neues Bereitstellungspaket erstellen. Wenn alle Softwareupdates bereits heruntergeladen wurden, wechselt der Assistent direkt zur Seite [Zusammenfassung](#bkmk_summary).  

    - **Bereitstellungspaket auswählen:** Fügen Sie diese Updates zu einem vorhandenen Bereitstellungspaket hinzu.  

    - **Neues Bereitstellungspaket erstellen:** Fügen Sie diese Updates zu einem neuen Bereitstellungspaket hinzu. Konfigurieren Sie die folgenden zusätzlichen Einstellungen:  

        -  **Name:** Geben Sie den Namen des Bereitstellungspakets an. Verwenden Sie einen eindeutigen Namen sein, der den Paketinhalt beschreibt. Dieser ist auf 50 Zeichen begrenzt.  

        -  **Beschreibung:** Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket ein. Die optionale Beschreibung ist auf 127 Zeichen begrenzt.  

        -  **Paketquelle:** Geben Sie den Speicherort der Quelldateien für das Softwareupdate an. Geben Sie für den Quellspeicherort einen Netzwerkpfad (z.B. `\\server\sharename\path`) ein, oder klicken Sie auf **Durchsuchen**, um den Netzwerkpfad zu suchen. Erstellen Sie den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets, bevor Sie mit der nächsten Seite fortfahren.  

            - Sie können den angegebenen Speicherort nicht als Quelle eines anderen Softwarebereitstellungspakets verwenden.  

            - Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

            -  Das Computerkonto des SMS-Anbieters und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen beide über die Berechtigung **Schreiben** für den Downloadspeicherort verfügen. Beschränken Sie den Zugriff auf den Downloadspeicherort. Diese Einschränkung verringert die Gefahr, dass Angreifer die Quelldateien von Softwareupdates manipulieren.  

        -  **Sendepriorität:** Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet diese Priorität beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.  

        - **Binäre differenzielle Replikation aktivieren:** Aktivieren Sie diese Einstellung, um den Netzwerkdatenverkehr zwischen den Standorten zu minimieren. Die binäre differenzielle Replikation (BDR) aktualisiert nur die Inhalte, die sich im Paket geändert haben, anstatt den gesamten Paketinhalt zu aktualisieren. Weitere Informationen finden Sie unter [Binäre differenzielle Replikation](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Kein Bereitstellungspaket:** Ab Version 1806 werden Softwareupdates auf Geräten bereitgestellt, ohne dass Inhalte zuvor auf Verteilungspunkte heruntergeladen und dort bereitgestellt werden. Diese Einstellung ist beim Umgang mit extrem großen Updateinhalten nützlich. Sie verwenden sie ferner, wenn Clients stets Inhalte vom Microsoft Update-Clouddienst erhalten sollen. Clients können den Inhalt in diesem Szenario auch von Peers herunterladen, die bereits über den erforderlichen Inhalt verfügen. Der Configuration Manager-Client verwaltet weiterhin den Inhaltsdownload und kann deshalb das Feature „Peercache“ von Configuration Manager oder andere Technologien verwenden, z.B. die Übermittlungsoptimierung. Dieses Feature unterstützt alle Updatetypen, die von der Configuration Manager-Softwareupdateverwaltung unterstützt werden, einschließlich Windows- und Office-Updates.<!--1357933-->  

10. Geben Sie auf der Seite **Verteilungspunkte** die Verteilungspunkte oder Verteilungspunktgruppen zum Hosten der Softwareupdatedateien an. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Wenn Sie [Schritt 3: Herunterladen des Inhalts für die Softwareupdategruppe](#BKMK_3DownloadContent) bereits durchgeführt haben, werden die Seiten **Bereitstellungspaket**, **Verteilungspunkte** und **Sprachauswahl** im Assistenten nicht angezeigt. Fahren Sie direkt mit der Seite [Zusammenfassung](#bkmk_summary) des Assistenten fort.  

11. Geben Sie auf der Seite **Downloadort** an, ob die Softwareupdatedateien aus dem Internet oder dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:  

    -   **Softwareupdates aus dem Internet herunterladen:** Wählen Sie diese Einstellung aus, um die Softwareupdates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen:** Wählen Sie diese Einstellung aus, um die Softwareupdates aus einem lokalen Verzeichnis oder einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Softwareupdates können von jedem Computer mit Internetzugang vorläufig heruntergeladen werden. Sie werden dann an einem Ort im lokalen Netzwerk gespeichert, auf den der Computer zugreifen kann, auf dem der Assistent ausgeführt wird.  

12. Wählen Sie auf der Seite **Sprachauswahl** die Sprachen aus, für die der Standort die ausgewählten Softwareupdates herunterlädt. Der Standort lädt diese Updates nur dann herunter, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Softwareupdate nicht unterstützt werden, schlägt das Herunterladen des Updates fehl.  

    > [!Note]  
    > Wenn Sie [Schritt 3: Herunterladen des Inhalts für die Softwareupdategruppe](#BKMK_3DownloadContent) bereits durchgeführt haben, werden die Seiten **Bereitstellungspaket**, **Verteilungspunkte** und **Sprachauswahl** im Assistenten nicht angezeigt. Fahren Sie direkt mit der Seite [Zusammenfassung](#bkmk_summary) des Assistenten fort.  

13. <a name="bkmk_summary"></a> Überprüfen Sie die Einstellungen auf der Seite **Zusammenfassung**. Klicken Sie auf **Als Vorlage speichern**, um die Einstellungen für eine Bereitstellungsvorlage zu speichern. Geben Sie einen Namen ein, und wählen Sie die Einstellungen aus, die Sie in der Vorlage einschließen möchten. Klicken Sie anschließend auf **Speichern**. Zum Ändern einer konfigurierten Einstellung klicken Sie auf die entsprechende Assistentenseite, und nehmen Sie die Änderung vor.  

    -  Der Vorlagenname kann alphanumerische ASCII-Zeichen sowie die Zeichen `\` (umgekehrter Schrägstrich) oder `'` (einfaches Anführungszeichen) enthalten.  

14. Klicken Sie auf **Weiter** , um das Softwareupdate bereitzustellen.  

    Nachdem Sie den Assistenten abgeschlossen haben, werden die Softwareupdates von Configuration Manager in die Inhaltsbibliothek auf dem Standortserver heruntergeladen. Anschließend wird der Inhalt an die konfigurierten Verteilungspunkte verteilt, und die Softwareupdategruppe wird für Clients in der Zielsammlung bereitgestellt. Weitere Informationen zum Bereitstellungsprozess finden Sie unter [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Nächste Schritte
[Überwachen von Softwareupdates](monitor-software-updates.md)
