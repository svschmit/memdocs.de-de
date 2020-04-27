---
title: Automatisches Bereitstellen von Softwareupdates
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die automatische Bereitstellung von Softwareupdates mithilfe von Regeln für die automatische Bereitstellung (Automatic Deployment Rules, ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: eca3227a023561a099804ef0928bfee7a7aff2c6
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110439"
---
#  <a name="automatically-deploy-software-updates"></a>Automatisches Bereitstellen von Softwareupdates  

*Gilt für: Configuration Manager (Current Branch)*

Anstatt neue Updates zu einer vorhandenen Updategruppe hinzuzufügen, können Sie eine Regel für die automatischen Bereitstellung verwenden. Die Bereitstellung per ADR eignet sich insbesondere für monatliche Softwareupdates („Patch-Dienstag“) und für die Verwaltung von Endpoint Protection-Definitionsupdates. Wenn Sie Hilfe bei der Ermittlung der für Sie geeigneten Bereitstellungsmethode benötigen, lesen Sie [Bereitstellen von Softwareupdates](deploy-software-updates.md).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Erstellen einer automatischen Bereitstellungsregel  
Sie können Softwareupdates mithilfe einer ADR automatisch genehmigen und bereitstellen. Die Regel kann bei jeder Ausführung Softwareupdates zu einer neuen Softwareupdategruppe hinzufügen oder Softwareupdates zu einer vorhandenen Gruppe hinzufügen. Wenn eine Regel ausgeführt wird und Softwareupdates zu einer vorhandenen Gruppe hinzufügt, entfernt sie alle Updates aus der Gruppe. Anschließend fügt sie der Gruppe die Updates hinzu, die die von Ihnen definierten Kriterien erfüllen. 

> [!WARNING]  
>  Überprüfen Sie, ob die Synchronisierung von Softwareupdates am Standort abgeschlossen ist, bevor Sie die erste ADR erstellen. Dieser Schritt ist wichtig, wenn Sie Configuration Manager in einer anderen Sprache als Englisch ausführen. Die Klassifizierungen für Softwareupdates werden vor der ersten Synchronisierung auf Englisch angezeigt und nach dem Abschluss der Synchronisierung in der lokalisierten Sprache. Regeln, die Sie vor der Synchronisierung der Softwareupdates erstellen, können nach der Synchronisierung möglicherweise nicht verwendet werden, da die Textzeichenfolgen eventuell nicht übereinstimmen.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a> Erstellen einer Regel für die automatische Bereitstellung  

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Softwareupdates**, und wählen Sie den Knoten **Automatische Bereitstellungsregeln** aus.  

2.  Klicken Sie auf dem Menüband auf **Automatische Bereitstellungsregel erstellen**.  

3.  Konfigurieren Sie im Assistenten zum Erstellen automatischer Bereitstellungsregeln auf der Seite **Allgemein** folgende Einstellungen:  

    -   **Name:** Geben Sie den Namen der automatischen Bereitstellungsregel an. Der Name muss eindeutig sein, den Zweck der Regel angeben und sich am Configuration Manager-Standort leicht von anderen Namen unterscheiden lassen.  

    -   **Beschreibung:** Geben Sie eine Beschreibung für die automatische Bereitstellungsregel an. Die Beschreibung muss einen Überblick über die Bereitstellungsregel und alle anderen relevanten Informationen umfassen, die die Unterscheidung der Regel von anderen Regeln erleichtern. Das Feld „Beschreibung“ ist optional, hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.  

    -   **Vorlage:** Wählen Sie eine Bereitstellungsvorlage aus, um anzugeben, ob zuvor gespeicherte Konfigurationen für automatische Bereitstellungsregeln angewendet werden sollen. Konfigurieren Sie eine Bereitstellungsvorlage, die mehrere allgemeine Updates umfasst und bei der Erstellung von ADRs eingesetzt werden kann. Mit diesen Vorlagen sparen Sie nicht nur Zeit, sondern sorgen auch für Konsistenz bei ähnlichen Bereitstellungen. Wählen Sie eine der folgenden integrierten Bereitstellungsvorlagen für Softwareupdates aus:  

         - Die Vorlage **Patch-Dienstag** enthält allgemeine Einstellungen für die monatliche Bereitstellung von Softwaredefinitionsupdates.  

         - Die Vorlage **Office 365-Clientupdates** stellt allgemeine Einstellungen bereit, die bei der Bereitstellung von Updates für Office 365 Pro Plus-Clients verwendet werden sollen.
             > [!Note]
             > Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Wenn Ihre ADRs auf der Eigenschaft „Title“ aufbauen, müssen Sie sie ab dem 9. Juni 2020 bearbeiten. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)` ist ein Beispiel für den neuen Titel. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change).

         - Die Vorlage **SCEP- und Windows Defender Antivirus-Updates** stellt allgemeine Einstellungen bereit, die bei der Bereitstellung von Endpoint Protection-Definitionsupdates verwendet werden sollen.  

    -   **Sammlung:** Gibt die Zielsammlung an, die für die Bereitstellung verwendet werden soll. Mitglieder dieser Sammlung erhalten die in der Bereitstellung definierten Softwareupdates.  

    -   Entscheiden Sie, ob Softwareupdates einer neuen oder bereits vorhandenen Softwareupdategruppe hinzugefügt werden sollen. In den meisten Fällen sollten Sie beim Ausführen der ADR eine neue Softwareupdategruppe erstellen. Falls für die Regel ein aggressiverer Zeitplan gilt, bietet es sich jedoch an, eine vorhandene Gruppe auszuwählen. Wenn Sie die Regel beispielsweise täglich für Definitionsupdates ausführen, können Sie die Softwareupdates einer vorhandenen Softwareupdategruppe hinzufügen.  

    -   **Bereitstellung nach Ausführung dieser Regel aktivieren:** Geben Sie an, ob die Softwareupdatebereitstellung nach der Ausführung der automatischen Bereitstellungsregel aktiviert werden soll. Ziehen Sie folgende Optionen für diese Einstellung in Betracht:  

        -   Wenn Sie die Bereitstellung aktivieren, werden die Updates, die die Kriterien der Regel erfüllen, einer Softwareupdategruppe hinzugefügt. Der Softwareupdateinhalt wird bei Bedarf heruntergeladen. Der Inhalt wird zu den angegebenen Verteilungspunkten kopiert, und die Updates werden für die Clients in der Zielsammlung bereitgestellt.  

        -   Wenn Sie die Bereitstellung nicht aktivieren, werden die Updates, die die Kriterien der Regel erfüllen, einer Softwareupdategruppe hinzugefügt. Der Bereitstellungsinhalt des Softwareupdates wird bei Bedarf heruntergeladen und an die angegebenen Verteilungspunkte verteilt. Der Standort erstellt eine deaktivierte Bereitstellung in der Softwareupdategruppe, um zu verhindern, dass Updates für Clients bereitgestellt werden. Durch diese Option haben Sie Zeit, sich auf die Bereitstellung der Updates vorzubereiten, zu prüfen, ob die den Kriterien entsprechenden Updates geeignet sind und die Bereitstellung anschließend zu aktivieren.  

4.  Konfigurieren Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Einstellungen:  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren:** Gibt an, ob Wake-On-LAN am Stichtag aktiviert werden soll. Wake-On-LAN sendet Aktivierungspakete an Computer, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Der Standort aktiviert alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, damit die Installation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert. Bevor Sie diese Option verwenden, müssen Sie Computer und Netzwerke für Wake-On-LAN konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen zur Updateerzwingung an.  

        > [!IMPORTANT]  
        >  Stellen Sie die Detailstufe beim Bereitstellen von Definitionsupdates auf **Nur Fehler** ein, damit vom Client nur dann eine Zustandsmeldung zurückgegeben wird, wenn ein Definitionsupdate fehlschlägt. Andernfalls gehen vom Client zahlreiche Zustandsmeldungen ein, die sich auf die Leistung des Standortservers auswirken können.  
        
        > [!NOTE]  
        > Die Detailstufe **Nur Fehler** sendet nicht die Erzwingungsstatusmeldungen, die für die Nachverfolgung ausstehender Neustarts erforderlich sind.

    -   **License terms setting** (Einstellung der Lizenzbedingungen): Geben Sie an, ob Softwareupdates mit zugehörigen Lizenzbedingungen automatisch bereitgestellt werden sollen. Einige Softwareupdates enthalten Lizenzbedingungen. Bei der automatischen Bereitstellung von Softwareupdates werden die Lizenzbedingungen nicht angezeigt, und es gibt keine Option zum Annehmen der Lizenzbedingungen. Sie können alle Softwareupdates unabhängig von den zugehörigen Lizenzbedingungen automatisch bereitstellen. Alternativ können Sie auch nur Updates bereitstellen, für die es keine zugehörigen Lizenzbedingungen gibt.  

         - Zum Überprüfen der Lizenzbedingungen eines Softwareupdates wählen Sie das Softwareupdate im Arbeitsbereich **Softwarebibliothek** im Knoten **Alle Softwareupdates** aus. Klicken Sie im Menüband auf **Lizenz lesen**.    

         - Zum Identifizieren der Softwareupdates mit zugehörigen Lizenzbedingungen fügen Sie dem Ergebnisbereich im Knoten **Alle Softwareupdates** die Spalte **Lizenzbedingungen** hinzu. Klicken Sie dann auf die Spaltenüberschrift, um die Spalte nach Softwareupdates mit Lizenzbedingungen zu sortieren.  

5.  Konfigurieren Sie auf der Seite **Softwareupdates** die Kriterien für die Softwareupdates, die von der automatischen Bereitstellungsregel abgerufen und der Softwareupdategruppe hinzugefügt werden.  

     - Das Limit für Softwareupdates in einer automatischen Bereitstellungsregel ist 1.000.  

     - Filtern Sie bei Bedarf nach Inhaltsgrößen für Softwareupdates in Regeln für die automatische Bereitstellung. Weitere Informationen finden Sie unter [Configuration Manager und vereinfachte Windows-Wartung auf vorherigen Betriebssystemebene](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).  

     - Ab Version 1910 können Sie **Bereitgestellt** jetzt als Updatefilter für die Regeln zur automatischen Bereitstellung verwenden. Mit diesem Filter können neue Updates identifiziert werden, die möglicherweise auf Ihre Pilot- oder Testsammlungen angewendet werden müssen. Mit diesem Softwareupdatefilter können Sie außerdem die erneute Bereitstellung älterer Updates vermeiden. 
         - Beachten Sie bei Verwendung der Option **Bereitgestellt** als Filter, dass Sie das Update möglicherweise bereits in einer anderen Sammlung – z.B. einer Pilot- oder Testsammlung – bereitgestellt haben. <!--4852033-->
     - Ab Version 1806 ist ein Eigenschaftenfilter für die **Architektur** verfügbar. Verwenden Sie diesen Filter, um Architekturen wie Itanium und ARM64 auszuschließen, die weniger verbreitet sind. Denken Sie daran, dass es 32-Bit (x86)-Anwendungen und Komponenten gibt, die auf 64-Bit (x64)-Systemen ausgeführt werden. Wenn Sie sich nicht sicher sind, ob Sie x86 nicht benötigen, aktivieren Sie es bei der Auswahl von x64 ebenfalls.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10, Version 1903 und höher** wurde Microsoft Update als eigenes Produkt hinzugefügt, anstatt wie frühere Versionen Teil des Produkts **Windows 10** zu sein. Aufgrund dieser Änderung mussten Sie eine Reihe von manuellen Schritten ausführen, um sicherzustellen, dass Ihre Clients diese Updates sehen. Nun wurde die Anzahl der manuellen Schritte, die Sie für das neue Produkt in Configuration Manager, Version 1906 ausführen müssen, erfolgreich verringert. Weitere Informationen finden Sie unter [Konfigurieren von Produkten für Windows 10-Versionen](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later). <!--4682946-->


6. Geben Sie auf der Seite **Auswertungszeitplan** an, ob die Ausführung der automatischen Bereitstellungsregel nach einem Zeitplan aktiviert werden soll. Ist dies der Fall, klicken Sie auf **Anpassen** , und legen Sie den Wiederholungszeitplan fest.  

    - Die für den Zeitplan konfigurierte Startzeit basiert auf der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird.  

    - Die Auswertung der automatischen Bereitstellungsregel kann dreimal täglich ausgeführt werden.  

    - Legen Sie für den Auswertungszeitplan niemals eine Häufigkeit fest, die über den Zeitplan der Softwareupdatesynchronisierung hinausgeht. Diese Seite zeigt den Zeitplan für die Synchronisierung des Softwareupdatepunkts an, damit Sie die Häufigkeit des Auswertungszeitplans leichter festlegen können.  

    - Sie können die automatische Bereitstellungsregel manuell ausführen, indem Sie die Regel im Knoten **Automatische Bereitstellungsregel** der Konsole auswählen und auf dem Menüband auf **Jetzt ausführen** klicken.  

    - Ab Version 1802 können ADRs so geplant werden, dass Sie den Offset eines Basistags überprüfen können. Wenn der Patchvorgang, der am Dienstag ausgeführt werden soll, bei Ihnen beispielsweise auf einen Mittwoch fällt, kann der Zeitplan für die Auswertung für den zweiten Dienstag des Monats versetzt um einen Tag festgelegt werden.<!--1357133-->  
        - Wenn Sie die Auswertung so planen, dass sie mit einem Offset während der letzten Woche des Monats durchgeführt werden soll, und Sie einen Offset auswählen, der bis in den nächsten Monat reicht, plant der Standort die Auswertung des Zeitplans für den letzten Tag des Monats.<!--506731-->  
        ![Offset der ADR des benutzerdefinierten Auswertungszeitplans von einem Basistag](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Konfigurieren Sie auf der Seite **Bereitstellungszeitplan** die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie den Zeitpunkt an, zu dem Configuration Manager die verfügbare Uhrzeit und die Installationsstichtage auswertet. Wählen Sie die koordinierte Weltzeit (UTC) oder die lokale Zeit des Computers aus, auf dem die Configuration Manager-Konsole ausgeführt wird.  

          - Wenn Sie hier **Lokale Zeit des Clients** auswählen und anschließend **So bald wie möglich** als **Zeitpunkt der Verfügbarkeit der Software** auswählen, wird die aktuelle Uhrzeit des Computers mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind. Dieses Verhalten deckt sich mit dem **Installationsstichtag** und dem Zeitpunkt, wann Updates auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software:** Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung gestellt werden sollen:  

        -   **So bald wie möglich**: Die Softwareupdates in der Bereitstellung werden den Clients so bald wie möglich zur Verfügung gestellt. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie über die Bereitstellung benachrichtigt. Die Softwareupdates sind dann für die Installation verfügbar.  

        -   **Bestimmte Zeit:** Dadurch werden die Softwareupdates, die in der für Clients verfügbaren Bereitstellung enthalten sind, zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie über die Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates so bald wie möglich automatisch in der Bereitstellung installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates zu einem bestimmten Termin (Datum und Uhrzeit) automatisch in der Bereitstellung installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.  

             - Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines zufälligen Zeitraums von bis zu zwei Stunden. Durch die zufällige Stichtaganordnung werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Updates in der Bereitstellung durch alle Clients in der Sammlung einhergehen.  

             - Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für die Gruppe **Computer-Agent** konfigurieren, um die zufällige Installationsverzögerung für erforderliche Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Clienteinstellungen des Computer-Agents](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    -  **Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen innerhalb der Karenzzeit verzögern, die in den Clienteinstellungen definiert ist:** Aktivieren Sie diese Einstellung, damit Benutzern mehr Zeit zur Verfügung steht, um erforderliche Softwareupdates vor dem Stichtag zu installieren.  

        - Dieses Verhalten ist in der Regel erforderlich, wenn ein Computer lange Zeit ausgeschaltet war und viele Softwareupdates oder Anwendungen installiert werden müssen. Dieser Fall kann beispielsweise eintreten, wenn ein Benutzer aus dem Urlaub zurückkehrt und lange warten muss, während der Client überfällige Bereitstellungen installiert.  

        - Konfigurieren Sie diese Karenzzeit mit der Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** in den Clienteinstellungen. Weitere Informationen finden Sie im Abschnitt [Computer-Agent](../../core/clients/deploy/about-client-settings.md#computer-agent). Die Karenzzeit für die Erzwingung gilt für alle Bereitstellungen, für die diese Option aktiviert wird, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben.  

        - Nach Ablauf der Frist installiert der Client die Softwareupdates im ersten Zeitraum, der außerhalb der Geschäftszeiten liegt, der vom Benutzer in der Karenzzeit konfiguriert wurde. Der Benutzer kann jedoch weiterhin das Softwarecenter öffnen und die Softwareupdates zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt.  

8. Konfigurieren Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen:** Geben Sie an, ob die Benachrichtigung im Softwarecenter zum konfigurierten **Zeitpunkt der Verfügbarkeit der Software** angezeigt werden soll. Mit dieser Einstellung wird auch gesteuert, ob Benutzer auf den Clientcomputern benachrichtigt werden sollen.  

    -   **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten an, wenn die Bereitstellung eines Softwareupdates den Ablauf der Frist außerhalb von definierten Wartungsfenstern erreicht. Zu den Optionen gehört die Festlegung, ob die Softwareupdates installiert werden sollen und ob das System nach der Installation neu gestartet werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  
        
        > [!Note]
        > Dies gilt nur, wenn das Wartungsfenster für das Clientgerät konfiguriert ist. Wenn auf dem Gerät kein Wartungsfenster definiert ist, finden das Update der Installation und der Neustart immer nach Ablauf der Frist statt.

    -   **Verhalten beim Geräteneustart**: Geben Sie an, ob ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn zum Abschließen der Updateinstallation ein Systemneustart erforderlich ist.  

        > [!WARNING]  
        >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen nützlich sein oder wenn Sie nicht möchten, dass die Zielcomputer standardmäßig neu gestartet werden. Allerdings können Computer dadurch in einem unsicheren Computerzustand verbleiben. Wenn Sie zulassen, dass ein Neustart erzwungen wird, gewährleisten Sie, dass die Softwareupdateinstallation umgehend abgeschlossen wird.  

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte:** Diese Einstellung steuert das Installationsverhalten auf Windows Embedded-Geräten, auf denen ein Schreibfilter aktiviert ist. Wählen Sie diese Option aus, um Änderungen am Installationsstichtag oder während eines Wartungsfensters vorzunehmen. Die Auswahl dieser Option erfordert einen Neustart. Die Änderungen werden auf dem Gerät beibehalten. Andernfalls wird das Update installiert, auf die temporäre Überlagerung angewendet und später committet.  

           -  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert wurde.  

    - **Verhalten für erneute Auswertung der Bereitstellung von Softwareupdates bei Neustart:** Aktivieren Sie diese Einstellung, um Softwareupdatebereitstellungen so zu konfigurieren, dass auf Clients gleich nach dem Installieren von Softwareupdates und nach dem Ausführen eines Neustarts eine Kompatibilitätsprüfung für Softwareupdates durchgeführt wird. Mithilfe dieser Einstellung kann der Client nach zusätzlichen Updates suchen, die nach dem Neustart des Clients relevant werden, und diese im gleichen Wartungsfenster installieren.  

9. Konfigurieren Sie auf der Seite **Warnungen**, wie Configuration Manager Warnungen für diese Bereitstellung generiert. Prüfen Sie die letzten Warnungen von Configuration Manager zu Softwareupdates im Knoten **Softwareupdates** des Arbeitsbereichs **Softwarebibliothek**. Wenn Sie auch System Center Operations Manager verwenden, konfigurieren Sie diese Warnungen ebenso.  

10. Konfigurieren Sie auf der Seite **Downloadeinstellungen** die folgenden Einstellungen:  

    - Geben Sie an, ob Clients die Updates herunterladen und installieren sollen, wenn sie einen Verteilungspunkt in einer benachbarten oder in der standardmäßigen Standortbegrenzungsgruppe verwenden.  

    - Geben Sie an, ob Clients die Updates von einem Verteilungspunkt in der standardmäßig festgelegten Standortbegrenzungsgruppe herunterladen und installieren dürfen, wenn der Inhalt für die Softwareupdates nicht über einen Verteilungspunkt in der aktuellen oder benachbarten Begrenzungsgruppe verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob beim Download von Inhalten BranchCache verwendet werden soll. Weitere Informationen finden Sie unter [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Ab Version 1802 ist BranchCache stets auf Clients aktiviert. Diese Einstellung wurde entfernt, da Clients BranchCache verwenden, sofern diese Option vom Verteilungspunkt unterstützt wird.  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind:** Aktivieren Sie diese Einstellung, damit über das Intranet verbundene Clients Updates von Microsoft Update herunterladen, wenn diese nicht über Verteilungspunkte verfügbar sind. Internetbasierte Clients laden Softwareupdates immer von Microsoft Update herunter.  

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Verbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

    > [!NOTE]  
    >  Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben.   

11. Wählen Sie auf der Seite **Bereitstellungspaket** eine der folgenden Optionen aus:  

    - **Bereitstellungspaket auswählen:** Fügen Sie diese Updates zu einem vorhandenen Bereitstellungspaket hinzu.  

    - **Neues Bereitstellungspaket erstellen:** Fügen Sie diese Updates zu einem neuen Bereitstellungspaket hinzu. Konfigurieren Sie die folgenden zusätzlichen Einstellungen:  

        -  **Name:** Geben Sie den Namen des Bereitstellungspakets an. Verwenden Sie einen eindeutigen Namen sein, der den Paketinhalt beschreibt. Dieser ist auf 50 Zeichen begrenzt.  

        -  **Beschreibung:** Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket ein. Die optionale Beschreibung ist auf 127 Zeichen begrenzt.  

        -  **Paketquelle**: Gibt den Speicherort der Quelldateien für das Softwareupdate an. Geben Sie für den Quellspeicherort einen Netzwerkpfad (z.B. `\\server\sharename\path`) ein, oder klicken Sie auf **Durchsuchen**, um den Netzwerkpfad zu suchen. Erstellen Sie den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets, bevor Sie mit der nächsten Seite fortfahren.  

            - Sie können den angegebenen Speicherort nicht als Quelle eines anderen Softwarebereitstellungspakets verwenden.  

            - Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

            -  Das Computerkonto des SMS-Anbieters und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen beide über die Berechtigung **Schreiben** für den Downloadspeicherort verfügen. Beschränken Sie den Zugriff auf den Downloadspeicherort. Diese Einschränkung verringert die Gefahr, dass Angreifer die Quelldateien von Softwareupdates manipulieren.  

        -  **Sendepriorität:** Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet diese Priorität beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.  

        - **Binäre differenzielle Replikation aktivieren:** Aktivieren Sie diese Einstellung, um den Netzwerkdatenverkehr zwischen den Standorten zu minimieren. Die binäre differenzielle Replikation (BDR) aktualisiert nur die Inhalte, die sich im Paket geändert haben, anstatt den gesamten Paketinhalt zu aktualisieren. Weitere Informationen finden Sie unter [Binäre differenzielle Replikation](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Kein Bereitstellungspaket:** Ab Version 1806 werden Softwareupdates auf Geräten bereitgestellt, ohne dass Inhalte zuvor auf Verteilungspunkte heruntergeladen und dort bereitgestellt werden. Diese Einstellung ist beim Umgang mit extrem großen Updateinhalten nützlich. Sie verwenden sie ferner, wenn Clients stets Inhalte vom Microsoft Update-Clouddienst erhalten sollen. Clients können den Inhalt in diesem Szenario auch von Peers herunterladen, die bereits über den erforderlichen Inhalt verfügen. Der Configuration Manager-Client verwaltet weiterhin den Inhaltsdownload und kann deshalb das Feature „Peercache“ von Configuration Manager oder andere Technologien verwenden, z.B. die Übermittlungsoptimierung. Dieses Feature unterstützt alle Updatetypen, die von der Configuration Manager-Softwareupdateverwaltung unterstützt werden, einschließlich Windows- und Office-Updates.<!--1357933-->  

        > [!Note]  
        > Nachdem Sie diese Option aktiviert und die Einstellungen angewendet haben, können Sie keine Änderungen mehr vornehmen. Die anderen Optionen werden abgeblendet dargestellt.<!--SCCMDocs-pr issue 3003-->  

12. Geben Sie auf der Seite **Verteilungspunkte** die Verteilungspunkte oder Verteilungspunktgruppen zum Hosten der Softwareupdatedateien an. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Diese Seite ist nur verfügbar, wenn Sie ein neues Softwareupdate-Bereitstellungspaket erstellen.  
  

13. Geben Sie auf der Seite **Downloadort** an, ob die Softwareupdatedateien aus dem Internet oder dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:  

    -   **Softwareupdates aus dem Internet herunterladen:** Wählen Sie diese Einstellung aus, um die Softwareupdates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen:** Wählen Sie diese Einstellung aus, um die Softwareupdates aus einem lokalen Verzeichnis oder einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Softwareupdates können von jedem Computer mit Internetzugang vorläufig heruntergeladen werden. Sie werden dann an einem Ort im lokalen Netzwerk gespeichert, auf den der Computer zugreifen kann, auf dem der Assistent ausgeführt wird.  

14. Wählen Sie auf der Seite **Sprachauswahl** die Sprachen aus, für die der Standort die ausgewählten Softwareupdates herunterlädt. Der Standort lädt diese Updates nur dann herunter, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Softwareupdate nicht unterstützt werden, schlägt das Herunterladen des Updates fehl.  

15. Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen. Klicken Sie auf **Als Vorlage speichern**, um die Einstellungen für eine Bereitstellungsvorlage zu speichern. Geben Sie einen Namen ein, und wählen Sie die Einstellungen aus, die Sie in der Vorlage einschließen möchten. Klicken Sie anschließend auf **Speichern**. Zum Ändern einer konfigurierten Einstellung klicken Sie auf die entsprechende Assistentenseite, und nehmen Sie die Änderung vor.  

    -  Der Vorlagenname kann alphanumerische ASCII-Zeichen sowie die Zeichen `\` (umgekehrter Schrägstrich) oder `'` (einfaches Anführungszeichen) enthalten.  

16. Klicken Sie auf **Weiter** , um die automatische Bereitstellungsregel zu erstellen.  

Nachdem Sie den Assistenten abgeschlossen haben, wird die ADR ausgeführt. Dadurch werden die Softwareupdates, die den angegebenen Kriterien entsprechen, einer Softwareupdategruppe hinzugefügt. Die ADR lädt daraufhin die Updates in eine Inhaltsbibliothek auf den Standortserver herunter und verteilt sie an die konfigurierten Verteilungspunkte. Die ADR stellt anschließend die Softwareupdategruppe für Clients in der Zielsammlung bereit.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Hinzufügen einer neuen Bereitstellung zu einer vorhandenen automatischen Bereitstellungsregel  

Nach der Erstellung einer ADR können Sie zusätzliche Bereitstellungen zur Regel hinzufügen. Dies hilft Ihnen dabei, die Komplexität der Bereitstellung verschiedener Updates für verschiedene Sammlungen zu verwalten. Jede neue Bereitstellung verfügt über sämtliche Funktionen und die Bereitstellungsüberwachungsumgebung.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Hinzufügen einer neuen Bereitstellung zu einer vorhandenen ADR  

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Softwareupdates**, und wählen Sie den Knoten **Automatische Bereitstellungsregeln** und die gewünschte Regel aus.  

2.  Klicken Sie im Menüband auf **Bereitstellung hinzufügen**.   

3.  Konfigurieren Sie auf der Seite **Sammlung** des Assistenten zum Hinzufügen einer Bereitstellung die verfügbaren Einstellungen auf ähnliche Weise wie bei der Seite **Allgemein** des Assistenten zum Erstellen automatischer Bereitstellungsregeln. Weitere Informationen finden Sie im vorherigen Abschnitt unter [Erstellen einer Regel für die automatische Bereitstellung](#bkmk_adr-process). Zum restlichen Inhalt des Assistenten zum Hinzufügen einer Bereitstellung zählen folgende Seiten, die ebenfalls mit den obigen Beschreibungen übereinstimmen:  

     - Bereitstellungseinstellungen
     - Bereitstellungszeitplan
     - Benutzererfahrung
     - Warnungen
     - Downloadeinstellungen  

Bereitstellungen können auch programmgesteuert mit Windows PowerShell-Cmdlets hinzugefügt werden. Eine vollständige Beschreibung der Verwendung dieser Methode finden Sie unter [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment).

Weitere Informationen zum Bereitstellungsprozess finden Sie unter [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Nächste Schritte
[Überwachen von Softwareupdates](monitor-software-updates.md)
